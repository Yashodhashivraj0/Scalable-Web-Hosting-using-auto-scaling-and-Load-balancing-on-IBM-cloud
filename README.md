# Scalable-Web-Hosting-using-auto-scaling-and-Load-balancing-on-IBM-cloud
Scalable Web Hosting with Auto Scaling & Load Balancing on IBM Cloud

Overview

This project demonstrates how to set up a scalable web hosting infrastructure using IBM Cloud with Auto Scaling and Load Balancing. The setup includes:

Virtual Private Cloud (VPC) for secure networking.

Load Balancer for distributing traffic across multiple instances.

Auto Scaling to handle traffic spikes efficiently.

Flask Web Application as the hosted service.

Prerequisites

Before running this project, ensure you have:

IBM Cloud Account (Sign Up)

IBM Cloud API Key (Generate from IAM > API Keys)

Python (>=3.7) installed

Jupyter Notebook (Optional, for step-by-step execution)

Installation

1. Install Required Packages

Run the following command to install the required Python packages:

pip install ibm-cloud-sdk-core ibm-vpc ibm-platform-services flask

2. Authenticate with IBM Cloud

Replace your_ibm_cloud_api_key with your actual IBM Cloud API key in the script:

from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from ibm_vpc import VpcV1

api_key = "your_ibm_cloud_api_key"

authenticator = IAMAuthenticator(api_key)
vpc_service = VpcV1(authenticator=authenticator)

Setting Up Infrastructure

3. Create a Virtual Private Cloud (VPC)

vpc_name = "my-scalable-vpc"
response = vpc_service.create_vpc(name=vpc_name)
print(response)

4. Create a Load Balancer

from ibm_platform_services import GlobalLoadBalancerV1

lb_service = GlobalLoadBalancerV1(authenticator=authenticator)
response = lb_service.create_load_balancer(
    name="my-load-balancer",
    type="application",
    is_public=True
)
print(response)

5. Configure Auto Scaling

from ibm_platform_services import AutoScalingV1

autoscale_service = AutoScalingV1(authenticator=authenticator)
response = autoscale_service.create_policy(
    group_id="your-autoscaling-group-id",
    name="scale-policy",
    min_membership_count=1,
    max_membership_count=5,
    cool_down_period_sec=60
)
print(response)

Deploying a Web Application

6. Create a Simple Flask Web App

from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Welcome to Scalable Web Hosting on IBM Cloud!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

Run the script and access the web app at http://localhost:5000.

Testing the Setup

Check IBM Cloud Dashboard to confirm that the VPC, Load Balancer, and Auto Scaling are set up correctly.

Simulate Traffic using tools like Apache JMeter or Locust to observe Auto Scaling in action.

Next Steps

Deploy the Flask app on IBM Kubernetes Service (IKS) for better scalability.

Integrate a Database Service (e.g., IBM Cloud Databases) for dynamic applications.


