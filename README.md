                              TASK 4: Infrastructure as Code (IaC) with Terraform


________________________________________
STEP 1: Launch EC2 Instance
•	AMI: Amazon Linux Kernel 5.10
•	Instance Type: t2.micro
•	EBS Volume: 8GB
________________________________________
STEP 2: Install Docker
yum install docker -y
systemctl start docker
chmod 777 /var/run/docker.sock
________________________________________
STEP 3: Install Terraform
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
________________________________________
STEP 4: Create main.tf

terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.23.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx_container" {
  name  = "Cont1"
  image = docker_image.nginx.name
  ports {
    internal = 80
    external = 8080
  }
}

 Steps Performed:
1. Initialized Terraform with Docker provider.
2. Pulled nginx:latest image.
3. Created a Docker container mapping port 8080 → 80.
4. Verified using `docker ps`.
5. Destroyed with `terraform destroy`.
________________________________________
Step5: Terraform Commands

terraform init
 # Initializes Terraform and downloads Docker provider
 
terraform plan
 # Shows what Terraform will do

terraform apply -auto-approve
 # Provisions the nginx container

docker ps
  # Confirms container is running

terraform destroy -auto-approve
 # Destroys the created container

Terraform state list
 # This lists all resources currently tracked in the Terraform state.
________________________________________
RESULT

 ![image](https://github.com/user-attachments/assets/8475e3b4-960f-4938-bc13-61abb7a8a4e5)

