# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

## Introduction

The infrastructure as code gives us a huge advantage in defining, deploying, updating and destroying our infrastructure. So to set up an image which contains our application for repeatable deployments, we will use packer to create the virtual machine images(in JSON format).

Terraform also expands on this by not only deploying virtual machines but also storage, networking and security entities across multiple infrastructures, clouds and vendors.

Based on these, this project will use a Packer template and a Terraform template to deploy a customizable, scalable web server in Azure.

## Getting Started

1. Clone this repository
2. Create your infrastructure as code
3. Create your tagging-policy in Azure
4. Create your resource group in Azure

## Dependencies

1. Create an [Azure Account](https://portal.azure.com) 
2. Install the [Azure command line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. Install [Packer](https://www.packer.io/downloads)
4. Install [Terraform](https://www.terraform.io/downloads.html)

## Instructions

### Configure azure policy
#### Create the tagging policy:
``az policy definition create --name tagging-policy --rules tagging-policy.json``
#### Apply the policy afterwards
``az policy assignment create --policy tagging-policy --name tagging-policy
``

#### Set up environment variables
In your terminal, export these environment variables:

``export ARM_CLIENT_ID=my_client_id``

``export ARM_CLIENT_SECRET=my_secret``

``export ARM_SUBSCRIPTION_ID=my_subscription_id``

#### Deploy packer image
In your terminal, create a build from packer json file
``packer build server.json``

#### Use terraform to provision build
In your terminal, run these following commands 

``terraform init``

<br>
To customize your deployment, you can edit these following fields in vars.tf file:

prefix - The prefix used for all resources

environment - The environment used for all resources

location - The Azure Region in which all resources

username - The admin username

password - The admin password 

server_names - Names of servers

packerImageId - Pointer to packer image

vm_count - Total number of virtual machines

<br>

Provision with terraform
``terraform apply``

Once you are finished, destroy the resource
``terraform destroy``

