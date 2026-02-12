# Terraform – count, for_each and Version Constraints Example

This project demonstrates the difference between `count` and `for_each` in Terraform, as well as how to use version constraints to control Terraform and provider versions.

The example creates multiple local sensitive files using a list of users. It highlights how `for_each` provides more stable resource management compared to `count`.

## Project Structure

* `main.tf` – Defines the resource using `for_each`
* `variables.tf` – Defines input variables

## Concepts Demonstrated

### for_each

The project uses:

for_each = toset(var.users)

This converts a list of users into a set.
Using a set removes duplicates and ensures each resource is uniquely identified by its value.

Unlike `count`, which tracks resources by index (0, 1, 2...), `for_each` tracks them by key. This makes infrastructure changes safer when modifying the list.

### count (conceptual comparison)

If `count` were used instead, Terraform would identify resources by index.
If the order of the list changes, Terraform might destroy and recreate resources unnecessarily.

### Version Constraints

Version constraints help control which Terraform and provider versions can be used.
This ensures consistency across environments and avoids unexpected behavior.

Example:

terraform {
required_version = ">= 1.5.0"

required_providers {
local = {
source  = "hashicorp/local"
version = "~> 2.4"
}
}
}

## Requirements

* Terraform installed (recommended version >= 1.5.0)
* No cloud provider required (uses local provider)

You can check your Terraform version with:

terraform version

## How to Run

1. Clone the repository:

git clone <your-repository-url>
cd <repository-folder>

2. Initialize Terraform:

terraform init

3. Review the execution plan:

terraform plan

4. Apply the configuration:

terraform apply

5. To clean up:

terraform destroy

## What This Project Creates

* Multiple local sensitive files based on the `users` variable
* Each file contains predefined content

Example default variable:

variable "users" {
type    = list(string)
default = ["/root/user10", "/root/user11", "/root/user12", "/root/user10"]
}

Note that converting the list to a set removes duplicate entries automatically.

## Learning Purpose

This project was created for learning purposes to better understand:

* The difference between `count` and `for_each`
* How Terraform tracks resources in state
* How version constraints improve environment stability
