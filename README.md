
# Email Controller

## Overview

This controller is responsible for managing Email resources within a Kubernetes cluster. It reconciles the desired state of Email objects with the actual state of the cluster, ensuring that emails are sent according to the specifications provided by the user.

## Creation

Create the project using operator-sdk and generate apis

```
operator-sdk create api --group mail --version v1 --kind Email --resource --controller
operator-sdk create api --group mail --version v1 --kind EmailSenderConfig --resource --controller
```


## Installation

To use this controller, follow these steps:

1. Install Go and set up your Go workspace.
2. Clone the repository containing the controller code.
3. Build the controller binary.
4. Deploy the controller to your Kubernetes cluster.

## How it Works

### Reconciliation Loop

The core functionality of the controller is implemented in the `Reconcile` function. This function is invoked periodically by the Kubernetes controller-runtime framework to ensure that the state of Email objects in the cluster matches the desired state.

### Reconcile Function

The `Reconcile` function performs the following steps:

1. Fetch the Email object specified in the reconciliation request.
2. Check if the email has already been sent. If it has, the reconciliation process is skipped.
3. Fetch the EmailSenderConfig referenced by the Email object.
4. Use the MailerSend API to send the email using the configuration provided by the EmailSenderConfig.
5. Update the status of the Email object based on the result of the email sending operation.


## Dependencies

This controller depends on the following libraries:

- Kubernetes controller-runtime
- MailerSend Go SDK

To install and run the controller using Operator SDK, you'll follow a set of steps including setting up your development environment, scaffolding the operator project, implementing the controller logic, building the operator image, and deploying it to your Kubernetes cluster. Here's a guide on how to do it:

## MaierSend config
Create account and generate token to be used in email config https://www.mailersend.com/

## Running The Controller

### Step 1: Set up your development environment

Ensure you have a working Go development environment. 

### Step 2: Install CRDs


```bash
make install
```

### Step 3: Deploy the Controller


```bash
make run
```

### Step 4: Create Sample Resources
Update the resources in `config/samples` and apply them

```
kubectl apply -f config/samples/email_v1_emailsenderconfig.yaml
```

```
 kubectl apply -f config/samples/email_v1_email.yaml
```
