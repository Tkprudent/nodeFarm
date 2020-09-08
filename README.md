In this project I will apply the skills and knowledge which was acquired throughout the Cloud DevOps Nanodegree program. These include:

As a capstone project, I will be deploying a web application titled **NODE FARM** which is just a simple application that helps to give a detailed information of my favorite natural fruits. The project was gotten from an udemy course I took and can be found at [Node.js, Express, MongoDB & More: The Complete Bootcamp 2020](https://www.udemy.com/course/nodejs-express-mongodb-bootcamp/). CI/CD pipeline for micro services applications with rolling deployment will be developed. 

Several Continuous Integration steps will be developed which include typographical checking (aka “linting”). To make my project stand out, you may also choose to implement other checks such as security scanning and performance testing.

Once I completed the Continuous Integration I set up Continuous Deployment, which will include:

* Pushing the built Docker container(s) to the Docker repository (using AWS ECR, I create my own custom Registry within my cluster, or another 3rd party Docker repository) ; and
* Deploying these Docker container(s) to a small Kubernetes cluster. 
* For my Kubernetes cluster I use AWS Kubernetes as a Service, or build your own Kubernetes cluster. 
* To deploy your Kubernetes cluster, use either Ansible or Cloudformation. Preferably, run these from within Jenkins as an independent pipeline.