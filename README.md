
# Scalable Edge: Face Detection using AWS IoT Greengrass

## 📘 Project Overview

This project demonstrates the deployment of a machine learning–based face detection pipeline using AWS edge computing services. By leveraging AWS IoT Greengrass and associated services, we design a distributed architecture that performs real-time face detection on image data received from IoT devices. The goal is to offload computational tasks from centralized cloud infrastructure and enable intelligent processing directly at the edge—thereby reducing latency, preserving bandwidth, and enhancing privacy.

The project uses EC2 instances to emulate both IoT devices and edge nodes, integrating them through secure MQTT-based messaging. It showcases how AWS-native services can be orchestrated to build a production-grade edge-cloud pipeline for computer vision tasks.

## 🎯 Objectives

- Implement an edge computing pipeline for face detection using AWS services  
- Deploy and run machine learning models at the edge using AWS IoT Greengrass  
- Simulate IoT device communication using MQTT over AWS IoT Core  
- Enable real-time message routing from edge to cloud using AWS SQS  
- Achieve modularity and scalability in the ML inference workflow by separating detection and recognition stages  

## 🛠️ Methodology

1. **IoT Device Simulation**  
   An EC2 instance simulates an IoT device that encodes image frames as Base64 strings and publishes them to an MQTT topic via AWS IoT Core.

2. **Greengrass Core Deployment**  
   Another EC2 instance runs AWS IoT Greengrass Core. It hosts a custom Greengrass component that:
   - Subscribes to the MQTT topic
   - Decodes incoming image data
   - Uses a pretrained MTCNN model for face detection
   - Sends the detected face(s) to an AWS SQS queue for further processing

3. **Cloud Integration via SQS**  
   Detected face data is forwarded to AWS SQS, forming a bridge to any cloud-based consumer services such as AWS Lambda for face recognition or post-processing.

4. **Security & Provisioning**  
   All communication is secured using X.509 certificates managed through AWS IoT, and IAM roles are used to securely enable token-based access to SQS.

## ☁️ AWS Tech Stack

| **Service**                  | **Role in the Project**                                                                                                                             |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **AWS EC2**                  | Emulates IoT devices and edge nodes. Hosts the Greengrass Core and MQTT publisher scripts.                                                         |
| **AWS IoT Greengrass v2**    | Provides a local runtime for ML components. Enables packaging, deployment, and management of edge applications.                                    |
| **AWS IoT Core**             | MQTT broker for secure communication. Manages IoT Thing identities, certificates, and topics.                                                      |
| **AWS SQS**                  | Acts as a message buffer between edge and cloud systems. Receives detected face metadata for downstream processing.                                |
| **AWS IAM**                  | Manages secure access to AWS resources through token exchange roles and policy-based permissions for Greengrass and IoT devices.                  |
| **AWS IoT Device Management**| Supports device provisioning and configuration when registering Greengrass Core as an IoT Thing.                                                   |

## 📄 Academic Policy Notice

The source code for this project **cannot be uploaded or made public** as it falls under the academic submission for **CSE 546: Cloud Computing** at **Arizona State University**. Sharing or publishing the project’s implementation details would be a **violation of ASU’s academic integrity policy**.

For any academic or technical queries related to this project, please contact:

📧 **itewari1@asu.edu**
