# Project :  Deploying a High-Availability Web Application Using AWS CloudFormation

Infrastructure-as-code (IAC) that automates the process of creating a secured and HA environment , deploying  a WebApp  (packaged and staged in AWS S3 Storage) into a cluster of NGINX Servers. The script contains all the configurations needed for a repeatable process so that the infrastructure can be discarded and recreated at will multiple times.

## Scenario to recreate:

Your company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.
You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.
This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

## Getting Started

These instructions below  will get you an undertstanding on how this project was builded and how to use the scripts , including  the construction of a "Udagram Web Sote" usinng Bootstrap4. Feel free to use them.

### Prerequisites

1. AWS account - Make sure you have an AWS account created and most importantly for Amazon, billing information setup :)

2. aws cli is installed and configured. To test, run the aws commands below.
```sh
aws --version

or 

aws s3 ls
```
3. A S3 bucket already created with another AWS Cloudformation IAC template:
File Name:
```sh
webapp-S3bucket.yml
```
   File Name: webapp-S3bucket.yml

- The above file generated a S3 bucket named: 
| Resource | Name |
| ------ | ------ |
| S3 | webapp-s3bucket-s3cloudfront-w5u9jy13vbmr [PlDb] | 

- The "udacity_udagram.zip" file was added as document to that bucket , and contains the files needed to recreate the "Udagram Web Site":
```sh
index.html --> the main page.
style.css --> the stylesheet.
app.js --> a small javascript code to control the carousel images.
``` 
4. Edit the "webapp-stack.yml" file and update/replace the line 449 with the full S3 path and file name of website zip. See AWS S3 console.

5. Create a Key Pair in AWS EC2 and take note of the name assigned to the key pair. Alternatively, upload the sample PEM file included in this repo.

6. Edit the "webapp-parameters.json"  file and update/replace the value of KeyPairName with the key pair name created in the previous step.



### AWS CLoudFormation Templates Description

A step by step series of examples that tell you how to get a development env running

| Template | Description |
| ------ | ------ |
| webapp-s3.bucket.yml | to create the S3 bucket ythat will be used later [PlDb] |
| webapp-stack.yml | to create the infraestructure (VPCs , SUbnets, EIP, Security Groups) and the servers ( ELB, AutoScaling group, BAstionHost, WebServers, IAM ROles ) [PlDb] |
| webapp-parameters.json | the parameters needed on the stack [PlDb] |


##  How to Running the templates

| Scripts | Description |
| ------ | ------ |
| create-stack.sh | to create the stack  [PlDb] |
| update-stack.sh | to update the stack  [PlDb] |
| destroy-stack.sh | to delete ( destroy) the stack  [PlDb] |


Example on how to execute the creation script:
```sh
> ./create-stack.sh Udagram-Stack webapp-stack.yml webapp-parameters.json
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Visual Studio Code](http://www.dropwizard.io/1.0.2/docs/) - Used as IDE to code
* [Lucid Chart](https://www.lucidchart.com/pages/) - to generate the diagram
* [BootStrap4](https://getbootstrap.com/) - Used to generate the WebSite as example

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

For the versions available, see the [tags on this repository](https://github.com/jfcb853/aws-cloudformation-udacity-project2.git/tags). 

## Authors

* **Javier Caparo** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)



## License

This project is licensed under the GNU GENERAL PUBLIC LICENSE - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Thanks to Udacity Nanodegree DevOps Program, really useful to learn a lot.