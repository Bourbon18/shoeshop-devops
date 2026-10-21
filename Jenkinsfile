pipeline {
    agent {
        label 'lab-server'
    }
    environment {
        appUser = "shoeshop"
        appName = "shoe-ShoppingCart"
        appVersion = "0.0.1-SNAPSHOT"
        appType = "jar"
        processName = "${appName}-${appVersion}.${appType}"
        folderDeploy = "/datas/${appUser}"
        buildScript = "mvn clean install -DskipTests=true -Dmaven.repo.local=/datadrive/jenkins_workspace/.m2/repository"
        copyScript = "sudo cp target/${processName} ${folderDeploy}"
        permsScript = "sudo chown -R ${appUser}. ${folderDeploy}"
        
        // GIỮ NGUYÊN CẤU TRÚC: Thêm điều kiện kiểm tra (if), chỉ chạy lệnh kill khi thực sự tìm thấy PID
        killScript = "PID=\$(ps -ef | grep ${processName} | grep -v grep | awk '{print \$2}'); if [ -n \"\$PID\" ]; then sudo kill -9 \$PID; fi"
        
        // ĐỔI DẤU NHÁY: Dùng nháy kép "" bên ngoài để Jenkins nhận diện được biến ${...}, nháy đơn '' bên trong cho lệnh Linux
        runScript = "sudo su ${appUser} -c 'cd ${folderDeploy}; java -jar ${processName} > nohup.out 2>&1 &'"
    }
    stages {
        stage('build') {
            steps {
                sh(script: """ ${buildScript} """, label: "build with maven")
            }
        }
        stage('deploy') {
            steps {
                script {
                    try {
                        timeout(time: 5, unit: 'MINUTES') {
                            env.usechoice = input message: "Can it be deployed?",
                                parameters: [choice(name: 'deploy', choices: 'no\nyes', description: 'Choose "yes" if you want to deploy')]
                        }
                        if(env.usechoice == 'yes') {
                            sh(script: """ ${copyScript} """, label: "copy the .jar file into deploy folder")
                            sh(script: """ ${permsScript} """, label: "set permission folder")
                            sh(script: """ ${killScript} """, label: "terminate the running process")
                            sh(script: """ ${runScript} """, label: "run the project")
                        }
                        else {
                            echo "Do not confirm the deployment"
            
                        } 

                    } catch (Exception err) {

                    }
                }
            }
        }
    }
}
