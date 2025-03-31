📌 Static Website Hosting on AWS S3
![image alt](https://github.com/aditya12-g/static-website-hosting-s3/blob/main/Screenshot%20(23).png)

🚀 A fully automated Terraform-based setup for hosting a static website on AWS S3 with public access enabled via a bucket policy.

📸 Project Overview

This project provisions an S3 bucket with static website hosting enabled and uploads an index.html and error.html page. The bucket policy is configured to allow public access to the hosted website.

📌 Key Features:

✅ Static Website Hosting on AWS S3

✅ Infrastructure as Code using Terraform

✅ Public Access Configuration via Bucket Policy

✅ Custom Error Page Handling

💽 Folder Structure


static-website-hosting-s3/
│── main.tf                  # Terraform configuration for AWS S3 bucket
│── variables.tf              # Terraform variables for customization
│── outputs.tf                # Outputs (S3 website endpoint)
│── index.html                # Main landing page for the static website
│── error.html                # Custom error page
│── terraform.tfstate         # Terraform state file (not included in repo)
└── README.md                 # Project documentation


🛠️ Prerequisites

Before deploying, ensure you have:

AWS CLI installed and configured (aws configure)

Terraform installed (terraform -v)

🚀 Deployment Steps

1. Clone the Repository

git clone https://github.com/aditya12-g/static-website-hosting-s3.git
cd static-website-hosting-s3

2. Initialize Terraform

terraform init

3. Validate Configuration

terraform validate

4. Deploy to AWS

terraform apply -auto-approve

5. Get the Website URL

After deployment, Terraform will output the S3 Website Endpoint. Open it in a browser to view your site.

📝 Terraform Configuration

S3 Bucket Configuration

resource "aws_s3_bucket" "mybucket" {
  bucket = var.bucketname
}

resource "aws_s3_bucket_website_configuration" "website" {
  bucket = aws_s3_bucket.mybucket.id
  index_document {
    suffix = "index.html"
  }
  error_document {
    key = "error.html"
  }
}

Bucket Policy (Public Access)

resource "aws_s3_bucket_policy" "public_read" {
  bucket = aws_s3_bucket.mybucket.id
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Sid       = "PublicReadGetObject"
        Effect    = "Allow"
        Principal = "*"
        Action    = "s3:GetObject"
        Resource  = "${aws_s3_bucket.mybucket.arn}/*"
      }
    ]
  })
}

📌 Outputs

After applying Terraform, you will get:

✅ Website URL – http://<your-bucket-name>.s3-website-<region>.amazonaws.com/

📢 Contributing

Feel free to fork this repository, improve it, and submit a pull request! Contributions are always welcome. 😊

📚 License

This project is open-source and available under the MIT License.





