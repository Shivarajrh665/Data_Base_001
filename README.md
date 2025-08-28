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
