# Shoeshop onlines
Shoe Shopping Cart built with SpringBoot, JPA, MySQL , Spring Security, Hibernate and Thymeleaf

![image](https://user-images.githubusercontent.com/29988949/75882730-9ad11680-5dd6-11ea-9648-252426582a96.png)


![image](https://user-images.githubusercontent.com/29988949/75947593-c6dfac80-5e55-11ea-8582-bce667beb9bb.png)

`ProductList Page`

![image](https://user-images.githubusercontent.com/29988949/75968115-bf35fd00-5e81-11ea-9bae-e78ff047dcfd.png)

`Cart Page`

![image](https://user-images.githubusercontent.com/29988949/75956013-da960d80-5e6b-11ea-84b2-a0ca854ef9c9.png)

## CI/CD Pipeline

Tested on self-hosted Jenkins and GitLab CI (lab environment, not public — screenshots below).

### GitLab CI
![Pipeline history](docs/screenshots/gitlab-pipelines-history.png)
![Jobs history](docs/screenshots/gitlab-jobs-history.png)
![Pipeline detail](docs/screenshots/gitlab-pipeline-detail.png)

Stages: `build` → `deploy` (manual) → `showlog` (manual)

### Jenkins
![Deploy log](docs/screenshots/jenkins-deploy-log.png)
![Build history](docs/screenshots/jenkins-build-history.png)

Stages: `build` → `deploy` (manual approval)
