# 🔐 Secure File Upload with AWS Lambda, S3 & Pre-signed URLs

This project demonstrates how to securely upload files to AWS S3 using **pre-signed URLs**, a **Lambda backend**, and a **clean HTML + JS frontend** — all built within the AWS Free Tier using modern, serverless architecture.

---

## ✅ One-Line Summary

> Secure, serverless file upload using AWS Lambda and pre-signed S3 URLs.

---

## 📸 Final Demo

| Step                  |
|-----------------------|
| Upload Form Interface |
| Pre-signed URL Debug  |
| Successful Upload Log |

  <img width="1919" height="1033" alt="Screenshot 2025-07-13 222302" src="https://github.com/user-attachments/assets/a0683dce-8c9b-4848-8d21-0edb541b8635" />
  <img width="1914" height="1022" alt="Screenshot 2025-07-13 191832" src="https://github.com/user-attachments/assets/14e95855-89d4-4ef6-b5b5-0cdac48faae4" />
  <img width="1919" height="1025" alt="Screenshot 2025-07-13 192013" src="https://github.com/user-attachments/assets/18636f5e-30c0-446a-ad18-25e278661b41" />

---

## 🧱 Architecture

```
User (Browser)
    ↓
HTML + JS Form
    ↓
API Gateway (HTTP API)
    ↓
AWS Lambda
    ↓
Pre-signed URL
    ↓
S3 Bucket (uploads/)
```

---

## 🧰 Tech Stack

| Component   | Purpose                            |
|-------------|-------------------------------------|
| **S3**      | Private file storage                |
| **Lambda**  | Generate signed URLs (Python)       |
| **API Gateway** | Route frontend calls to Lambda |
| **IAM**     | Secure permissions for Lambda       |
| **HTML + JS** | Upload UI + direct S3 PUT         |

---

## 🚀 Features

- 🔐 Files are stored in a **private S3 bucket**
- 🔁 Lambda returns **pre-signed, temporary** upload links
- 🧠 Works from any frontend using JavaScript
- 🆓 100% AWS Free Tier compliant

---

## 📁 Project Structure

```
.
├── index.html        # Upload form (frontend)
├── lambda_function.py # AWS Lambda backend
├── README.md
└── Screenshots/      # Demo screenshots
```

---

## 🔧 Step-by-Step Implementation

---

### ✅ Step 1: Create a Private S3 Bucket

- Created an S3 bucket with **public access blocked**
- Example bucket: `secure-upload-demo-01`

📸 <img width="1918" height="984" alt="Screenshot 2025-07-13 182539" src="https://github.com/user-attachments/assets/d0fb2505-1bb9-4f82-ba29-49c8cb97c0f1" />


---

### ✅ Step 2: Enable CORS on the Bucket

- Under **Permissions → CORS configuration**:

📸 <img width="1919" height="978" alt="Screenshot 2025-07-13 191354" src="https://github.com/user-attachments/assets/6045f182-a231-407e-9b32-44c685b22143" />
    <img width="1919" height="974" alt="Screenshot 2025-07-13 191417" src="https://github.com/user-attachments/assets/69b09919-07d9-4931-8c58-97303b314cd3" />
    <img width="1919" height="975" alt="Screenshot 2025-07-13 191433" src="https://github.com/user-attachments/assets/41e1223d-770a-4e9f-bebd-d9b2aafec56f" />

This fixed the common CORS error:

Blocked by CORS policy: No 'Access-Control-Allow-Origin' header
---

### ✅ Step 3: Create the Lambda Function

- Runtime: **Python 3.12**
- Function name: `GenerateUploadURL`
- Added environment variable: `BUCKET_NAME = secure-upload-demo-yourname`

📸
    <img width="1919" height="978" alt="Screenshot 2025-07-13 183235" src="https://github.com/user-attachments/assets/41d0f732-5e96-4834-80d1-07c202abb42c" />
    <img width="1917" height="978" alt="Screenshot 2025-07-13 183339" src="https://github.com/user-attachments/assets/9a5e56bc-8925-4c74-8530-6c08e7036cf2" />

---

### 🔹 Lambda Code :

  <img width="797" height="948" alt="Screenshot 2025-07-13 204836" src="https://github.com/user-attachments/assets/82d43796-fc79-447f-8276-0070b3c80099" />
  <img width="675" height="312" alt="Screenshot 2025-07-13 204848" src="https://github.com/user-attachments/assets/30a12bd5-0782-4ffb-be5d-93de621bad4c" />

---

### ✅ Step 4: Give Lambda Permission to Upload

- Attached this IAM policy:

```json
{
  "Effect": "Allow",
  "Action": "s3:PutObject",
  "Resource": "arn:aws:s3:::YOUR-S3-BUCKET-NAME/uploads/*"
}
```

📸 <img width="1919" height="978" alt="Screenshot 2025-07-13 183417" src="https://github.com/user-attachments/assets/ebceaf70-1b45-447c-b62d-97f0c60792e8" />
    <img width="1919" height="977" alt="Screenshot 2025-07-13 183455" src="https://github.com/user-attachments/assets/ca67b33b-88bf-4e46-a197-8583539de9bb" />
    <img width="1919" height="976" alt="Screenshot 2025-07-13 183708" src="https://github.com/user-attachments/assets/eaf55fbf-7c5f-494e-a475-e5d2472a85e0" />
    <img width="1919" height="983" alt="Screenshot 2025-07-13 183733" src="https://github.com/user-attachments/assets/c344a744-8fba-4e52-a9d2-46f774fde759" />
    <img width="1919" height="975" alt="Screenshot 2025-07-13 183906" src="https://github.com/user-attachments/assets/f8b9fc35-9e51-40cf-a030-a24da451c4fc" />
    <img width="1919" height="980" alt="Screenshot 2025-07-13 183928" src="https://github.com/user-attachments/assets/bd2e6bb7-abe2-4e44-bded-110577ad9b2d" />

---

### ✅ Step 5: Create API Gateway (HTTP API)

- Created **HTTP API** with route:
- Integrated with Lambda
- Enabled CORS (POST, OPTIONS, *, Content-Type)

📸 <img width="1919" height="982" alt="Screenshot 2025-07-13 184018" src="https://github.com/user-attachments/assets/4caa7f99-e496-4eee-ac13-29f0f24512d3" />
    <img width="1919" height="981" alt="Screenshot 2025-07-13 184103" src="https://github.com/user-attachments/assets/36e77297-6b19-4676-9e1a-e9466a4b4456" />
    <img width="1919" height="979" alt="Screenshot 2025-07-13 184251" src="https://github.com/user-attachments/assets/84f251b6-f433-4aec-b307-8c091123e290" />
    <img width="1919" height="979" alt="Screenshot 2025-07-13 190152" src="https://github.com/user-attachments/assets/3097f44f-ab93-4829-8230-7ce0c714bff0" />
    <img width="1919" height="984" alt="Screenshot 2025-07-13 190220" src="https://github.com/user-attachments/assets/4e116863-09d7-4554-9928-784d3a8836b3" />
    <img width="1089" height="147" alt="Screenshot 2025-07-13 210116" src="https://github.com/user-attachments/assets/fe9ca3ed-851b-474a-b7b3-61c85ee1f748" />
    
---

### ✅ Step 6: Build the Frontend (`index.html`)

📸 <img width="1919" height="1033" alt="Screenshot 2025-07-13 222302" src="https://github.com/user-attachments/assets/c87d6cbd-528f-4df2-a776-d6644d417dde" />
    <img width="1919" height="1029" alt="Screenshot 2025-07-13 191513" src="https://github.com/user-attachments/assets/7cf2d28b-84b5-4bb9-b9f7-13e3837f9531" />
    <img width="1917" height="981" alt="Screenshot 2025-07-13 191625" src="https://github.com/user-attachments/assets/c0ad8d34-31dd-450b-a8d5-6525f3175f91" />

---

## 🧪 Result

- Uploads go to:
  ```
  s3://secure-upload-demo-01/uploads/filename.jpg
  ```
- Bucket is private — only **pre-signed uploads allowed**
- Lambda returns temporary signed links with 5-min expiry

---

## 🛠 Common Errors & Fixes

| Error                             | Fix                                                       |
|----------------------------------|------------------------------------------------------------|
| CORS policy block                | Add CORS config to S3 (see Step 2)                         |
| “Access Denied” on PUT           | Check IAM `PutObject` permission on Lambda role            |
| `uploadUrl` returns null         | Ensure `BUCKET_NAME` is set in Lambda env vars             |

<img width="1918" height="1035" alt="Screenshot 2025-07-13 190249" src="https://github.com/user-attachments/assets/c39c65db-4c1e-445d-8d14-43a2e2c74bcf" />
<img width="1919" height="1027" alt="Screenshot 2025-07-13 191231" src="https://github.com/user-attachments/assets/c62e77a1-b8e5-41ff-a8b1-7f5194f58ce0" />

---

## 🧑‍💻 Author

**Ujjwal Wadhai**  

🔗 [GitHub](https://github.com/Ujjwal-04) 
🔗 [LinkedIn](www.linkedin.com/in/ujjwal-wadhai)

---
