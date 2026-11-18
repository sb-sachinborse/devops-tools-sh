# Automate GCP: Creating VPC, Subnet, Firewall Rules, and Compute Instances Using gcloud cli

#### Why Automate?
Manually creating resources in the GCP Console can be time-consuming and error-prone. By automating with a script, you:

- Reduce human errors.
- Save time and effort.
- Create reusable infrastructure setups.

Prerequisites
Before you begin, ensure you have the following:

- GCP Account: A Google Cloud account with billing enabled.
- Cloud SDK: Install the Google Cloud SDK.

gcloud Authentication: Authenticate using the following command
```
gcloud auth login
```
Project Setup: Set your GCP project:
```
gcloud config set project [PROJECT_ID]
```
Script to Automate Resource Creation:
Here’s a bash script to automate the creation of a VPC, subnets, firewall rules, and compute instances.
Save the creation script as gcp-infra.sh:


```
#!/bin/bash

# Create a VPC called custom-vpc
gcloud compute networks create custom-vpc --subnet-mode=custom
echo "Custom-vpc successfully created!"

# Create a subnet called subnet-a under custom-vpc
gcloud compute networks subnets create subnet-a --network custom-vpc --region us-central1 --range=10.0.0.0/24
echo "Created subnet-a under custom-vpc"

# Create a subnet called subnet-b under custom-network
gcloud compute networks subnets create subnet-b --network custom-vpc --region asia-east1 --range=10.0.1.0/24
echo "Created subnet-a under custom-vpc"

# Create an instance called instance-1a under subnet-a
gcloud compute instances create instance-1a --zone us-central1-a --subnet=subnet-a
echo "created instance-1a under subnet-a"

# Create an instance called instance-1b under subnet-a
gcloud compute instances create instance-1b --zone us-central1-a --subnet=subnet-a --no-address
echo "created instance-1b under subnet-a"

# Create an instance called instance-1c under subnet-a
gcloud compute instances create instance-1c --zone us-central1-a --subnet=subnet-a
echo "created instance-1c under subnet-a"

# Create an instance called instance-2 under subnet-b
gcloud compute instances create instance-2 --zone asia-east1-a --subnet=subnet-b
echo "created instance-2 under subnet-b"

# Create an instance called instance-3 under subnet-b
gcloud compute instances create instance-3 --zone asia-east1-a --subnet=subnet-b --no-address
echo "created instance-3 under subnet-b"

# Create firewall rules to allow SSH, HTTP, and HTTPS
gcloud compute firewall-rules create allow-ssh --network custom-vpc --allow tcp:22 --description "Allow SSH traffic on port 22"
echo "Created firewall rule for port 22"

gcloud compute firewall-rules create allow-http --network custom-vpc --allow tcp:80 --description "Allow HTTP traffic on port 80"
echo "created firewall rule for port 80"

gcloud compute firewall-rules create allow-https --network custom-vpc --allow tcp:443 --description "Allow HTTPS traffic on port 443"
echo "Created firewall rule for port 443"

echo "Succesfully Custom-VPC, Subnet, Virtual Machines, Firewall rules for SSH, HTTP, and HTTPS have been successfully created!"

```

Running the Script:
```
chmod 777 gcp-infra.sh
sh gcp-infra.sh
```



Destroying Resources:
To clean up resources, use the following script:

##### Save the creation script as infra-destroy.sh:
```
#!/bin/bash

# Delete firewall rules
gcloud compute firewall-rules delete allow-ssh --quiet
echo "Deleted firewall rule for SSH (port 22)"

gcloud compute firewall-rules delete allow-http --quiet
echo "Deleted firewall rule for HTTP (port 80)"

gcloud compute firewall-rules delete allow-https --quiet
echo "Deleted firewall rule for HTTPS (port 443)"

# Delete the instances created under subnet-a
gcloud compute instances delete instance-1a --zone us-central1-a --quiet
echo "Deleted instance-1a created under subnet-a"

gcloud compute instances delete instance-1b --zone us-central1-a --quiet
echo "Deleted instance-1b created under subnet-a"

gcloud compute instances delete instance-1c --zone us-central1-a --quiet
echo "Deleted instance-1c created under subnet-a"

# Delete the instances created under subnet-b
gcloud compute instances delete instance-2 --zone asia-east1-a --quiet
echo "Deleted instance-2 created under subnet-b"


gcloud compute instances delete instance-3 --zone asia-east1-a --quiet
echo "Deleted instance-3 created under subnet-a"

# Delete the subnets
gcloud compute networks subnets delete subnet-a --region us-central1 --quiet
echo "Deleted subnet subnet-a"

gcloud compute networks subnets delete subnet-b --region asia-east1 --quiet
echo "Deleted subnet subnet-b"

# Delete the custom VPC network
gcloud compute networks delete custom-vpc --quiet
echo "Deleted VPC custom-vpc"

echo "All resources have been successfully deleted!"

```
Running the Script:
```
chmod 777 infra-destroy.sh
sh infra-destroy.sh
```
Key Benefits of Automation
- Efficiency: Provision resources quickly.
- Reproducibility: Consistent setups across environments.
- Scalability: Easily modify scripts to scale infrastructure.
