On the forty first day, I learned the following things about Terraform.

## Terraform Refresh

- First of all remove the second repository data in the *teraform.tf* file.

- Apply the changes by writing `terraform apply --auto-approve`. It will remove the second repository from the GitHub.

- Open the first repository on GitHub and make some changes in it like change the description of it.

- If you open the *terraform.tfstate* file, you will see that the state of the GitHub repo and the state of *terraform.tfstate* are different.

- To make the state the same, write `terraform refresh` command and then to check the status of *terraform.tfstate* file. It will make both the states equal. 

- Write `terraform show` command to show the output of resources in the terminal.

- Although both the states are same but the problem is that if you open `terraform.tf` file, the original text is still present. It means that if you apply the terraform, it will remove the newly created changes.

- In this way, if somebody made changes in your repository but you want the original text to be present then you can write the `terraform plan` to show you the changes. You will see that the new changes will be replaced with the original text.

- After seeing the changes, type `terraform apply` command. Now the changes will be reversed and back to the original text.

- If you open the *terraform.tf* file and delete the description and then type `terraform plan` command. It will show you the text that will be removed from the GitHub repository.

- Type `terraform apply` command and after applying, if you open the github repository, the description will be removed.

## Terraform Output

- Open the *terraform.tf* file and write the following data into it.

      output "terraform-first-repo-url" {
              value = github_repository.terraform-first-repo.html_url
      }

- You can the find the attributes [here](https://registry.terraform.io/providers/integrations/github/latest/docs/resources/repository).

- Once the attribute is added, write the `terraform validate` to first validate it, then write `terraform plan` command to see which things will be added.

- After that, write `terraform apply --auto-approve` command to apply it. Once it is applied, write `terraform output`. It will give you the output.

## Terraform console

- Open the *variable.tf* file and write the following variables in it.

      variable "username" {
              default="bilal"
      }

      variable "age" {
              default = 23
      }

      variable "city" {
              default = "quetta"
      }

- After saving the file, close it and write `terraform console` command in the terminal.

- If you type, *var.city*, it will give you the city. If you type *var.username*, it will give you the username.

- If you type `github_repository.terraform-first-repo.html_url`, it will give you the output link.

- It will read the data from the current working directory that you have.

## Terraform file indentation

- Open the terraform files and add spaces in the file.

- After adding spaces, if you go to the terminal and write `terraform fmt`, all the data will be formatted correctly.

## **Explaining it in a video**

Here you can get an explanation in a video. [41/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=C4wProJIy40&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=39)