On the fortith day, I learned the following things about Terraform.

## Terraform .tfstate file and destroy Command

- After the creating the *terraform.tf* file and creating a repository on GitHub, two more files will created after that. Those files are *terraform.tfstate* and *terraform.tfstate.backup*.

- Open the *terraform.tfstate* file and it will show you all the resources that you have created in *terraform.tf* file.

- If you want to create another repository, you can add it in the *terraform.tf* file.

- After adding the second repository code in the file, type `terraform plan` command. It will show the new repository resources to be added.

- Write `terraform apply --auto-approve` command. Auto approve won't ask you *YES* or *NO* option everytime and it will make the second repository without making changes in the first one.

- Open the *terraform.tfstate* file and it will show you the first repository resources and the second repository resources that you have created.

- Open the *terraform.tfstate.backup* and it will show you the backup of the earlier resources that you have created.

- **Tip:** Don't try to manually change the .tfstate file.

## Terraform Destroy

- If you want to destroy the resources, you can do it by writing, `terraform destroy`. It will destroy all the resources and the repositories that you have created.

- If you want to destroy a specific resource, you can do this by simply writing `terraform destroy --target github_repository.terraform-second-repo`.

- If you write `terraform plan`, it will show you the resources of the second repository that needs to be added.

## Terraform Validate Command

- Before showing you how to validate the terraform, let's make some changes in the terraform files.

- Open the *terraform.tf* file, copy the provider and paste into the *provider.tf* file.

- Remove the token from the *provider.tf* file and write the following data into it.

      provider "github" {
          token = "${var.token}"
      }

- Make a *variable.tf* file and write the following data into it.

      variable token {}

- Make a *terraform.tfvars* file and write the token inside it.

      token="<token>"

- After making these changes, type `terraform validate` command and it will give you the message **Success! The configuration is valid.**

- Now you can destroy and apply the configuration file.

## **Explaining it in a video**

Here you can get an explanation in a video. [40/60 Day of DevOps Challenge]()