# Steps to Deploy FastAPI directly on the Server

This guide outlines the steps to deploy a FastAPI application directly on a server without Kubernetes. It includes server preparation, database setup, application deployment, process management, and securing the application with HTTPS.

### Server Preparation
[ ] Update Ubuntu packages
[ ] Install PostgreSQL server and client
[ ] Create a dedicated system user for the application
[ ] Configure firewall (UFW): allow SSH (22), HTTP (80), HTTPS (443), block all other ports by default

### Database Setup
[ ] Configure PostgreSQL (create database, user, and set permissions)
[ ] Test database connection and verify access

### Application Deployment
[ ] Clone or upload your FastAPI application code to the server
[ ] Create a Python virtual environment
[ ] Install application dependencies from requirements.txt
[ ] Configure environment variables (database URL, secrets, etc.)
[ ] Test the application runs locally

### Process Management
[ ] Install and configure a process manager (systemd service)
[ ] Create service file to manage FastAPI application lifecycle
[ ] Enable and start the service
[ ] Verify the service runs automatically on system boot

### Reverse Proxy Setup
[ ] Install and configure Nginx as reverse proxy
[ ] Create Nginx server block configuration for your domain
[ ] Configure proxy settings to forward requests to FastAPI
[ ] Test Nginx configuration and restart service

### HTTPS Configuration
[ ] Install Certbot (Let's Encrypt client)
[ ] Obtain SSL certificate for your domain
[ ] Configure automatic certificate renewal
[ ] Update Nginx configuration to redirect HTTP to HTTPS
[ ] Test HTTPS connection and SSL certificate validity