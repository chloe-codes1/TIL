# AWS IoT 

> IoT (Internet Of Things) services for industrial, consumer, and commercial solutions

<br>

- AWS IoT provides broad and deep functionality, spanning the edge to the cloud, so you can build IoT solutions for virtually any use case across a wide range of devices
- Since AWS IoT integrates with **AI services**, you can make devices smarter, even without Internet connectivity
- AWS IoT can easily scale as your device fleet grows and your business requirements evolve
- AWS IoT also offers the most comprehensive security features so you can create **preventative security policies** and **respond immediately to potential security issues**

<br>

<br>

### What AWS IoT offers

> AWS IoT provides device software, control services, and data services

<br>

![AWS IoT products we offer](https://d1.awsstatic.com/IoT/category%20page/Virtuous%20Cycle%20for%20Category%20Page.97e042ebfe3d5f25280d512e7d29bc9a924b167b.png)

<br>

- #### Device software 

  : enables you to securely connect devices, gather data, and take intelligent actions locally, even when Internet connectivity is not available.

- #### Connectivity & Control 

  : services allow you to control, manage, and secure large and diverse device fleets

- #### Analytics 

  : services help you extract value from IoT data.

<br><br>

## AWS IoT Services

<br>

### 1. Device Software

> Connect your devices & operate them at the edge

<br>

#### 1-1. FreeRTOS

<br>

![How to use Amazon FreeRTOS](https://d1.awsstatic.com/diagrams/Updated%20FreeRTOS%20how%20it%20works.fe61439aeb67580604f20cc89dba2bf1c89c1dc0.png)<br>

- FreeRTOS is an **open source**, **real-time operating system** for `microcontrollers `that makes small, low-power edge devices easy to program, deploy, secure, connect, and manage.
- Distributed freely under the MIT open source license, FreeRTOS includes a kernel and a growing set of software libraries suitable for use across industry sectors and applications
- This includes securely connecting your small, low-power devices to AWS cloud services like AWS IoT Core or to more powerful edge devices running `AWS IoT Greengrass`
- FreeRTOS is built with an emphasis on reliability and ease of use.

<br>

<br>

#### 1-2. AWS IoT Greengrass

<br>

- AWS IoT Greengrass seamlessly extends AWS to edge devices so they can act locally on the data they generate, while still using the cloud for management, analytics, and durable storage
- With AWS IoT Greengrass, connected devices can run [AWS Lambda](https://aws.amazon.com/lambda/) functions, Docker containers, or both, execute predictions based on machine learning models, keep device data in sync, and communicate with other devices securely – even when not connected to the Internet
- With AWS IoT Greengrass, you can use familiar languages and programming models to create and test your device software in the cloud, and then deploy it to your devices
- AWS IoT Greengrass can be programmed to filter device data, manage the life-cycle of that data on the device, and only transmit necessary information back to AWS
- You can also connect to third-party applications, on-premises software, and AWS services out-of-the-box with AWS IoT Greengrass Connectors
- Connectors also jumpstart device onboarding with pre-built protocol adapter integrations and allow you to streamline authentication via integration with [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/).

<br>

**How AWS IoT Greengrass works**

![AWS IoT Greengrass - How it Works](https://d1.awsstatic.com/diagrams/product-page-diagram-Greengrass_How-It-Works.dfbc94bee098d673fa9fdc1d69c022daa7670251.png)

- AWS IoT Greengrass Core devices, AWS IoT Device SDK-enabled devices, and FreeRTOS devices can be configured to communicate with one another in an AWS IoT Greengrass group
- If the AWS IoT Greengrass Core device loses connectivity to the cloud, devices in the AWS IoT Greengrass group can continue to communicate with each other over the local network
- An AWS IoT Greengrass group may represent one floor of a building, one truck, or an entire mining site.

<br>

![AWS IoT Greengrass Connectors](https://d1.awsstatic.com/r2018/b/product-page-diagram-AWS-Greengate-Launch_Application-Arch@1.5x.db4d6299f3d918d6c1006764b2c65923f9ff1ceb.png)

- AWS IoT Greengrass provides pre-built connectors so you can easily extend edge device functionality without writing code
- AWS IoT Greengrass Connectors enable you to quickly connect to third-party applications, on-premises software, and AWS services at the edge.

<br>

![AWS IoT Greengrass Security](https://d1.awsstatic.com/r2018/b/Greengrass/Product-Page-Diagram-Greenkey.aac67be473d3825a8a3a93531568c212485771c2.png)

- AWS IoT Greengrass provides hardware root of trust private key storage for edge devices
- You can use AWS IoT Greengrass capabilities alongside hardware-secured message encryption.

<br>

<br>

### 2. Connectivity & Control Services

> Secure, control, and manage your devices from the cloud

<br>

#### 2-1. AWS IoT Core

- AWS IoT Core lets connected devices easily and securely interact with cloud applications and other devices
- AWS IoT Core can support billions of devices and trillions of messages, and can process and route those messages to AWS endpoints and to other devices reliably and securely
- With AWS IoT Core, your applications can keep track of and communicate with all your devices, all the time, even when they aren’t connected
- AWS IoT Core also makes it easy to use AWS and Amazon services like `AWS Lambda`, `Amazon Kinesis`, `Amazon S3`, `Amazon SageMaker`, `Amazon DynamoDB,` `Amazon CloudWatch`, `AWS CloudTrail`, `Amazon QuickSight`, and `Alexa Voice Service` to build IoT applications that gather, process, analyze and act on data generated by connected devices, without having to manage any infrastructure

<br><br>

#### 2-2. AWS IoT Device Defender

<br>

![How it Works - AWS IoT Device Defender](https://d1.awsstatic.com/IoT/How%20it%20Works%20AWS%20IoT%20Device%20Defender.1839e9f3b9630f6db29cd5b4c63984c1bfdd5ebb.png)

<br>

- AWS IoT Device Defender is a **fully managed service** that helps you secure your fleet of IoT devices
- AWS IoT Device Defender **continuously audits your IoT configurations** to make sure that they aren’t deviating from security best practices
- AWS IoT Device Defender also lets you continuously **monitor security metrics** from devices and AWS IoT Core for deviations from what you have defined as appropriate behavior for each device
- AWS IoT Device Defender can **send alerts** to the AWS IoT Console, Amazon CloudWatch, and Amazon SNS
  - If you determine that you need to take an action based on an alert, you can use [AWS IoT Device Management](https://aws.amazon.com/iot-device-management/) to take mitigating actions such as pushing security fixes

<br>

<br>

#### 2-3. AWS IoT Device Management

<br>

![How it Works - AWS IoT Device Management](https://d1.awsstatic.com/IoT/product-page-diagram-AWSIoTDeviceManagement_how_it_works.d83855d6d1688452da09c31f43f0aa0418e4fef9.png)

<br>

- AWS IoT Device Management makes it easy to securely register, organize, monitor, and remotely manage IoT devices at scale
- With AWS IoT Device Management, you can register your connected devices individually or in bulk, and easily manage permissions so that devices remain secure
- You can also organize your devices, monitor and troubleshoot device functionality, query the state of any IoT device in your fleet, and send firmware updates `over-the-air (OTA)`
- AWS IoT Device Management is agnostic to device type and OS, so you can manage devices from constrained microcontrollers to connected cars all with the same service
- AWS IoT Device Management allows you to **scale your fleets** and **reduce the cost and effort** of managing large and diverse IoT device deployments.

<br><br>

### 3. Analytics Services

> Work with IoT data faster to extract value from your IoT data

<br>

#### 3-1. AWS IoT Analytics

: AWS IoT Analytics makes it easy to run sophisticated analytics on massive volumes of IoT data.

<br>

#### 3-2. AWS IoT SiteWise

: AWS IoT SiteWise makes it easy to collect, organize and analyze industrial data at scale.

<br>

#### 3-3. AWS IoT Events

: AWS IoT Events makes it easy to detect and respond to events from large numbers of IoT sensors and applications.

<br>

#### 3-4. AWS IoT Things Graph

: AWS IoT Things Graph makes it easy to connect different devices and cloud services to build IoT applications.



<br><br>

<br>

#### Summary

1. AWS IoT는 edge 영역부터 cloud에 이르기까지 광범위하고 심층적인 기능을 제공하므로 다양한 device에서 거의 모든 사용 사례에 적합한 IoT Solution을 개발할 수 있다
2. AWS IoT는 device software, control service & data service를 제공한다