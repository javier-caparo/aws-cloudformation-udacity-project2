# Project :  Deploying a High-Availability Web Application Using AWS CloudFormation

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)]

Infrastructure-as-code (IAC) that automates the process of creating a secured and HA environment , deploying  a WebApp  (packaged and staged in AWS S3 Storage) into a cluster of NGINX Servers. The script contains all the configurations needed for a repeatable process so that the infrastructure can be discarded and recreated at will multiple times.

## Scenario to recreate:

Your company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.
You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.
This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

[![AWS Cloudformation](https://cdn.lynda.com/video/504618-185-636144053204152091_338x600_thumb.jpg)]

## Getting Started

These instructions below  will get you an undertstanding on how this project was builded and how to use the scripts , including  the construction of a "Udagram Web Sote" usinng Bootstrap4. Feel free to use them.

### Prerequisites

1. AWS account - Make sure you have an AWS account created and most importantly for Amazon, billing information setup :)

2. aws cli is installed and configured ( remember your credentials). To test, run the aws commands below.
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
| S3 | webapp-s3bucket-s3cloudfront-w5u9jy13vbmr | 

- The "udacity_udagram.zip" file was added as document to that bucket , and contains the files needed to recreate the "Udagram Web Site":
```sh
index.html --> the main page.
style.css --> the stylesheet.
app.js --> a small javascript code to control the carousel images.
``` 
4. Edit the "webapp-stack.yml" file and update/replace the line 449 with the full S3 path and file name of website zip. See AWS S3 console.

5. Create a Key Pair in AWS EC2 and take note of the name assigned to the key pair. Alternatively, upload the sample PEM file included in this repo. The "KeyPair" is requested as parameter in "webapp-parameters.json" , so don't forget incude in.

6. Edit the "webapp-parameters.json"  file and update/replace the value of KeyPairName with the key pair name created in the previous step.



### AWS CLoudFormation Templates Description

A step by step series of examples that tell you how to get a development env running

| Template | Description |
| ------ | ------ |
| webapp-s3.bucket.yml | to create the S3 bucket ythat will be used later |
| webapp-stack.yml | to create the infraestructure (VPCs , SUbnets, EIP, Security Groups) and the servers ( ELB, AutoScaling group, BAstionHost, WebServers, IAM ROles ) |
| webapp-parameters.json | the parameters needed on the stack |

- Diagram in Lucid Chart:
[![Lucid Chart](https://webapp-s3bucket-s3cloudfront-w5u9jy13vbmr.s3-us-west-2.amazonaws.com/Udagram+WebApp+Project+-+Udacity.png)]

- Template Designer in CloudFormation
[![Template Designer](https://webapp-s3bucket-s3cloudfront-w5u9jy13vbmr.s3-us-west-2.amazonaws.com/webapp-template-designer.png)]

##  How to Running the scripts with the templates

| Scripts | Description |
| ------ | ------ |
| create-stack.sh | to create the stack  [PlDb] |
| update-stack.sh | to update the stack  [PlDb] |
| destroy-stack.sh | to delete ( destroy) the stack  [PlDb] |


Example on how to execute the creation script:
```sh
> ./create-stack.sh udagram-Stack webapp-stack.yml webapp-parameters.json
```

Example on how to execute the deletion script:
```sh
> ./destroy-stack.sh udagram-Stack 
```
Note:
* if you are cloning the repository, don't forget give executable permissions to the "*.sh" scripts. Example:
```sh
> chmod +x *.sh
```

## Tests

1. Check the results of the execution of your script in AWS CloudFormation Console ( or aws cli). Must be " STATUS : CREATE COMPLETE"
* using aws cli (exmaple):
```sh
$ aws cloudformation describe-stacks --stack-name udagram-stack
```

2. On the output results  you will be the htpp link to the "udagram webapp" created: Example:
```sh
"OutputKey": "WebAppLoadBalancerDNSName",
                    "OutputValue": "http://udagr-WebAp-S2YEAO61BWAI-33908833.us-west-2.elb.amazonaws.com",
                    "Description": "DNS name or Public URL of the Load Balancer",
                    "ExportName": "MyUdagramProject-LB-DNSName"
```

3. You can connect to the BAstion HOST remotely and ping the WEb Servers for example . See "results" subdirectory on this repository to find screenshoots and some checks performeed.

4. and also you can check that  your Web Servers were installed with NGINX:
```sh
systemctl status nginx
```

5. The configuration included a Scaling Up and Scaling down actions on WebServer AutoScalign group. so don't afraid if your ec2 isntances goes to terminated after 5 minutes ( cooldown period ) if you are not using them!!!! ( Nice !!) 

## Built With

* [Visual Studio Code](http://www.dropwizard.io/1.0.2/docs/) - Used as IDE to code
* [Lucid Chart](https://www.lucidchart.com/pages/) - to generate the diagram
* [BootStrap4](https://getbootstrap.com/) - Used to generate the WebSite as example

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

For the versions available, see the [tags on this repository](https://github.com/jfcb853/aws-cloudformation-udacity-project2.git/tags). 

## Authors

* **Javier Caparo** - *javier.caparo@gmail.com* - [WebSite](http://javier-caparo.com/)

## License

This project is licensed under the GNU GENERAL PUBLIC LICENSE - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Thanks to Udacity Nanodegree DevOps Program, really useful to learn a lot.