# 🚀 Project 4: Production Deployment with PM2 & Nginx (AWS EC2)

## 📌 Overview

This project demonstrates how to deploy a Node.js application in a **production-ready environment** using **PM2** as a process manager and **Nginx** as a reverse proxy on an AWS EC2 instance.

It builds on earlier projects by moving from a basic development setup to a more scalable and reliable architecture used in real-world applications.

---

## 🏗️ Architecture

* **AWS EC2 (Amazon Linux)** – Hosting environment
* **Node.js Application** – Backend server running on port 3000
* **PM2** – Process manager for uptime and monitoring
* **Nginx** – Reverse proxy serving traffic on port 80

---

## 🌐 Live Application

👉 http://18.170.92.187

---

## ⚙️ What I Built

* Deployed a Node.js application on an EC2 instance
* Configured the app to run on `0.0.0.0:3000`
* Installed and configured **PM2** to:

  * Keep the app running in the background
  * Automatically restart on failure
  * Manage logs and processes
* Installed and configured **Nginx** to:

  * Listen on port 80
  * Route traffic to the Node.js app
  * Act as a reverse proxy for production setup
* Created clean routing:

  * `/` → Node.js portfolio homepage
  * `/project2` → Static Apache project page

---

## 🔧 Key Commands Used

### Start app with PM2

```bash
pm2 start app.js --name project3-app
```

### Check running processes

```bash
pm2 list
```

### View logs

```bash
pm2 logs project3-app
```

### Restart app

```bash
pm2 restart project3-app
```

### Enable PM2 on system startup

```bash
pm2 startup
pm2 save
```

---

## 🌐 Nginx Configuration

```nginx
server {
    listen 80;
    server_name _;

    location /project2/ {
        alias /usr/share/nginx/html/project2/;
        index index.html;
    }

    location = /project2 {
        return 301 /project2/;
    }

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 🔐 Security Configuration

* Opened required ports in EC2 Security Group:

  * **22 (SSH)**
  * **80 (HTTP)**
  * **3000 (for testing only)**
* Restricted access to ensure controlled exposure

---

## 📸 Screenshots (Add to GitHub)

Include the following:

* ✅ Portfolio homepage (Nginx serving Node app)
* <img width="982" height="836" alt="image" src="https://github.com/user-attachments/assets/6b668082-4678-4a86-80fe-7779159be97d" />

* ✅ PM2 process list (`pm2 list`)
* <img width="1595" height="156" alt="image" src="https://github.com/user-attachments/assets/2245b0cd-0a39-40e3-b5f3-78faec365e70" />

* ✅ Nginx status (`systemctl status nginx`)
* <img width="1576" height="396" alt="image" src="https://github.com/user-attachments/assets/89af06bb-20a9-4794-8651-bf7baecab89f" />

* ✅ Browser showing live app on port 80
* <img width="1550" height="89" alt="image" src="https://github.com/user-attachments/assets/23a51ec3-c977-4dc6-90b3-198bf61e7de3" />

---

## 🚧 Challenges Faced

* Application not accessible via public IP
* Timeout errors due to port configuration
* Nginx conflicts on port 80
* PM2 process showing as errored

---

## 🧠 What I Learned

* Difference between development and production setups
* How reverse proxies work
* Importance of port management and security groups
* How to debug deployment issues in cloud environments
* Managing Node.js apps with PM2

---

## 📈 Key Skills Demonstrated

* AWS EC2 deployment
* Linux server configuration
* Nginx reverse proxy setup
* PM2 process management
* Networking and troubleshooting
* Real-world production architecture

---

## 🎯 Project Outcome

Successfully deployed a **production-style Node.js application** using PM2 and Nginx, making it accessible via a public IP on standard HTTP port (80).

---

## 🔗 Related Projects

* **Project 1:** Static Website Hosting (S3 + CloudFront)
* **Project 2:** Apache Web Server Deployment
* **Project 3:** Node.js App Deployment (Basic)

---

## 👤 Author

**Kingsley Evans**
Cloud Engineering Portfolio Project
AWS Free Tier
