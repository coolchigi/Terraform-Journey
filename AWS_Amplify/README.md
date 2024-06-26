# AWS Amplify Deployment with Terraform

This repository contains the necessary Terraform code to automate the deployment of an AWS Amplify application.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Resources Deployed](#resources-deployed)
- [Getting Started](#getting-started)
- [Cleanup](#cleanup)

## Introduction

The project aims to simplify the process of deploying an AWS Amplify application by providing a pre-configured Terraform infrastructure-as-code solution. We will be building a serverless fullstack Amplify App. With this code, you can easily provision the required AWS resources and deploy your Amplify application with just a few simple steps.

By using Terraform, you can define your infrastructure in code, version control it, and easily replicate it across different environments. This allows for consistent and reproducible deployments, reducing the risk of manual errors and ensuring a reliable and scalable infrastructure for your Amplify application.

To get started, make sure you have the prerequisites mentioned below and follow the steps outlined in the "Getting Started" section.

Happy deploying!

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account
- Terraform installed on your local machine
- AWS CLI configured with your AWS credentials

## Architecture

Here's the architecture of what we are going to be build:

![Solution Architecture](https://utfs.io/f/98d015e3-df7c-4784-9ebe-870d2214df5b-kijm2f.png)

## Tech Stack

- [AWS Amplify](https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html)
- [Amazon S3](https://docs.aws.amazon.com/s3/index.html)
- [AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html/)
- [AWS DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [AWS AppSync](https://docs.aws.amazon.com/appsync/latest/devguide/welcome.html)

## Resources Deployed

Below are the list of resources we are going to deploy with terraform.

AWS Amplify

- Web Application

  - `<app_name>` - `app_name` is variable you define in the Terraform Config.

AWS AppSync

- GraphQL API

  - `<app_name>-graphql-api`

AWS CodeCommit

- Repository (Optional)

  - `<app_name>-codecommit_repo`

Amazon Cognito

- user_pool
- identity_pool
- user_pool_client
- cognito_groups (dynamic)
- cognito_users (dynamic)

Amazon DynamoDB

- Table

  - `<app_name>-output-<uuid>`

Amazon EventBridge

- Event Bus

  - `<app_name>-event_bus`

- Event Rule

  - default_event_bus_to_sample_event_bus
  - `<app_name>-landing_bucket_object_created`

AWS IAM

- Roles

  - `<app_name>_amplify_codecommit`
  - `<app_name>_appsync_dynamodb_restricted_access`
  - `<app_name>_cognito_admin_group_restricted_access`
  - `<app_name>_cognito_authrole_restricted_access`
  - `<app_name>_cognito_standard_group_restricted_access`
  - `<app_name>_cognito_unauthrole_restricted_access`
  - `<app_name>_eventbridge_invoke_custom_sample_event_bus_restricted_access`
  - `<app_name>_eventbridge_invoke_sfn_state_machine_restricted_access`
  - `<app_name>_step_functions_master_restricted_access`

- Policies

  - `<app_name>_s3_restricted_access_policy`
  - `<app_name>_dynamodb_restricted_access_policy`
  - `<app_name>_dynamodb_restricted_access_read_only_policy`
  - `<app_name>_ssm_restricted_access_policy`
  - `<app_name>_eventbridge_invoke_custom_sample_event_bus_restricted_access_policy`
  - `<app_name>_eventbridge_invoke_sfn_state_machine_restricted_access_policy`
  - `<app_name>_gitlab_mirroring_policy` (conditional)

  - `<app_name>_gitlab_mirroring` (conditional)

# Amazon S3

- Buckets
  - `<app_name>_landing_bucket`

AWS Systems Manager Parameter Store

- SSM Parameter
  - ssm_github_access_token (conditional)
  - `<app_name>-landing_bucket_name`
  - `<app_name>-dynamodb_output_table_name`

Step Functions

- State Machine
  - `<app_name>-state-machine`

## Getting Started

To get started with the deployment, follow these steps:

1. Clone this repository to your local machine.
2. Navigate to the project directory.
3. Initialize the Terraform configuration by running the following command:
   ```
   terraform init
   ```
4. Modify the `variables.tf` file to customize the deployment settings.
5. Review the `main.tf` file to understand the resources that will be provisioned.
6. Run the following command to preview the changes that will be applied:
   ```
   terraform plan
   ```
7. If the plan looks good, apply the changes by running:
   ```
   terraform apply
   ```
8. Once the deployment is complete, you will see the output URL of your Amplify application.

## Cleanup

To clean up the resources created by this deployment, follow these steps:

1. Open a terminal or command prompt.
2. Navigate to the project directory.
3. Run the following command to destroy the provisioned resources:

   ```bash
   terraform destroy
   ```

   This command will prompt for confirmation before destroying the resources.

4. Confirm the destruction by typing `yes` and pressing Enter.
