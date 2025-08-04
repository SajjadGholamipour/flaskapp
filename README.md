# 🧰 FastAPI Redis Platform

This project is a sample **DevOps platform setup** featuring a FastAPI service with Redis, deployed using **Docker Compose**. It includes a **CI/CD pipeline**, optimized Docker image, **centralized logging** using Fluent Bit and Elasticsearch, and performance considerations.





## 📐 Architecture

```text
                          +---------------------+
                          |     GitHub Repo     |
                          +---------------------+
                                    |
                                    ▼
                        +-----------------------+
                        |      GitHub Actions   |
                        |  (CI/CD: Build & Push)|
                        +-----------------------+
                                    |
                                    ▼
         ┌─────────────────────────────────────────────────────┐
         │                     Docker Compose                   │
         └─────────────────────────────────────────────────────┘
          |                      |                         |
          ▼                      ▼                         ▼
   +------------+         +------------+         +-------------------+
   |  FastAPI   | <---->  |   Redis    |         |    Fluent Bit     |
   +------------+         +------------+         +-------------------+
                                                         |
                                                         ▼
                                            +-----------------------+
                                            |     Elasticsearch     |
                                            +-----------------------+
```


---
## 📁 Project Structure

ci.yml                # GitHub Actions pipeline
main.py               # FastAPI app with Redis
requirements.txt      # Python dependencies
docker-compose.yml        # Infrastructure definition
Dockerfile                # Optimized image build
fluent-bit.conf       # Main Fluent Bit config
parsers.conf          # Parser definitions
README.md                 # You're here!





---
## 🚀 Features

🐍 FastAPI + Redis key-value API

🐳 Optimized Dockerfile using python:3.9-slim

🔁 Automated CI/CD pipeline with GitHub Actions

📦 Image pushed to GitHub Container Registry

📋 Centralized logging with Fluent Bit → Elasticsearch

📊 Ready for future integration with Kibana or Grafana




---
## 🧪 API Endpoints

GET /
- Returns the value of Redis key "example_key"
- 404 if not set

POST /write/{key}?value=xxx
- Sets a Redis key with a given value




---
## ⚙️ CI/CD Pipeline

Tool: GitHub Actions
Steps:

- Checkout code

- Log in to GHCR using GitHub Token

- Build + push Docker image using docker/build-push-action

- Trigger: on push to main branch.

- File: .github/workflows/ci-cd.yml



---
## 🐋 Docker Compose Services

services:
- web 
- redis
- fluentbit:
- elasticsearch

## 📝 Justifications
Area	                    Tool / Decision	                        Justification
App Framework	            FastAPI	                                Fast, async-ready, OpenAPI built-in
Caching	                    Redis	                                Simple, lightweight, ideal for key-value storage
Image Registry  	        GHCR                                    Native to GitHub, integrated permissions
CI/CD	                    GitHub Actions	                        Tight GitHub integration, YAML-based
Log Collection	            Fluent Bit	                            Lightweight, fluentd-compatible, Elasticsearch output plugin
Log Storage	                Elasticsearch	                        Scalable full-text search & log indexing
Dockerfile Optimization	    Slim base, minimal COPY, multi stage	Smaller image size, faster build & deploy

## 📦 Running Locally

docker-compose up -d

Check FastAPI:
curl -X POST "http://localhost:8000/write/example_key?value=hello"
curl "http://localhost:8000/"
Check Elasticsearch logs:

curl http://localhost:9200/fluentbit/_search?pretty



---
## 📚 Future Work

 Add tools like watchtower to get latest version of app's image automatically

 Add Kibana or Grafana for visual log analysis

 Add performance testing with locust or k6 or jmeter

 Use Helm + K8s instead of Docker Compose(to scale and manage high load efficiently)

 Use ArgoCD or FluxCD for GitOps

 Structured logging (JSON) for more accurate parsing

 Using Elasticsearch in cluster mode and tunning shards and replica for index in high load log management
 
 Empower log management pipeline by kafka and logstash



---
## 👤 Author
Sajjad Gholamipour
DevOps Engineer
