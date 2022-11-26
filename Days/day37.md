On the thirty seventh day, I learned the following things about Terraform.

## Set the default value

- If you want to set the value to be default and not want to get asked every time then you can do it by making changes in the given code.

**Change this**

    variable username {}

**To this**

    variable username {
      default = "World"
    }

- Now the username is set to *World*. If you type `terraform plan`, it won't ask you to enter the value.

- Instead it will show you the message. If you want to give it a value, you can do this through the command `terraform plan -var "username=Bilal Khan"`.

## Multiple variables

- You can give multiple variables also if you want to. The process is really simple and you can print them at the same time.

- In the *variable.tf* file, under the username variable, type another variable like this:

      variable age {
        default = "25"
      }

- Make changes in the *hello-variable.tf* file like this:

      output printname {
            value = "Hello, ${var.username}. Your age is ${var.age}"
      }

- Now if you type `terraform plan`, it won't ask you for your username and age. It will give you the values.

- If you removed the default value of age, then it will ask you for the entry when you type `terraform plan`.

- You can then give the age by writing this command in the terminal `terraform plan -var "age=24"`.

- If you want to give both the username and age on the terminal without being asked, you can do this by writing `terraform plan -var "username=Bilal Khan" -var "age=24"`.

## Variable Types

- In the block of data, you can set the type also. If you want to check the list of multiple types, you can visit this [website](https://developer.hashicorp.com/terraform/language/expressions/types).

- Add a type in a variable like this:

      variable age {
        type = number
        default = "25"
      }

- If you type `terraform plan -var "age=fds"`, it will give you an error by pointing the invalid type.

## List Variables

- Create a directory by the name of **list-variable** and get into by writing `cd list-variable`.

- After that, create a file by the name of *first.tf* and write the following data into it.

      variable users {
          type = list
      }

      output printfirst {
          value = "first user is ${var.users[0]}"
      }

- In the above code, first the values will be taken in list and then the first value is going to be printed.

- Save the data in a file and run `terraform plan`. It will ask you for the values to enter. You can enter the values in a list like this: `["bilal", "ali", "khan"]`.

- You can also give a list of values in the terminal by typing `terraform plan -var 'users=["bilal", "ali", "khan"]'`

- You can set the default values by making the changes in a file like this:

      variable users {
          type = list
          default = ["bilal", "ali", "khan"]
      }

- Now just the `terraform plan` command and the result will be shown to you without asking for entry.

## Functions in Terraform

- The Terraform language includes a number of built-in functions that you can call from within expressions to transform and combine values.

- Go to this [website](https://developer.hashicorp.com/terraform/language/functions) and take a look at all the functions.

### Join function

- Let's take a look at an example by using some functions.

      output printfirst {
          value = "first user is ${join(", ", var.users)}"
      }

- If you save it and run the `terraform plan` command, you will get the following result.

      printfirst = "first user is bilal, ali, khan"

### Upper function

- Write the data in an upper using the `upper` function.

- Make another output by the name of *UpperFunc* and convert the first user into upper case.

      output UpperFunc {
        value = "${upper(var.users[0])}"
      }

- Write `terraform plan` in the terminal and you will get the upper-case value.

### Lower function

- Make another output by the name of *LowerFunc* and convert the first user into lower case.

      output LowerFunc {
        value = "${lower(var.users[0])}"
      }

- Write `terraform plan` in the terminal and you will get the lower-case value.

### Title function

- Make another output by the name of *TitleFunc* and convert the first alphabet of a word into an upper case.

      output TitleFunc {
        value = "${title(var.users[0])}"
      }

- Write `terraform plan` in the terminal and you will get the first alphabet in an upper-case.

## **Explaining it in a video**

Here you can get an explanation in a video. [37/60 Day of DevOps Challenge]()