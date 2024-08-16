# 2048
<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1175750/8614312/280e5dc2-26f1-11e5-9f1f-5891c3ca8b26.png" alt="Screenshot"/>
</p>

Here I as demostrating on how to build this application in Docker by creating the **Dockerfile** then deploy this application on **nginx** server and host it on **AWS EBS**.

## Steps to deploy the application

#### Step 01:
Clone the application or download the Dokcerfile

#### Step 02:
Build the docker image<br>
`$ docker build -t <dockerhub-username>/2048 .`

#### Step 03:
Run the build in local machine<br>
`$ docker run -d -p 80:80 <dockerhub-username>/2048`

#### Step 04:
Open the browser and type `localhost:80`. If everything is working fine stop the docker container<br>
`$ docker stop <container-id>`

#### Step 05:
Login to AWS management console. Navigate to Elastic Beanstalk Service --> Create application.

#### Step 06:
Setup application configurations

1. Environment tier: WebServer
2. Application name: 2048
3. Application tags: Key:Game, Value:2048
4. Domain: (leave blank or set any available domain name)
5. Platform: Docker
6. Platform Branch: Docker running on 64bit Amazon Linux 2023
7. Application code: Upload your code --> Local file --> upload Dockerfile
8. Presets: Single instance
9. Service role: Use existing --> set service-role --> set ec2-role (ec2 key pair is not required)
10. Next --> skip to review --> Submit

***Leave any other settings as default***

> [!IMPORTANT]  
> If any event fails or you are using elastic beanstalk first time, you need to create new role in IAM service called aws-elasticbeanstalk-service-role. Set following permissions.<br>
> 1. AWSElasticBeanstalkEnhancedHealth
> 2. AWSElasticBeanstalkManagedUpdatesCustomerRolePolicy

> [!IMPORTANT]  
> If any event fails or you are using elastic beanstalk first time, you need to create new role in IAM service called aws-elasticbeanstalk-ec2-role. Set following permissions.<br>
> 1. AWSElasticBeanstalkMulticontainerDocker
> 2. AWSElasticBeanstalkWebTier
> 3. AWSElasticBeanstalkWorkerTier

**Beginner guide to setup [AWS Elastic Beanstalk Deployment](https://www.youtube.com/watch?v=aTQbyBUNoms&t=246s)**

# Final Result

<p align="center">
  <img src="https://github.com/user-attachments/assets/34c23c15-f5b1-4c5b-889c-88fad09a6279" alt="Screenshot"/>
</p>

<hr>

> [!TIP]
> Please feel free to follow this [guide](https://mrcloudbook.com/deploying-2048-game-on-docker-and-kubernetes-with-jenkins-ci-cd/#more-1813) if you want to learn more on how to deploy this application with Jenkins CI/CD

<hr>

**This repository is a copy of [following repository](https://github.com/gabrielecirulli/2048) and used this for testing and learning purposes. You can find the original repository I have used in [here](https://github.com/gabrielecirulli/2048).**
