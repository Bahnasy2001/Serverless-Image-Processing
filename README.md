# 📷 Serverless Image Editor

A fast, secure, and scalable serverless image processing application built on AWS. Users can upload images via a modern web interface, and the system automatically resizes them using a fully managed backend.

> 🚀 Developed by Hassan El Bahnasy as part of the Manara Solution Architect course.

---

## 🧩 Overview

This project showcases a full-stack, event-driven image processing solution built entirely on serverless AWS services. It enables image uploads, automated resizing, and downloads — all from a static HTML site hosted on S3.

---

## 🛠️ Technology Stack

| Layer        | Service                          | Purpose                               |
|--------------|----------------------------------|---------------------------------------|
| Frontend     | HTML, CSS, JS + S3 Static Site   | User interface                        |
| API          | API Gateway + Lambda             | Presigned URL generation              |
| Processing   | S3 Event Trigger + Lambda        | Image resize on upload                |
| Storage      | S3 (Original & Processed buckets)| Secure file storage                   |
| Security     | IAM, Bucket Policies, CORS       | Least-privilege access + public read  |

---

## 📸 Workflow

1. User selects an image on the frontend.
2. Frontend fetches a presigned upload URL from API Gateway.
3. Image is uploaded directly to the original S3 bucket.
4. Upload triggers a Lambda function that:
   - Resizes the image to a width of 500px (maintaining aspect ratio)
   - Stores the result in the processed S3 bucket.
5. User can download the resized image from a secure public URL.

---
## 🗺️ Default Architecture

![Architecture](Blank%20diagram.png)

---

## 🧪 Demo

You can preview the app by opening the S3 static website URL hosting the HTML frontend.

✅ Upload → 📤 Resize → 📥 Download
### 🔗 Live URL : [Link](http://bahnasy-manara-project-main-bucket.s3-website.eu-central-1.amazonaws.com)

---

## 📁 Project Structure

```
serverless-image-editor/
│   .DS_Store
│   Blank diagram.png
│   README.md
│
├───Lambda/
│   ├───GeneratePresignedURL/
│   │   └── generate_presigned_url.py   # Lambda to generate presigned POST URLs
│   │
│   └───ResizeImage/
│       ├── Dockerfile                  # (Optional) Docker image for image resizing Lambda
│       └── lambda_function.py          # Lambda triggered by S3 event to resize images
│
└───WebPage/
    ├── .DS_Store
    ├── favicon.ico                     # Optional browser tab icon
    ├── index.html                      # Frontend interface
    └── logo.png                        # App logo displayed in the header
````

---

## 🔐 Security & Access Control

- Original Bucket:
  - Only accepts image uploads via presigned POST (Content-Type enforced)
- Processed Bucket:
  - Public read-only for resized files (for download only)
- CORS configured for upload (POST) and download (GET)
- IAM policies follow least privilege principles
- Lambda execution roles grant scoped S3 access

---

## 🔄 Example Presigned Upload Flow

Thanks for pointing that out. Here's the corrected formatting and content of that section for your README or documentation:



#### Frontend makes a request


```GET https://{api_id}.execute-api.{region}.amazonaws.com/prod/upload?filename=your_image.jpg```

Lambda returns:


````json
{
  "url": "https://bahnasy-original-images.s3.amazonaws.com/",
  "fields": {
    "key": "original/your_image.jpg",
    "acl": "private",
    "Content-Type": "image/jpeg",
  }
}
````

Frontend performs a direct POST upload to the S3 bucket using form data.


---

## 📚 Credits

Built by Hassan El Bahnasy as a graduation project during the Manara AWS Solution Architect training track.

---


## 👤 Author

This project was created by [Hassan El Bahnasy](https://www.linkedin.com/in/hassanbahnasy) as part of the Manara Solution Architect course.
It is intended for educational purposes and to demonstrate serverless image processing with AWS.

* 💻 GitHub: [Bahnasy2001](https://github.com/Bahnasy2001)
* 🌐 LinkedIn: [hassanbahnasy](https://www.linkedin.com/in/hassanbahnasy)



