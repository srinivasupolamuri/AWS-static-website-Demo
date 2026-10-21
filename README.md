# AWS Static Website Hosting on EC2 with Apache

## Project Overview

This project demonstrates how to host a static website on an AWS EC2
instance running Ubuntu, using Apache HTTP Server to serve the website
files over HTTP. The website was deployed to the Apache document root
and verified through the EC2 instance's public IPv4 address.

## Architecture

**Browser → EC2 public IPv4 address → AWS Security Group (HTTP/80) →
Apache → Static website files**

## Technology Stack

-   **Cloud:** AWS EC2
-   **Operating system:** Ubuntu Linux
-   **Web server:** Apache HTTP Server (`apache2`)
-   **Frontend:** HTML, CSS, JavaScript
-   **Version control:** Git and GitHub

## Screenshots

### Existing GitHub repository

<img width="1717" height="961" alt="github-repository" src="https://github.com/user-attachments/assets/d119e82a-9dea-4a1c-ad14-c1a8a63f7f8b" />

### Apache service status

The Apache service was checked with `systemctl` and showed
`active (running)`.

<img width="1407" height="917" alt="apache-service-status" src="https://github.com/user-attachments/assets/6a5c7cf6-5b69-41c2-ae06-ff4735749a40" />


### Website running in the browser

<img width="1917" height="911" alt="website-live" src="https://github.com/user-attachments/assets/915a2f71-7fac-4ff5-aadd-8a45c7662cc0" />



## Implementation

### 1. Connect to the EC2 instance

Connect to the Ubuntu instance using SSH and the private key associated
with the instance.

### 2. Install Apache

``` bash
sudo apt update
sudo apt install apache2 -y
```

### 3. Start Apache and enable it at boot

``` bash
sudo systemctl enable --now apache2
sudo systemctl status apache2
```

### 4. Deploy the website files

The Apache document root on Ubuntu is `/var/www/html`. Copy the website
files there, making sure the source directory contains the intended site
files.

``` bash
sudo cp -r ~/master/. /var/www/html/
```

If you only need to replace the home page, copy just `index.html`
instead:

``` bash
sudo cp ~/master/index.html /var/www/html/index.html
```

### 5. Configure network access

In the EC2 instance's security group, allow inbound **HTTP (TCP port
80)** from the intended client IP range. Use `0.0.0.0/0` only when the
site is meant to be publicly accessible.

### 6. Verify the website

Open the following URL in a browser, replacing the placeholder with the
instance's current public IPv4 address:

``` text
http://YOUR_EC2_PUBLIC_IP
```

Check Apache locally if needed:

``` bash
curl -I http://localhost
```

A successful response commonly includes `HTTP/1.1 200 OK`.

## Repository Structure

``` text
AWS-static-website-Demo/
├── README.md
├── index.html
├── assets/
├── images/
└── error/
```

The exact folders depend on the website template and its supporting
files.

## What I Practised

-   Installing and managing Apache on Ubuntu
-   Deploying static website files to a Linux web server
-   Accessing an EC2-hosted site through a public IPv4 address
-   Configuring inbound HTTP access with an AWS security group
-   Maintaining project files with Git and GitHub

## Possible Improvements

-   Configure HTTPS using a domain name and TLS certificate
-   Automate deployment from GitHub with a CI/CD workflow
-   Add a custom domain and DNS configuration
-   Review Apache access and error logs for troubleshooting

## Template Attribution

The deployed page shown in the screenshot uses the **Dimension**
template by [HTML5 UP](https://html5up.net/). Retain the template's
required attribution and license notices when redistributing or
modifying its files.
