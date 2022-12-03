On the thirty sixth day, I learned the following things about Terraform.

## Terraform Configurations in JSON Format

- First create a directory by the name of **hello-world-json**.

- Get into it by writing `cd hello-world-json` and create a file by the name of *first.tf.json* in it.

- Inside that file, write the following data in the JSON format.

      {
              "output": {
                      "hello": {
                              "value": "Hello Bilal, nice meeting you."
                      }
              }
      }

- After writing and saving the data, write a command `terraform plan` and it will show the keys and values as a result that you have written in a file.

- Terraform also works with the JSON format to write the infrastructure.

## Write Multiple Blocks in Single Terraform File

- Create a directory by the name of **hello-world-multi-block**.

- Get into it by writing `cd hello-world-multi-block` and create a file by the name of *first.tf* in it.

- Inside the *first.tf* file, write the following data.

      output "firstoutputblock" {
              value = "this is the first hello world block"
      }

      output "secondoutputblock" {
              value = "this is the second hello world block"
      }

      output "thirdoutputblock" {
              value = "this is the third hello world block"
      }

- After writing and saving the data, write a command `terraform plan` and it will show the keys and values as a result that you have written in a file.

## Write Multiple Terraform files in the Same Directory

- Create a directory by the name of **hello-world-file-destructure**.

- Get into it by writing `cd hello-world-file-destructure` and create a file by the name of *first.tf* in it.

- Inside the *first.tf* file, write the following data.

      output "firstoutputblock" {
              value = "this is the first hello world block"
      }

- Create another file by the name of *second.tf* and write the following data in it.

      output "secondoutputblock" {
              value = "this is the second hello world block"
      }

- Create another file by the name of *third.tf* and write the following data in it.

      output "thirdoutputblock" {
              value = "this is the third hello world block"
      }

- After writing and saving the data, write a command `terraform plan` and it will show the keys and values as a result that you have written in the files.

- The result will be loaded in an alphabetical sequence according to the given output.

## Create a variable in a file

- Create a directory by the name of **hello-variable** and get into by writing `cd hello-variable`.

- After that, create a file by the name of *hello-variable.tf* and write the following data into it.

      variable username {}

      output printname {
            value = var.username
      }

- After writing and saving the data, write a command `terraform plan` and it will ask you for the username and then show the keys and values as a result that you have written in a file.

- If you want to write something more with the user name then write it inside the commas like this:

      variable username {}

      output printname {
            value = "Hello, ${var.username}"
      }

- After writing and saving the data, write a command `terraform plan` and it will ask you for the username and then show the keys and values as a result that you have written in a file.

- Now separate the variables and the outputs in different files by simply creating another file by the name of *variable.tf* inside the **hello-variable** directory.

- Cut the `variable username {}` from the *hello-variable.tf* and paste it in a newly created file *variable.tf*.

- After writing and saving the data, write a command `terraform plan` and it will ask you for the username and then show the keys and values as a result that you have written in a file.

## Enter a variable value in the command

- We have seen that in order to enter the username, you first have to write `terraform plan` and then it will ask you for the value to be printed.

- But you can give a value in the command also by simply writing `terraform plan -var "username=Bilal Khan"` and it will print the data for you without asking to enter the value.

## **Explaining it in a video**

Here you can get an explanation in a video. [36/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=9zsbSwEyLkw&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=34)