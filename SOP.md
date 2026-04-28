# Roboshop Project Manual Implementation SOP on AWS EC2

## Purpose
This document standardizes the manual implementation of the Roboshop project on AWS EC2 instances using the required lab environment and provisioning conventions.

## Standard VM Provisioning Rules
1. Always use the lab AMI to provision `t3.micro` **Spot** VMs for Roboshop application components.
2. Do not attach a key pair while provisioning these component VMs.
3. Use the following lab image and access details:
   - **AMI**: `DevOps-LabImage-RHEL9`
   - **Region**: `N. Virginia`
   - **Default Credentials**: `ec2-user / DevOps321`
4. Every VM must be attached to the `B60-Allow-All` security group.
5. The `B60-Allow-All` security group must allow all ports from the internet.

## Hostname Standard
Each VM must use the application component name as its hostname.

Example:
```bash
set-hostname componentName
```

## Connectivity Validation Between Components
If communication between components fails, validate connectivity from the dependent application server to the target service.

Example: if `catalogue` needs to connect to MongoDB, log in to the `catalogue` server and run:

```bash
timeout 5 telnet mongoDBIP 27017
```

This checks whether the `catalogue` component can reach MongoDB on port `27017`.

## MongoDB and Redis Configuration
For both MongoDB and Redis, ensure the respective configuration file is updated with `0.0.0.0` where required so the service listens for external connections.

If this is not updated, the database or cache service may reject connections from other components.

## Redis Requirement
For the Redis server, ensure **Protected Mode** is turned off.

If Protected Mode remains enabled, Redis may allow only authenticated connections using username and password, while the Roboshop application is not designed to use Redis authentication.

## Workstation Requirement
Provision one separate EC2 instance as **On-Demand** capacity, not Spot.

This instance must:
- Use the same lab AMI: `DevOps-LabImage-RHEL9`
- Be named either `WS` or `Workstation`
- Remain available until the end of the training

## Workstation Purpose
The workstation instance is intended for installing tools, validating prerequisites, and testing the basic setup required throughout the training.

It serves as the persistent utility machine for the entire Roboshop implementation process.