# QuickCart Support Portal — AWS EC2 Deployment

## Project Overview

QuickCart Support Portal is a static website that demonstrates how to deploy a web application on an AWS EC2 Linux server using Apache HTTP Server and GitHub.

The portal provides sample support options for order tracking, missing items, and returns and refunds.
# QuickCart Support Portal

A responsive support portal built using HTML and CSS, with a focus on a clean, modern user experience.

## 🌐 Live Website

**[Visit QuickCart Support Portal](https://ghouse7162.github.io/project_devops/)**

## Features

- Order tracking demo page
- Missing item support page
- Returns support page
- Contact support page
- Responsive design
- Delivery-themed hero image

## Technologies Used

- HTML5
- CSS3
- Git and GitHub
- GitHub Pages for hosting

## Repository

[View the source code on GitHub](https://github.com/Ghouse7162/project_devops)

## Architecture

1. **Local development:** HTML and CSS are created and edited in VS Code.
2. **Source control:** Git tracks code changes, and GitHub stores the project repository.
3. **Cloud server:** An Ubuntu EC2 instance hosts the website.
4. **Web server:** Apache serves the website files from `/var/www/html`.
5. **Networking:** An EC2 security group allows HTTP traffic on TCP port 80.
6. **Client access:** Users access the website through the EC2 instance's public IPv4 address.

## Technologies Used

- AWS EC2
- Ubuntu Linux
- Apache HTTP Server
- HTML5 and CSS3
- Git and GitHub
- SSH
- HTTP and basic networking

## Deployment Workflow

1. Build the website locally.
2. Commit and push code changes to GitHub.
3. Connect to the EC2 instance using SSH.
4. Clone the GitHub repository onto the server.
5. Install and start Apache.
6. Copy the website files into `/var/www/html`.
7. Configure the security group to allow inbound HTTP traffic on port 80.
8. Verify the website using a browser and `curl`.

## Troubleshooting and Lessons Learned

### 1. Verify Apache

Command:

`sudo systemctl status apache2`

This checks whether the Apache service is running.

### 2. Test the local website

Command:

`curl -I http://localhost`

An HTTP `200 OK` response confirms that the local web server returned a successful response.

### 3. Check listening ports

Command:

`sudo ss -lntp | grep ':80'`

This verifies whether a process is listening on port 80.

### 4. Inspect web server logs

Commands:

`sudo tail -n 20 /var/log/apache2/access.log`

`sudo tail -n 20 /var/log/apache2/error.log`

The access log records HTTP requests and responses. The error log helps investigate server-side problems.

### 5. Understand AWS networking

- A public IPv4 address allows the instance to be addressed from outside AWS.
- An Internet Gateway and a route to it enable internet connectivity for a suitably configured public subnet.
- Security groups control permitted instance traffic.
- Network ACLs provide subnet-level traffic filtering.
- SSH uses TCP port 22; HTTP uses TCP port 80.

### 6. Test public access

Use `curl` from a separate computer to test the public IP:

`curl.exe -v --connect-timeout 8 http://PUBLIC-IP/`

Replace `PUBLIC-IP` with the instance's current public IPv4 address.

A successful HTTP response confirms that the test computer can reach the website.

## Security and Cost Notes

- Restrict SSH access to a trusted source IP rather than allowing SSH from everywhere.
- This demonstration uses HTTP, which does not encrypt traffic. HTTPS requires additional configuration.
- An EC2 instance, attached storage, and other AWS resources may incur charges. Review AWS billing and unused resources regularly.
- The public IPv4 address may change if the instance is stopped and started again.

## Current Limitations

- Static frontend only; no backend API or database.
- Support options are demonstration content, not working ticket-management features.
- HTTPS and a custom domain are not configured.

## Future Improvements

- Configure HTTPS with a domain name.
- Automate deployment from GitHub.
- Add backend APIs and persistent ticket storage.
- Add monitoring and operational alerts.
- Document resource cleanup and cost controls.

## Project Repository

GitHub: https://github.com/Ghouse7162/project_devops

## Live Demo

The public IPv4 address can change. Use the current EC2 public IPv4 address and HTTP port 80 to access the live demonstration.
