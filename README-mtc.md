# Based off of https://cloud.google.com/docs/terraform/resource-management/managing-infrastructure-as-code?hl=en
#
# IaC with Terraform, GCP Cloud Build and GitOps
#

gcloud projects list
gcloud config set project srx-iac-gcp
gcloud services enable cloudbuild.googleapis.com compute.googleapis.com

# Start with gitops terraform/cloudbuild template from github.  In Github, 
# fork the project / repo GoogleCloudPlatform /
# solutions-terraform-cloudbuild-gitops.git to 
# https://github.com/miketclew/srx-iac-tf in github.com web interface.

# Now pull it to my local system for initial configuration/setup.

git clone https://github.com/miketclew/srx-iac-tf/

# Create a GCS Bucket to centralize Terraform state file(s).

PROJECT_ID=$(gcloud config get-value project)
gsutil mb gs://${PROJECT_ID}-tfstate

# Populate template files with our GCP project id.

cd ~/srx-iac-tf
sed -i s/PROJECT_ID/$PROJECT_ID/g environments/*/terraform.tfvars
sed -i s/PROJECT_ID/$PROJECT_ID/g environments/*/backend.tf




