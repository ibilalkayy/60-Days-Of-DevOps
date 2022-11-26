On the thirty eighth day, I learned the following things about Terraform.

## Map Variable

- Create a directory by the name of *map-variable* and get inside it by typing `cd map-variable`.

- After creating a directory, make a file in it by the name of *variable.tf* and write the following data inside it.

      variable "userage" {
        type = map
        default = {
          bilal = 25
          ali = 20
        }
      }

      output "userage" {
        value = "my name is bilal and my age is ${lookup(var.userage, "bilal")}"
      }

- First a variable is declared by the name of *userage* and inside this variable, there is a type map and values are set to default. The default ages are of bilal and ali.

- After declaring the variables, let's print the output to show the age of a particular key using the `lookup` function.

## Use map variable Dynamically

- Instead of changing the key like bilal or ali every time in a file, how to dynamically use the map variables.

- Create another variable like this and write the following data into it.

      variable "username" {
        type = string
      }

- After the variable is created, make some changes in the output like this:

      output "userage" {
          value = "my name is ${var.username} and my age is ${lookup(var.userage, "${var.username}")}"
      }

- Now if you write `terraform plan`, it will ask you for a key to enter. Once you enter a key, it will show you the age according to that key.

- You can also write a key in the terminal like `terraform plan -var "username=bilal"` and it will show you the value according to it.

## TFVARS files in Terraform

- You may face a problem that every time you want a person's data, the command line will ask you everytime to enter the key so that it brings you the value.

- You can automate this process by making a file and write the age and username there.

- To make this happen, first make a directory by the name of **tf-var** and get into it by using the `cd` command.

- After that, make a file by the name of *first.tf* and write the following data into it.

      variable "username" {
        type = string
      }

      variable "age" {
        type = number
      }

      output printname {
        value = "Hello, ${var.username}, your age is ${var.age}"
      }

- Once the data is saved in a file, make another file by the name of *terraform.tfvars*. Inside this file, write the following data so that it never ask you again.

      age=25
      username="Bilal Khan"

- After saving the data in both of the files, if you write `terraform plan`, it will give you the result without asking you the username and age.

## TFVARS File With Different Name.

- If you want to change the name of *tfvars* file into something else according to your need, you can do this.

- First of all copy the data of **tf-var** directory into a new directory using the command `cp -rvf tf-var tf-var-custom`. Get into the newly created directory by writing `cd tf-var-custom`.

- After that, make a *tfvar* file by any name that you want like development, production, etc and write the following data into it.

      age=20
      username="Ali Ahmed"

- After that, write `terraform plan -var-file=filename.tfvars`, it will show you the result of that particular file.

- You can find more about this command and other commands by writing `terraform plan --help | less`.

## Read Environment Variable in Terraform Configurations

- If you want to declare the variable in your terminal and then use it in the terraform then you can also do it.

- Create a directory by the name of *env-variable* and get inside it by typing `cd env-variable`.

- After creating a directory, make a file in it by the name of *first.tf* and write the following data.

      variable "username" {
              type = string
      }

      output printname {
              value = "Hello, ${var.username}"
      }
      
- Once the file is saved, write `terraform plan` to get the result. You will see that it will ask you for the value to enter and then it will give you the result.

- To avoid this, you have to first declare an environment variable and then if you run the `terraform plan` command again, it won't ask you for the value to enter. Instead it will fetch the value from the environment variable.

- First of all, type `echo $username`. It will show you nothing because an environment variable is not declared yet.

- To declare an environment variable, type `export username=Umar` and then if you type `echo $username` again, it will show you result.

- After that, type `terraform plan` command. You will see that again it is asking you for the value to enter.

- The problem is not in the environment variable. The problem was that the terraform wants the specific name environment variable to be declared.

- You need to declare an environment variable by the name of `TF_VAR_username` and then it will accept it.

- First export it by writing `export TF_VAR_username=Umar` and then if you write `terraform plan` it won't ask you for the value to enter.

## **Explaining it in a video**

Here you can get an explanation in a video. [38/60 Day of DevOps Challenge]()