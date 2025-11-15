# 🚀 Static Website Hosting on AWS S3

![AWS S3](https://img.shields.io/badge/AWS-S3-orange?style=for-the-badge&logo=amazon-aws)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

A modern, responsive static website hosted on Amazon S3, demonstrating cloud-based web hosting capabilities with high availability and scalability.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Deployment Steps](#deployment-steps)
- [Project Structure](#project-structure)
- [Cost Estimation](#cost-estimation)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🌟 Overview

This project showcases how to deploy a static website on AWS S3 bucket with optimal performance and cost-efficiency. The website features a clean, modern design built with HTML5 and CSS3, perfect for portfolios, landing pages, or informational sites.

## ✨ Features

- **Fully Responsive Design** - Works seamlessly across all devices
- **Fast Loading Times** - Leveraging AWS S3's CDN capabilities
- **Cost-Effective** - Pay only for what you use
- **Highly Available** - 99.99% uptime SLA from AWS
- **Secure** - HTTPS support with SSL/TLS
- **Scalable** - Automatically handles traffic spikes
- **Easy Maintenance** - Simple file uploads to update content

## 🏗️ Architecture

```
┌─────────────┐
│   User      │
└──────┬──────┘
       │
       ▼
┌─────────────────┐
│  Route 53 (DNS) │
└──────┬──────────┘
       │
       ▼
┌─────────────────────┐
│  CloudFront (CDN)   │
│    [Optional]       │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   S3 Bucket         │
│   Static Website    │
│   Hosting           │
└─────────────────────┘
```

## 📦 Prerequisites

Before you begin, ensure you have:

- ✅ An AWS Account ([Sign up here](https://aws.amazon.com/))
- ✅ AWS CLI installed and configured ([Installation Guide](https://aws.amazon.com/cli/))
- ✅ Basic knowledge of HTML/CSS
- ✅ A custom domain name (optional)

## 🚀 Deployment Steps

### Step 1: Create an S3 Bucket

```bash
aws s3 mb s3://your-unique-bucket-name --region us-east-1
```

### Step 2: Enable Static Website Hosting

```bash
aws s3 website s3://your-unique-bucket-name/ \
  --index-document index.html \
  --error-document error.html
```

### Step 3: Configure Bucket Policy

Create a `bucket-policy.json` file:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-unique-bucket-name/*"
    }
  ]
}
```

Apply the policy:

```bash
aws s3api put-bucket-policy \
  --bucket your-unique-bucket-name \
  --policy file://bucket-policy.json
```

### Step 4: Upload Website Files

```bash
aws s3 sync . s3://your-unique-bucket-name/ \
  --exclude ".git/*" \
  --exclude "README.md"
```

### Step 5: Access Your Website

Your website will be available at:
```
http://your-unique-bucket-name.s3-website-us-east-1.amazonaws.com
```

## 📁 Project Structure

```
static-website-aws-s3/
│
├── index.html              # Main HTML file
├── styles.css              # Stylesheet
├── README.md               # Project documentation
├── bucket-policy.json      # S3 bucket policy
│
└── assets/                 # (Optional) Images and resources
    ├── images/
    └── fonts/
```

## 💰 Cost Estimation

AWS S3 pricing is based on:

- **Storage**: $0.023 per GB/month (first 50 TB)
- **Requests**: $0.0004 per 1,000 GET requests
- **Data Transfer**: First 1 GB/month free, then $0.09 per GB

**Example**: A 10MB website with 10,000 monthly visitors ≈ **$0.50 - $2.00/month**

## 🔧 Troubleshooting

### Issue: 403 Forbidden Error

**Solution**: Check your bucket policy allows public read access.

### Issue: 404 Not Found

**Solution**: Ensure `index.html` is in the root directory and static website hosting is enabled.

### Issue: CSS Not Loading

**Solution**: Verify the CSS file path in your HTML and ensure it was uploaded correctly.

## 🌐 Optional Enhancements

### Add CloudFront CDN

```bash
# Improves global performance and enables HTTPS
aws cloudfront create-distribution --origin-domain-name your-bucket.s3.amazonaws.com
```

### Configure Custom Domain

1. Register domain in Route 53
2. Create hosted zone
3. Add A record pointing to S3 endpoint or CloudFront distribution

### Enable Versioning

```bash
aws s3api put-bucket-versioning \
  --bucket your-unique-bucket-name \
  --versioning-configuration Status=Enabled
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Contact

Your Name - Tina Yerne

Project Link: [https://github.com/tinayerne04/static-website-aws-s3](https://github.com/tinayerne04/static-website-aws-s3)

---

⭐ **If you found this project helpful, please consider giving it a star!** ⭐

---

## 📚 Additional Resources

- [AWS S3 Static Website Hosting Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [AWS CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/)
- [Route 53 Documentation](https://docs.aws.amazon.com/route53/)
- [AWS Free Tier](https://aws.amazon.com/free/)

---

**Built with ❤️ using AWS S3**
