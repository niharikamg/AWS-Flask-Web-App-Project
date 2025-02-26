# Deploying a Flask Web App on AWS

## Overview
This guide walks you through the process of setting up a **Flask web application** on an **AWS EC2 instance**. You'll be using **SQLite** for the database and deploying the app with **Apache and mod_wsgi**.

## What You'll Need
- An **AWS account**
- Basic knowledge of Linux commands
- Familiarity with **Flask** and **SQLite**
- A **terminal** or SSH client

---

## Step-by-Step Setup
### 1. Launch an AWS EC2 Instance
1. Log in to [AWS Console](https://aws.amazon.com/)
2. Go to **EC2 Dashboard** → **Launch Instance**
3. Choose **Ubuntu Server 24.04 LTS (Free Tier Eligible)**
4. Configure your instance:
   - **Enable inbound traffic** for **HTTP (80), HTTPS (443), and SSH (22)**
   - **Generate and download** an SSH key pair for secure access
5. Start the instance and **note down the public IP address**

### 2. Connect to Your EC2 Instance
Open your terminal and connect via SSH:
```sh
ssh -i your-key.pem ubuntu@your-ec2-ip
```

### 3. Install Necessary Packages
Once connected, install Apache, mod_wsgi, Flask, and SQLite:
```sh
sudo apt update
sudo apt install apache2 libapache2-mod-wsgi-py3 python3-pip python3-flask sqlite3 -y
```

### 4. Deploy Your Flask App
1. **Create a project directory:**
   ```sh
   mkdir -p /var/www/flaskapp && cd /var/www/flaskapp
   ```
2. **Upload your files** (e.g., `flaskapp.py`, `register.html`, `login.html`, `profile.html`)
3. **Run Flask locally to test:**
   ```sh
   python3 flaskapp.py
   ```

### 5. Configure Apache to Serve Your App
1. **Copy `flaskapp.wsgi`** to `/var/www/flaskapp/`
2. **Configure Apache:**
   ```sh
   sudo nano /etc/apache2/sites-available/flaskapp.conf
   ```
   Paste the contents of `apache_config.conf` and save the file.
3. **Enable the site and restart Apache:**
   ```sh
   sudo a2ensite flaskapp.conf
   sudo systemctl restart apache2
   ```

### 6. Access Your Web App
Once everything is set up, open **http://your-ec2-ip** in your browser to see your Flask app in action!

---

## Extra Credit: File Upload & Word Count
To take your project further, implement a **file upload feature** in `flaskapp.py`:
1. Allow users to **upload Limerick-1.txt**
2. Store and process the uploaded file
3. Display the **word count** and provide a **download option**



---

## Wrapping Up
By following this guide, you'll successfully **deploy a Flask app on AWS**, integrate an **SQLite database**, and configure **Apache with mod_wsgi**.

🚀 Happy Deploying!

