# Data_Base_001
AWS testing
https://github.com/Kevin-byt/AWS-Projects/tree/main/S3%20Static%20Website
 https://www.datacamp.com/blog/top-aws-projects
 


Hosting a **static website on AWS** is straightforward using **Amazon S3 (Simple Storage Service)**. Below is a **step-by-step guide** with an example that helps you deploy a basic HTML website.

---

## 🧾 What You’ll Need:

* An **AWS account**
* A simple **static website** (e.g., an `index.html` file)
* (Optional) A custom domain (via Route 53 or another DNS provider)

---

## ✅ Step-by-Step Guide to Host a Static Website Using Amazon S3:

---

### 🔹 Step 1: Prepare Your Website Files

**Example files:**

```html
// index.html
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Website</title>
</head>
<body>
    <h1>Hello from AWS S3!</h1>
</body>
</html>
```

Put this in a folder like `my-static-site`.

---

### 🔹 Step 2: Log in to AWS Console

* Visit: [https://aws.amazon.com](https://aws.amazon.com)
* Log in with your credentials

---

### 🔹 Step 3: Create an S3 Bucket

1. Go to **Services** → **S3**
2. Click **Create bucket**
3. Set the bucket name (must be globally unique, e.g., `my-website-2025`)
4. **Uncheck** "Block all public access" (very important for public websites)
5. Acknowledge the warning and click **Create bucket**

---

### 🔹 Step 4: Upload Website Files

1. Click on the bucket name you just created
2. Click **Upload**
3. Add `index.html` (and any other assets like CSS or images)
4. Click **Upload**

---

### 🔹 Step 5: Make Files Public

You can either:

* Make the whole bucket public via **Bucket Policy**
* Or make individual files public

To make a file public:

1. Go to the file (e.g., `index.html`)
2. Click **Actions** → **Make public** (or under Permissions)

---

### 🔹 Step 6: Enable Static Website Hosting

1. Go to **Properties** tab of the bucket
2. Scroll to **Static website hosting**
3. Enable it
4. Enter:

   * **Index document**: `index.html`
   * (Optional) **Error document**: `error.html`
5. Save changes

---

### 🔹 Step 7: Access Your Website

After enabling, you’ll see a **bucket endpoint** like:

```
http://my-website-2025.s3-website-us-east-1.amazonaws.com
```

Open this in your browser — your static website should appear!

---

## 🌐 Optional: Use a Custom Domain (with Route 53)

If you want to use a custom domain:

1. Buy a domain (via Route 53 or another registrar)
2. In Route 53:

   * Create a **Hosted Zone**
   * Add an **A Record** → **Alias** to your S3 website endpoint
3. Update your domain's **Name Servers (NS)** to match Route 53

Let me know if you want the **custom domain steps** in detail.

---

## ✅ Summary

| Step | Task                             |
| ---- | -------------------------------- |
| 1    | Create `index.html`              |
| 2    | Create S3 bucket                 |
| 3    | Upload files                     |
| 4    | Make files public                |
| 5    | Enable static website hosting    |
| 6    | Access via website endpoint      |
| 7    | (Optional) Connect custom domain |

---

Would you like a **deployment automation** using AWS CLI or Terraform as well?

Absolutely! Let's walk through **5 different website hosting methods on AWS**, explained in **beginner-friendly, step-by-step instructions**, assuming you're new to AWS. Each example includes simple steps and explains what's happening along the way.

---

## ✅ 1. Static Website Hosting using Amazon S3

### 📌 Goal:

Host a basic HTML website with no backend (like a portfolio or landing page).

---

### 👣 Step-by-Step:

#### Step 1: Prepare your website files

* Create a folder on your computer: `my-website`
* Inside, add a simple `index.html`:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head><title>My First AWS Site</title></head>
<body>
<h1>Hello from AWS S3!</h1>
</body>
</html>
```

---

#### Step 2: Sign in to AWS

* Go to: [https://aws.amazon.com](https://aws.amazon.com)
* Click **Sign in to Console**

---

#### Step 3: Create an S3 Bucket

1. Go to **S3** from AWS Services.
2. Click **Create Bucket**
3. Enter a unique bucket name: `my-first-static-site-123`
4. **Region**: Choose your region (e.g., US East - N. Virginia)
5. **Uncheck** “Block all public access”
6. Check the box to acknowledge and click **Create bucket**

---

#### Step 4: Upload Your Files

1. Click on your bucket name
2. Click **Upload** > **Add files**
3. Choose your `index.html`
4. Click **Upload**

---

#### Step 5: Enable Static Website Hosting

1. Go to the **Properties** tab of the bucket
2. Scroll down to **Static website hosting**
3. Click **Edit**
4. Choose: **Enable**
5. Enter:

   * Index document: `index.html`
6. Click **Save changes**

---

#### Step 6: Make Your Files Public

1. Go to the **Permissions** tab
2. Click **Bucket policy**
3. Paste the following policy (replace `your-bucket-name`):

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::your-bucket-name/*"
  }]
}
```

4. Click **Save**

---

#### Step 7: Visit Your Website

* Go to **Properties** > **Static Website Hosting**
* Copy the **website endpoint URL**
* Paste it in your browser — you should see your HTML page!

---

✅ **You just hosted your first website using AWS S3!**

---

## ✅ 2. Static Website with S3 + CloudFront (HTTPS & CDN)

### 📌 Goal:

Same as #1, but faster globally and supports HTTPS (SSL)

---

### 👣 Step-by-Step:

#### Step 1: First, complete S3 Hosting (steps 1–7 above)

#### Step 2: Go to **CloudFront**

* Click **Create Distribution**
* Choose **Web**
* **Origin domain**: Select your S3 bucket website endpoint
* Keep defaults or set:

  * Viewer Protocol Policy: Redirect HTTP to HTTPS
* Click **Create Distribution**

⏳ Wait \~10–20 minutes to deploy

---

#### Step 3: Get CloudFront URL

* After it's deployed, you'll see a **Domain name** like:

  ```
  d12345678abcd.cloudfront.net
  ```
* Open that in your browser

✅ Now your site is secure and faster worldwide!

---

## ✅ 3. Dynamic Website using Amazon EC2 (Virtual Server)

### 📌 Goal:

Host a dynamic website using a server (e.g., PHP, Python, Node.js)

---

### 👣 Step-by-Step:

#### Step 1: Go to EC2

* Search for **EC2** in AWS
* Click **Launch Instance**

#### Step 2: Set up your instance

* Name: `MyWebServer`
* Choose AMI: Amazon Linux 2
* Instance type: `t2.micro` (free tier)
* Key pair: Create new one and **download the `.pem` file**
* Allow traffic:

  * Check **Allow HTTP traffic**
  * Check **Allow SSH traffic**

Click **Launch Instance**

---

#### Step 3: Connect to your instance

* From EC2 dashboard, click **Connect**
* Follow the instructions to SSH into your instance using your `.pem` file

---

#### Step 4: Install Web Server

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

#### Step 5: Create a Web Page

```bash
echo "<h1>Hello from EC2</h1>" | sudo tee /var/www/html/index.html
```

---

#### Step 6: Visit Your Website

* In EC2 dashboard, copy the **Public IPv4 address**
* Paste it in your browser:
  `http://<your-public-ip>`

✅ You now have a simple server-hosted website running on EC2!

---

## ✅ 4. Web App Hosting with AWS Elastic Beanstalk

### 📌 Goal:

Deploy an app (e.g., Node.js or Python) easily without managing servers.

---

### 👣 Step-by-Step:

#### Step 1: Create Your App

For example, a Node.js app:

```javascript
// app.js
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello from Elastic Beanstalk!'));
app.listen(3000);
```

* Zip your code files into `app.zip`

---

#### Step 2: Go to **Elastic Beanstalk**

* Click **Create Application**
* Name: `my-node-app`
* Platform: Node.js
* Upload your `app.zip`

---

#### Step 3: Deploy

* Beanstalk will create EC2, Load Balancer, Auto Scaling automatically
* Takes a few minutes

---

#### Step 4: Access Your App

* Once deployed, you’ll get a URL like:
  `http://my-node-app.us-east-1.elasticbeanstalk.com`

✅ Your Node.js app is now live with no server management!

---

## ✅ 5. Containerized Website using ECS + Fargate

### 📌 Goal:

Run a Docker container as a website/app without managing servers.

---

### 👣 Step-by-Step:

#### Step 1: Create a Docker App

Create a file called `Dockerfile`:

```dockerfile
FROM nginx
COPY ./index.html /usr/share/nginx/html/index.html
```

Create an `index.html`:

```html
<h1>Hello from ECS Fargate!</h1>
```

Build and test locally:

```bash
docker build -t my-ecs-app .
docker run -p 8080:80 my-ecs-app
```

---

#### Step 2: Push Image to Amazon ECR

1. Go to **ECR** → Create Repository
2. Follow the push commands AWS gives you to upload the image

---

#### Step 3: Create ECS Service (Fargate)

1. Go to **ECS** → Create Cluster → Networking Only
2. Create a Task Definition:

   * Use **Fargate**
   * Add container image from ECR
3. Launch a **Service** using that Task
4. (Optional) Attach an Application Load Balancer

---

#### Step 4: Visit Your Website

* Copy the Load Balancer DNS or public IP

✅ Your Docker-based website is now live!

---

## 🧾 Summary Table (Beginner View)

| Method                | Best For       | Tools Used      | Public Access | Difficulty |
| --------------------- | -------------- | --------------- | ------------- | ---------- |
| **S3**                | Static sites   | S3              | S3 URL        | Easy ⭐     |
| **S3 + CloudFront**   | Static + HTTPS | S3 + CloudFront | CDN URL       | Easy ⭐⭐    |
| **EC2**               | Dynamic code   | EC2 (Linux)     | Public IP     | Medium ⭐⭐  |
| **Elastic Beanstalk** | Web apps       | EB + EC2 + LB   | App URL       | Easy ⭐⭐    |
| **ECS + Fargate**     | Containers     | ECR + ECS       | Load Balancer | Medium ⭐⭐⭐ |

---

Would you like me to provide a **real working code + screenshots + video tutorial** for any one of these?
