# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning Infrastructure as Code (IaC).

To install Terraform, visit https://www.terraform.io/downloads.html and download the appropriate zipped file compatible with your system.

With Terraform installed, you can start creating some infrastructure.

Most users prefer to create a new directory on their local machine and create Terraform configuration code inside it.

To do this, run the following command in a shell window:

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Now paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Next, initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

Check for any errors. If it ran successfully, provision the resource with the `apply` command.
```shell
$ terraform apply
```

The command will take a few minutes to finish and will display a message indicating that the resource was created.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it created earlier.
