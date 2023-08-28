# Azure DevOps with AKS and ACR

In this project, we are deploying a javascript application in AKS containers using Azure pipeline. The pipeline is used to build the docker image, store it in ACR, and deploy it to AKS on trigger.

![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/f51d257c-74d4-43f1-8ef5-58b159d6b3bd)



## Integrating Azure DevOps with Azure

- We will first need to create a service connection between Azure DevOps and Azure.
- Create a service principal ID by going to AAD in the Azure portal and  navigating to  app registration.
-  Provide this service principal ID contributor access at the Subscription level:
![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/4b7bd27a-7a61-4a2b-ae85-2af72c8a394b)

-  Go to Azure DevOps and configure the service connection:
![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/0a2137d3-e4da-4500-bc9c-9e15de1ba4a6)
- Service connection is created!!
 ![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/61c341f8-0caf-4225-ba96-1eedaa99f66a)


## Creating the resources in Azure using Terraform
- Create the terraform configuration file to create resource group, ACR, and AKS. ALso create `terraform.tfvars`, `variables.tf` for managing and organizing variables.
- Download the terraform file from the repo and run it VS code.
- After initializing and planning, run terraform `apply --auto-approve` to finally create the resources.
![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/579cd42c-e98a-4beb-9e28-36f1df1e4a56)

## Creating the Azure Pipeline 
- Clone the Github repo to Azure DevOps.
- ![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/d124d1bc-36ea-4e05-bfac-2a65861592f5)

- Create a pipeline using `azure-pipelines.yml`. In this pipeline, two tasks are added. One for building the docker and storing the image and the other for performing `kubectl apply` on the image.
- ![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/5f83d2c1-28f6-4961-8b30-e6fda403a7a2)
- This pipeline will be triggered as soon as a commit is merged on the main branch.
- The new image will get deployed into the container managed in AKS.

## Verify application using ip address
- Inside the Kubernetes logs, we'll find the ingress IP address which can be used to access the application.
![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/cd424bed-1c98-4aa6-99c9-48a7e7c379e3)
![image](https://github.com/bishal-kashyap/Azure-devops-with-AKS-ACR/assets/142091530/81554cf3-9a71-4fae-99ed-30ddc9cdf82b)

Hurray!! Our application is up and running!









