# PROJECT-HOST-WEBSITE-USING-S3
Static Website Hosting with AWS S3, Cloudflare & GitHub Actions
📌 Project Overview

This project demonstrates how to host and deploy a static website using Amazon S3 as the hosting service, Cloudflare for DNS and CDN, and GitHub Actions for CI/CD automation.

Whenever code is pushed to the repository, GitHub Actions automatically builds and deploys the updated files to the S3 bucket. Cloudflare then serves the website globally with caching and HTTPS support.

🛠️ Tech Stack

AWS S3 → Static website hosting

AWS IAM → Access management for CI/CD pipeline

Cloudflare → Domain management, SSL, and CDN caching

GitHub Actions → Continuous deployment pipeline

HTML / CSS / JavaScript → Static frontend

⚙️ Architecture Workflow

Code is committed and pushed to GitHub.

GitHub Actions workflow triggers on main branch.

Build and sync files to S3 bucket (harshithamd.space).

S3 Static Website Hosting serves the files.

Cloudflare DNS points the domain (harshithamd.space) to the S3 static hosting endpoint.

Website is available worldwide with Cloudflare CDN & SSL.

🚀 Setup Instructions
1️⃣ Create an S3 Bucket

Name it after your domain - harshithamd.space

Disable Block Public Access.

Enable Static Website Hosting and set:

Index document → index.html

Error document → error.html

2️⃣ Set Permissions

Add bucket policy:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example.com/*"
    }
  ]
}

3️⃣ Configure Cloudflare

Add a CNAME record for @ and www → point to S3 website endpoint.

Enable Proxy (orange cloud) for CDN & SSL.

4️⃣ Setup GitHub Actions CI/CD

workflow path:
 (.github/workflows/deploy.yml):

name: Deploy static site to S3

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Deploy to S3
        run: |
          aws s3 sync ./public s3://example.com \
            --delete \
            --acl public-read \
            --cache-control "max-age=31536000"


🔑 Requires AWS credentials added as GitHub repository secrets.

✅ Features

Fully automated deployments with GitHub Actions

Low-cost hosting with AWS S3

Global CDN and free SSL via Cloudflare

Caching optimization (index.html served with no-cache, assets long cached)

Scalable and serverless hosting

🌍 Live Site: https://harshithamd.space
