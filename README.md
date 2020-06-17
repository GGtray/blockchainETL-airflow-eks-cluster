# blockchainETL-airflow-eks-cluster
Building an airflow on Amazon Elastic Kubernetes Service
## What is this about?
Code in this repository along with this Introduction is able to:
1. define and deploy a customized k8s cluster on AWS EKS(Elastic Kubernetes Service)
2. run airflow dags auto-synchronized with a customized github repository URL (in this case, this address point to https://github.com/GGtray/airflow-dags.git)
## How to use it? (on MacOS)
### Before using it, you will need
- An AWS account (with enough money in it, eks costs, add IAM role premisson via configuring policy)
- AWS CLI
- kubectl
- wget
### Spining up K8s and connect it to your local computer (waiting for optimizing with terragrunt)
- Step 1: Configure awscli for Authentication
```
$ aws configure
AWS Access Key ID [None]: YOUR_AWS_ACCESS_KEY_ID
AWS Secret Access Key [None]: YOUR_AWS_SECRET_ACCESS_KEY
Default region name [None]: YOUR_AWS_REGION
Default output format [None]: json
```
this step makes you login your aws account on your computer, thus charge you after your cluster spinned up.
- Step 2: Provision the EKS cluster
```
$ terraform init
$ terraform apply
```
wait with patience, it is pretty normal to run for 30min.
- Step 3: Configure kubectl
```
$ aws eks --region us-east-2 update-kubeconfig --name [name in the output]
$ terraform apply
```
this step will asure your kubectl is connected to the cluster, run
```
$ kubectl cluster-info
```
to check this connection out!
### (Option) check cluster through DashBoard

### Run airflow
- Step 1: configure vales.yml
```
$ cd charts/stable/airflow
```
change as such: 
```
