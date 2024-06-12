## Deployment guide for myself

This project is a deplyoment guide for AWS, azure, AWS + docker, Azure + docker for myself because i probably will end up forgetting everything after 3 days.

### STUPID MISTAKES I HAVE MADE
* Using the wrong python version
* Using the wrong file name in docker file(app.py instead of applicaiton.py) 
* Missspleing everyhitng
* Not getting hired <- big one
### Errors:
* ensure the py file in the dockerfile is correct(application.py not app.py)
* out of memory: docker system prune -a --volumes
* ensure the sklearn that saved the model is the same sklearn version that opens the model
* 

## AWS deployment with Elastic beanstalk(only works for python 3.8)
* Create an environment in elastic beanstalk
  * Create a service role if you dont have it
  * Create an ec2 role if you dont have it 
* Create a codepipeline and connect it with github and elastic beanstalk. 

## azure(USE THE CORRECT PYTHTON VERISON)(the yml file for workflow is in azure-web branch)
* Create a web app using azure and connect to github

## AWS Deplyoment production(idk more complicated guess) + Docker!
* Create and build docker image and workflow
  * Workflow file can be found in github actions, adjust the aws yaml file(we didnt use ecs)
* Create IAM user with EC2containerREgistryFullcess and EC2FullAccess
  * download the csv for retrieve access key
* Create ECR(private)
  * save the url
* Create/launch ec2 instance
  * Ubuntu
  * instance type: t2.medium
  * Create Key pair(RSA)
  * allow HTTP and https from traffic
* Connect to ec2 after it finishes
  * Also, in security, edit security group and add a new inbound rule, custom TCP port: 5000(what ever you set your port in application.py). source: 0.0.0.0/0
  * Run(maybe try to learn what each command does):
```
sudo apt-get update -y
sudo apt-get upgrade
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```
* Create new self hosted runner(idk the diff between this one(acccess it through settings rather than actions) and the one on actions)
 * Download(paste the code listed in the runner page)
 * Name of runner: self-hosted
 * No name for runner group, no need for additonal labels and no name for work folder.
* Secrets and variables/actions
 * AWS_ACCESS_KEY_ID: From the csv file
 * AWS_SECRET_ACCESS_KEY: csv file
 * AWS_REGION: us-west-1(you can just manually enter in the aws.yaml file)
 * AWS_ECR_LOGIN_URI: you should have saved it
 * ECR_REPOSITORY_NAME: repo name i think
 

 

