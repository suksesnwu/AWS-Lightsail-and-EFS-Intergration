# AWS Lightsail and EFS Integration

This repository is a continuation of the [AWS Lightsail WordPress](https://github.com/suksesnwu/AWS-Lightsail-WordPress/blob/main/README.md) project. It provides a step-by-step guide to connect AWS Lightsail instances to an Amazon Elastic File System (EFS), allowing instances to share a common file system across Availability Zones (AZs).

## Project Overview

Building on the initial setup from the AWS Lightsail WordPress project, this guide focuses on:
- Setting up a VPC peering connection between Lightsail and the default VPC.
- Creating an EFS file system.
- Configuring EFS mount targets in each AZ.
- Setting up security group rules for NFS access.
- Mounting the EFS file system on Lightsail instances.
- Verifying file access across multiple instances.

## Prerequisites

- AWS CLI installed and configured.
- jq tool installed for parsing JSON output.
- AWS Lightsail and EFS services enabled.

## Steps

### Step 1: Peer Lightsail VPC with Default VPC
1. Peer the Lightsail VPC with the default VPC to enable communication.
    ```
    aws lightsail peer-vpc
    ```

### Step 2: Create an EFS File System
1. Create a new EFS file system.
    ```
    aws efs create-file-system
    ```

### Step 3: Obtain Subnet Information
1. Retrieve subnet information for the default VPC.
    ```
    aws ec2 describe-subnets --filters Name=vpc-id,Values=<Default VPC ID> Name=default-for-az,Values=true
    ```

### Step 4: Create EFS Mount Targets
1. Create an EFS mount target for each subnet.
    ```
    aws efs create-mount-target --file-system-id <EFS File System ID> --subnet-id <Subnet ID>
    ```

### Step 5: Configure Security Group Rules
1. Allow NFS traffic from the Lightsail VPC.
    ```
    aws ec2 authorize-security-group-ingress --group-id <Default Security Group ID> --protocol tcp --port 2049 --cidr <Lightsail VPC CIDR>
    ```

### Step 6: Connect Lightsail Instances to EFS
1. SSH into the Lightsail instance.
2. Install NFS client and mount the EFS file system.
    ```
    sudo apt install nfs-common
    sudo mkdir /mnt/efs
    sudo mount -t nfs -o nfsvers=4.1 <EFS Mount Point IP Address>:/ /mnt/efs
    ```
3. Verify file access by creating and reading a file on the shared file system.
    ```
    sudo touch /mnt/efs/sharedfile.txt
    cat /mnt/efs/sharedfile.txt
    ```

## Verification
- Ensure all Lightsail instances can read and write to the shared EFS file system.
- Verify security group settings to maintain secure access.

## Conclusion

This guide helps establish a shared storage solution for AWS Lightsail instances using EFS, enhancing data sharing and management across instances.
