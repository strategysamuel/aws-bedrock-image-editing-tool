AWS Bedrock Image Editing Tool

Serverless Inpainting, Outpainting & Background Cleanup Using Amazon Bedrock Titan Image Generator v2

🔗 Live Demo (AWS Amplify Hosted App):
https://staging.d10wzvh8ozqbav.amplifyapp.com/

🚀 Overview

This project is a fully serverless image-editing application using Amazon Bedrock's Titan Image Generator v2.
Users can upload an image, draw a mask, and generate new content using:

INPAINTING – Modify selected region

OUTPAINTING – Extend background outward

PRECISE OUTPAINTING – High-fidelity extension for real-estate/product photos

All generations are logged in DynamoDB with analytics like:

Prompt

Model used

Image input/output size

Generation time

Success/failure

Perfect for learning AWS Bedrock, building professional editing tools, or extending into commercial use cases.

🧠 Why This Tool?

✔ Real-world use case (real estate, product photography, cleanup, restoration)
✔ Secure authentication via Amazon Cognito
✔ Scalable backend via Lambda + API Gateway
✔ Zero server maintenance (pure serverless)
✔ Analytics tracking for performance insights

🏗️ Architecture Diagram

Below is a clean, readable architecture representation for your README:

                     ┌──────────────────────────┐
                     │        User Browser       │
                     │  (AWS Amplify Hosted UI)  │
                     └──────────────┬───────────┘
                                    │
                                    ▼
                     ┌──────────────────────────┐
                     │   Amazon Cognito Auth    │
                     │  (User Login + JWT Token)│
                     └──────────────┬───────────┘
                                    │ (Authenticated)
                                    ▼
                     ┌──────────────────────────┐
                     │   Amazon API Gateway     │
                     │   POST /generate         │
                     └──────────────┬───────────┘
                                    │
                                    ▼
                     ┌──────────────────────────┐
                     │    AWS Lambda Backend    │
                     │  - Processes request     │
                     │  - Prepares Titan input  │
                     │  - Logs analytics        │
                     └──────────────┬───────────┘
                                    │
                                    ▼
                     ┌──────────────────────────┐
                     │ Amazon Bedrock Runtime   │
                     │ Titan Image Generator v2 │
                     └──────────────┬───────────┘
                                    │
                                    ▼
                     ┌──────────────────────────┐
                     │ Amazon DynamoDB Table    │
                     │  ImageGenerationTable     │
                     │ Logs each generation     │
                     └──────────────────────────┘

✨ Features
🎨 Image Editing Modes
Mode	What It Does
INPAINTING	Modify selected area of an image
OUTPAINTING	Extend image beyond original boundary
PRECISE OUTPAINTING	Cleaner, sharper extensions
🔒 Secure Auth

Only authenticated users can generate images. Cognito handles sign-up, sign-in, and password reset.

📊 DynamoDB Logging

Each request stores:

request_id

prompt

model_id

mode

input image size

output image size

generation time

success/failure

Perfect for auditing and analytics.

📁 Folder Structure

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


🛠️ AWS Services Used
AWS Service	Purpose
Amazon Bedrock	Titan Image Generator v2 for inpainting/outpainting
AWS Lambda	Backend logic + Bedrock invocation
Amazon API Gateway	REST endpoint for frontend
Amazon Cognito	Auth & JWT token validation
Amazon DynamoDB	Logging analytics + request metadata
AWS Amplify Hosting	Hosting the frontend
⚙️ Backend Lambda Logic (High-Level)

The Lambda function:

Validates request + JWT token

Extracts mask, base image & prompt

Prepares Titan Image Generator v2 request

Calls Bedrock Runtime

Returns generated images

Stores analytics in DynamoDB

Error-handling ensures all failures still get logged.

📈 Scaling Strategy
🌐 Frontend Scaling

Amplify Hosting auto-scales globally with CDN distribution.

⚙️ Backend Scaling

API Gateway scales to tens of thousands of RPS

Lambda auto-scales with concurrency

DynamoDB auto-scales with on-demand capacity

🔮 Future Enhancements

Add S3 for storing images

Add CloudWatch dashboards for metrics

Add model selection (SDXL, Imagen, etc.)

Add batch editing & presets

📚 Full Code and Resources

🔗 GitHub Repository:
https://github.com/strategysamuel/aws-bedrock-image-editing-tool

🔗 Live Demo:
https://staging.d10wzvh8ozqbav.amplifyapp.com/
