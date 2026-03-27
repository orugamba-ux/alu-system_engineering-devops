
# Load Balancer and Custom HTTP Header

## 📖 Overview
This directory contains scripts that configure web servers and a load balancer for improved performance and reliability.  
The scripts are written in **Bash** and are intended to run on **Ubuntu servers**.

---

## 🗂️ Files

### 1. `0-custom_http_response_header`
This script installs and configures **Nginx** with a custom HTTP response header.

- **Purpose:**  
  Adds the header `X-Served-By` to every HTTP response, showing the hostname of the server that handled the request.
  
- **Usage:**  
  ```bash
  ./0-custom_http_response_header
  curl -I http://<server-ip>
