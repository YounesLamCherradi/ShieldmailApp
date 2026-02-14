# Shieldmail – Real-Time Spam and Malicious Link Detection

**Academic Team Project**  
**Institution**: ITMO University, St. Petersburg, Russia  
**Course**: Web Software Development  
**Developed by**: Student team (including Lamhamedi-Cherradi Younes)  

## Introduction

Shieldmail is a web application that detects spam content and malicious/phishing links in emails in real time. It provides accurate classification, detailed analysis, and clear insights to help users maintain online security and avoid harmful messages.

The project was developed collaboratively as a **team effort** during the **Web Software Development** course at ITMO University. It demonstrates full-stack web development practices, secure application design, real-time processing, and practical application of web technologies to cybersecurity challenges.

**Contributor**: Lamhamedi-Cherradi Younes  
**Contact**: younes@lamhamedicherradi.com
## What Does Shieldmail Do?
Shieldmail is a powerhouse at:

Swiftly catching and filtering spam content.
Hunting down malicious links to shield users.
Harnessing emoticons for rich sentiment analysis.
Breaking language barriers with multilingual support.

## Technologies Used
Shieldmail is built on a diverse and dynamic technology stack, promising a responsive, intuitive, and resilient application:

Flask: Our nimble web framework for quick deployments and scalable growth.
Python: The scripting powerhouse, enabling complex operations with graceful simplicity.
JavaScript & AJAX: For interactive user interfaces and real-time communication without page reloads.
MongoDB: Our chosen NoSQL database for storing and managing data flexibly and efficiently, ensuring that every piece of content is analyzed and processed with speed and accuracy.
Nginx & Gunicorn: Providing a sturdy serving and execution environment.
APIs: The digital synapses of interoperability, connecting our app with the expansive web ecosystem.

## How to Work with Shieldmail
Ready to dive in? Follow these steps to set up Project Name on your local machine for development and testing. We welcome code warriors, wizards of the web, and ninjas of new creations to contribute to our quest for a spam-free realm!
### Cloning the Project
First, you'll need to clone the repository to create a local copy on your computer. Fire up your terminal (or command prompt) and run the following magical spell:
textpip install gunicorn
git clone https://github.com/yourusername/yourprojectname.git
cd yourprojectname
### Cloning the Project
First, you'll need to clone the repository to create a local copy on your computer. Fire up your terminal (or command prompt) and run the following magical spell:
textpip install gunicorn
git clone https://github.com/yourusername/yourprojectname.git
cd yourprojectname
for windows users with Visual Studio code use the following comamnd to open it i nvisual studio:
textcode .
Setting Up the Environment
Before diving into the magical world of Your Project Name, let's prepare your potion brewing station (a.k.a. development environment) to ensure everything works like a charm!
## Step 1: Install Python and pip
Make sure you have Python on your machine computer). If not, visit Python's official site to download and install it.
## Step 3: Install Dependencies
With a wave of your wand, install all the necessary spells (dependencies) from the requirements.txt scroll:
in the visual code terminal enter the following command:
textpip install -r requirements.txt
## Step 4: Nginx Configuration as a Reverse Proxy
Now that your magical application is bubbling nicely in your cauldron, it's time to share it with the world! Let's set up Nginx as a protective charm (reverse proxy) to ensure that your app can handle a swarm of visitors without a hitch.
Conjuring Nginx
First, if Nginx is not already guarding your server, summon it with:
textsudo apt update
sudo apt upgrade
sudo apt install nginx
Crafting the Spell (Configuration)
textcd /etc/nginx/sites-available/
Use your favorite text editor to create a new scroll (file) named after your project:
sudo nano yourprojectname
Add the follwoing configuration:
textserver {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    location / {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
Don't forget to enable your Nginx configuration in sites-enabled:
textsudo ln -s /etc/nginx/sites-available/yourprojectname /etc/nginx/sites-enabled/
To check your Nginx configuration is working:
sudo systemctl status nginx
when makin gchanges, reload and erstart your nginx for the changes to take place:
sudo systemctl restat nginx
## Step 5: Deploying with Gunicorn 
After setting up Nginx as your reverse proxy, it’s time to conjure up Gunicorn, the Green Unicorn, to serve your Flask application to the world with grace and strength. Follow these steps to summon and configure Gunicorn.
Install Gunicorn
If you haven't already, install Gunicorn by running the following enchantment in your terminal:
textpip install gunicorn
Running Your Application with Gunicorn Navigate to your project’s root directory, where your main Flask file (e.g., app.py) is located. Cast the following spell to awaken Gunicorn and start serving your application:
textsudo gunicorn --workers=1 filename:app
if your file is app.py, instead of filename you will put app
## Step 6: Enchanting Your Application with SSL Certificates
Secure Sockets Layer (SSL) certificates are crucial for protecting your application's data during transfer over the internet. They encrypt the data sent between your server and your users' browsers, ensuring that sensitive information remains confidential and inaccessible to malicious entities. In this step, we'll guide you through the process of obtaining a free SSL certificate from Let's Encrypt and configuring Nginx to use it, adding an extra layer of security to your Shieldmail application.
### Obtain an SSL Certificate with Certbot
textsudo apt update
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
### Adjust the Nginx Configuration to Use SSL
text# Redirect HTTP traffic to HTTPS
server {
    listen 80;
    listen [::]:80;
    server_name yourdomain.com www.yourdomain.com;
    # Redirect all HTTP requests to HTTPS
    return 301 https://$server_name$request_uri;
}
server {
    # Listen on port 443 for SSL connections
    listen 443 ssl;
    listen [::]:443 ssl ipv6only=on;
    server_name yourdomain.com www.yourdomain.com;
    # SSL certificate and key paths (replace with your actual paths provided by Certbot)
    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    # Include the SSL configuration from Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
    # Your project's public directory or root, adjust if necessary
    root /var/www/yourprojectname;
    # Proxy pass configuration for the Flask application
    location / {
        proxy_pass http://localhost:8000; # Assuming Gunicorn runs on port 8000
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    access_log /var/log/nginx/yourprojectname_access.log;
    error_log /var/log/nginx/yourprojectname_error.log;
}
