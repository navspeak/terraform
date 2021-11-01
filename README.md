# terraform.tfvars
* Add this to .gitignore 
* You may generally put values specific to your environment in this file like AWS_ACCESS_KEY and AWS_SECRET_KEY here
```
AWS_ACCESS_KEY = "AKIAXXX"
AWS_SECRET_KEY = "XXXX"
MY_LAPTOP_IP = "172.X.X.X/32"
```
# Multiple Providers:

|<pre>Default Provider                         </pre>|<pre>Non Default Provider                        </pre>| 
|--------------------------                     |--------------------------------|
| provider "aws" {                              |  provider "aws" {              | 
| region ="us-east-1"                           |    region = "us-west-2"        |  
| }                                             |    alias = "london"            |
|                                               |     }                          |

| <pre>Resource from Default Provider           </pre>|<pre>Resource from Non-default                </pre>| 
|--------------------                           |-------------------------------- |
| resource "aws_vpc" "vpc_from_default" {       | resource "aws_vpc" "vpc_from_default_non_default" { |
|  cidr_block = "10.0.0.0/16"                   | cidr_block = "10.1.0.0/16" |
|} | provider = "aws.london"                    |
|                                               |}|

* When there are multiple providers, all after first must have an alias
* Every resource has a ```provider``` property that you can set. 
* In above example, we did not have ```provider``` property for ```ireland_vpc```. However, we could have exlicitly told Terraform to use the default provider by adding ```provider = "aws"```; albeit unecessarily!


# Terraform Usage
1. Interpolation

