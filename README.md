# Azure DevOps with AKS and ACR

In this project, we are deploying a javascript application in AKS containers using Azure pipeline. The pipeline is used to build the docker image, store it in ACR, and deploy it to AKS.

![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/0f4c2f43-3405-4527-8e27-38f154a0c497)




## Integrating Azure DevOps with Azure

- We will first need to create a service connection between Azure DevOps and Azure.
- Create a service principal ID by going to AAD in the Azure portal and  navigating to  app registration.
- Provide this service principal ID contributor access at the Subscription level:
![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/526bb9fb-d67b-44b8-a274-f8b63dc213d8)


-  Go to Azure DevOps and configure the service connection:
![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/a9ead308-2e51-4659-9a64-8db0f7c5cb8a)

- Service connection is created!!
![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/d57af47f-ca1f-469e-9092-42329fad3252)



## Creating the resources in Azure using Terraform
- Create the terraform configuration file to create resource group, ACR, and AKS. ALso create `terraform.tfvars`, `variables.tf` for managing and organizing variables.
- Download the terraform file from the repo and run it VS code.
- After initializing and planning, run terraform `apply --auto-approve` to finally create the resources.
![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/ce6a3348-391d-4300-833e-c0b40b10de6c)



## Creating the Azure Pipeline 
- Import the Github repo to Azure DevOps.
 ![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/1faacb42-366c-4817-8881-415c053991ea)


- Create a pipeline using `azure-pipelines.yml`. In this pipeline, two tasks are added. One for building the docker and storing the image and the other for performing `kubectl apply` on the image.
![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/82862438-c482-40c8-90a4-1ddddf7aeeb7)
- This pipeline will be triggered as soon as a commit is merged on the main branch.
- The new image created will get replaced with the old one and will deployed into the container managed in AKS.

## Verify application using ip address
- Inside the Kubernetes logs, we'll find the ingress IP address that can be used to access the application.
  ![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/26ecc8b4-26a7-4e37-965f-dc01cfaffbae)
  ![image](https://github.com/bishal-kashyap/azure-pipeline-deploy-to-ACR-and-AKS-using-terraform/assets/142091530/54c7bcf5-2ac2-496f-a743-768fc2d8a2a9)


Hurray!! Our application is up and running!

Now destroy the resources created using `terraform destroy`.









