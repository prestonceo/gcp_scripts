# gcp_scripts
Simplified GCP scripts for getting started with google cloud platform, Please keep in mind some of these scripts will cause you to be billed, any use of these scripts on the cli should be deleted once you've configured them for testing purposing or editing the resources for deployment. 


# two virtual machine instances in different zones within the same region

```
# Create a network
gcloud compute networks create my-network --subnet-mode custom

# Create the subnet in one of the zones
gcloud compute networks subnets create my-subnet-a \
  --network my-network \
  --range 10.0.1.0/24 \
  --region us-central1 \
  --secondary-range my-network-internal=10.0.2.0/24 \
  --enable-private-ip-google-access

# Create the subnet in another zone
gcloud compute networks subnets create my-subnet-b \
  --network my-network \
  --range 10.0.3.0/24 \
  --region us-central1 \
  --secondary-range my-network-internal=10.0.4.0/24 \
  --enable-private-ip-google-access

# Create the first instance in one zone
gcloud compute instances create my-instance-1 \
  --zone us-central1-a \
  --network my-network \
  --subnet my-subnet-a

# Create the second instance in another zone
gcloud compute instances create my-instance-2 \
  --zone us-central1-b \
  --network my-network \
  --subnet my-subnet-b
  
 ```
 
 # create an instance with custom specifications
 
 ```
 gcloud compute instances create example-instance \
  --zone us-central1-a \
  --image-family ubuntu-2004-lts \
  --image-project ubuntu-os-cloud \
  --boot-disk-size 50GB \
  --boot-disk-type pd-standard \
  --machine-type n1-standard-1 \
  --create-disk size=50GB,type=pd-standard
```

# create a viewer role for gke and a project creator role
```
# Create the viewer role for GKE
gcloud iam roles create viewer-gke \
  --project [PROJECT_ID] \
  --title "Viewer Role for GKE" \
  --permissions container.clusters.get,container.clusters.list

# Create the project creator role

gcloud iam roles create project-creator \
  --project [PROJECT_ID] \
  --title "Project Creator Role" \
  --permissions resourcemanager.projects.create,resourcemanager.projects.get,resourcemanager.projects.update
  ```



