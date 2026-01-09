🌐 Linux VM Home Lab — Ubuntu + Docker + Tailscale + NGINX + Nextcloud

A fully self‑hosted personal cloud environment running inside an Ubuntu virtual machine. This lab demonstrates secure remote access, reverse proxying, container orchestration, and private cloud hosting — perfect for showcasing modern homelab and DevOps skills.

🚀 Overview

This project runs on:

Host Machine: Physical or hypervisor-based system running the Linux VM

Ubuntu Linux VM: Base OS for Docker stack

Docker: Container runtime

Tailscale: Secure remote access via mesh VPN

NGINX Reverse Proxy: Routing and TLS termination

Nextcloud: Personal cloud server

The setup allows you to securely access your Nextcloud instance from anywhere using a Tailscale tunnel — without exposing your home network to the public internet.

🧱 Architecture

Components

Layer

Technology

Purpose

Host Machine

Linux OS

Runs the Ubuntu VM

Virtual Machine

Ubuntu Linux

Base OS for Docker stack

Container 1

Tailscale

Creates secure mesh VPN tunnel

Container 2

NGINX

Reverse proxy + HTTPS

Container 3

Nextcloud

Personal cloud server

🔐 Remote Access Flow

A remote client connects through Tailscale, joins your private mesh network, and securely reaches your Nextcloud server through NGINX inside the VM.

📁 GitHub Repo Structure

linux-vm-home-lab/
├── README.md
├── docker-compose.yml
├── .gitignore
├── .dockerignore
├── /diagrams/
│   └── network-architecture.png
├── /tailscale/
│   └── config/
├── /nginx/
│   ├── conf.d/
│   │   └── nextcloud.conf
│   └── certs/
├── /nextcloud/
│   └── data/
└── /scripts/
    └── init.sh

🐳 Docker Compose Example

version: "3.9"

services:
  tailscale:
    image: tailscale/tailscale
    container_name: tailscale
    network_mode: host
    volumes:
      - ./tailscale:/var/lib/tailscale
    cap_add:
      - NET_ADMIN
    restart: unless-stopped

  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d
      - ./nginx/certs:/etc/nginx/certs
    depends_on:
      - nextcloud
    restart: unless-stopped

  nextcloud:
    image: nextcloud
    container_name: nextcloud
    volumes:
      - ./nextcloud:/var/www/html
    restart: unless-stopped


💼 Skills Highlighted:

Virtualization

Secure networking

Docker containerization

Reverse proxying

Self‑hosted cloud services

Architecture documentation
