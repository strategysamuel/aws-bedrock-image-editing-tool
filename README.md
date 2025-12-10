AWS Bedrock Image Editing Tool

Serverless image editing application powered by Amazon Bedrock, AWS Lambda, API Gateway, Amazon Cognito, DynamoDB, and AWS Amplify.

This project demonstrates how to build a complete, secure, scalable image-editing pipeline using Titan Image Generator v2 for inpainting and outpainting operations — fully serverless and production-ready.

🚀 Overview

Modern image editing often requires high-quality AI models, intuitive user interfaces, and scalable backend systems.
This project solves that by integrating:

🎨 Frontend UI hosted on AWS Amplify

🧠 Image generation with Amazon Titan (Bedrock)

🔐 Secure authentication via Cognito User Pools

🔌 API Gateway + Lambda for model invocation

🗄️ DynamoDB for logging & analytics

This solution is perfect for learning Bedrock, building real-world inpainting/outpainting tools, or extending into commercial use cases (real estate editing, product showcase cleanup, background removal, etc.)

🏗️ Architecture Diagram
🧱 **High-Level Architecture**

```text
[ User Browser ]
      │
      ▼
[AWS Amplify Hosting]
(Static frontend: index.html + JS + config.js + styles.css)
      │  HTTPS (Cognito auth + JWT)
      ▼
[Amazon API Gateway - REST API /dev/generate]
      │  Invokes
      ▼
[AWS Lambda - ImageEditBackend]
  • Validates JWT from Cognito
  • Parses mask, base image, and prompt
  • Calls Bedrock Titan Image Generator v2
  • Logs request/response metadata to DynamoDB
      │
      ├─► [Amazon Bedrock Runtime]
      │      • Model: amazon.titan-image-generator-v2:0
      │      • Returns edited images (base64)
      │
      └─► [Amazon DynamoDB - ImageGenerationTable]
             • Stores: request_id, timestamp, prompt, mode,
               input sizes, output size, generation time, success flag


🔍 Features
🎯 Image Editing Modes

INPAINTING – Modify inside the selected mask

OUTPAINTING – Extend background beyond the mask

PRECISE OUTPAINTING – Cleaner edges for real estate/product images

🛡️ Secure Auth

Cognito ensures only authenticated users can generate images.

📊 Analytics

Every request is logged:

request ID

timestamps

prompt text

model used

input image size

output image size

generation time in ms

success/failure state

Perfect for monitoring performance and usage.

### 2️⃣ Folder Structure

```md
📁 **Repository Structure**

```text
aws-bedrock-image-editing-tool/
├─ frontend/
│  ├─ index.html               # Image editing UI (canvas + controls)
│  ├─ config.js                # Cognito, API Gateway, region configuration
│  ├─ styles.css               # Neon terminal-style UI styling
│  └─ vite.svg (or other assets)  # Static assets used by the UI
│
├─ backend/
│  └─ lambda_function.py       # Lambda handler that calls Bedrock
│                              # and logs metadata to DynamoDB
│
├─ screenshots/
│  ├─ Login_Screen.png
│  ├─ Password_change_Screen.png
│  ├─ Authorisation_Screen.png
│  ├─ Imageupload_screen.png
│  ├─ Imageediting_screen.png
│  ├─ ImageGeneration_screen.png
│  ├─ DynamoDB_Imageconfirmation_Screen.png
│  └─ DynamoDB_AttributesConfirmation_Screen.png
│      # Screenshots used in the README / blog
│
└─ README.md                   # Project documentation


⚙️ AWS Services Used
Service	Purpose
Amazon Bedrock (Titan Image Generator v2)	Inpainting, outpainting image generation
AWS Lambda	Backend compute to call Bedrock and return results
API Gateway	REST API endpoint for frontend → Lambda
Amazon Cognito	User authentication and token validation
Amazon DynamoDB	Logging every image generation event
AWS Amplify Hosting	Frontend static website hosting
🧩 Backend Lambda Function

Full code is available in:

📁 backend/lambda_function.py
This function performs:

Request validation

Image + mask extraction

Titan model invocation

Error handling

DynamoDB structured logging

Response formatting

🖥️ Frontend

Located in:

📁 frontend/

Includes:

UI for image upload & masking

Prompt input

Mode selection

JWT auth handling

API request builder

Live preview + download

🧪 How to Run Locally

Clone the project:

git clone https://github.com/strategysamuel/aws-bedrock-image-editing-tool
cd aws-bedrock-image-editing-tool


Frontend is static — open index.html directly or host via Amplify.

Lambda deployment requires:

Titan model access

DynamoDB table named ImageGenerationTable

API Gateway with Cognito Authorizer

📸 Screenshots

All screenshots are located in /screenshots for blog/article integration.

🌐 Live Demo

Amplify Hosted App:
👉 https://staging.d10wzvh8ozqbav.amplifyapp.com/

📦 Repository Link

GitHub Repo:
👉 https://github.com/strategysamuel/aws-bedrock-image-editing-tool

📝 License

This project is for educational and workshop use.
