# Node.js Demo App - CI/CD Pipeline Project

## Project Overview

This project demonstrates a complete CI/CD (Continuous Integration and Continuous Deployment) pipeline using:

- GitHub
- GitHub Actions
- Node.js
- Docker
- DockerHub

The pipeline automatically:

1. Builds the Node.js application
2. Runs tests
3. Creates a Docker image
4. Pushes the image to DockerHub

The workflow is triggered automatically whenever code is pushed to the `main` branch.

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | Backend Application |
| Express.js | Web Framework |
| Docker | Containerization |
| GitHub | Source Code Management |
| GitHub Actions | CI/CD Automation |
| DockerHub | Docker Image Registry |

---

# Project Structure

```bash
nodejs-demo-app/
│
├── .github/
│   └── workflows/
│       └── main.yml
│
├── Screenshots/
├── node_modules/
├── .dockerignore
├── Dockerfile
├── index.js
├── package.json
├── package-lock.json
└── README.md
```

---

# Application Setup

## Clone Repository

```bash
git clone https://github.com/HarshavardhanBhosale/nodejs-demo-app.git
```

```bash
cd nodejs-demo-app
```

---

# Install Dependencies

```bash
npm install
```

---

# Run Application

```bash
npm start
```

Application runs on:

```bash
http://localhost:3000
```

---

# Docker Setup

## Build Docker Image

```bash
docker build -t nodejs-demo-app .
```

---

## Run Docker Container

```bash
docker run -d -p 3000:3000 nodejs-demo-app
```

---

# Dockerfile

```Dockerfile
FROM node:alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

# GitHub Actions Workflow

Workflow file location:

```bash
.github/workflows/main.yml
```

---

# CI/CD Pipeline Workflow

The pipeline performs the following steps automatically:

1. Checkout Source Code
2. Setup Node.js Environment
3. Install Dependencies
4. Run Tests
5. Login to DockerHub
6. Build Docker Image
7. Push Docker Image to DockerHub

---

# GitHub Actions Workflow File

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:

  build-and-deploy:

    runs-on: ubuntu-latest

    steps:

    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: 18

    - name: Install Dependencies
      run: npm install

    - name: Run Tests
      run: npm test

    - name: Login to DockerHub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build Docker Image
      run: docker build -t ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app .

    - name: Push Docker Image
      run: docker push ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app
```

---

# GitHub Secrets Configuration

Add the following secrets in GitHub:

Repository Settings → Secrets and Variables → Actions

| Secret Name | Description |
|---|---|
| DOCKER_USERNAME | DockerHub Username |
| DOCKER_PASSWORD | DockerHub Password or Access Token |

---

# Application Endpoint

```bash
GET /
```

Response:

```bash
CI/CD Pipeline Working!
```

---

# Screenshots

Add screenshots inside the `Screenshots` folder:

- GitHub Actions Pipeline
- DockerHub Repository
- Running Application
- Docker Container Output

---

# Learning Outcomes

By completing this project, I learned:

- CI/CD automation
- GitHub Actions workflow creation
- Docker containerization
- Docker image deployment
- Pipeline automation
- DevOps project structure
- Automated testing and deployment

---

# Future Improvements

- Add real unit testing using Jest
- Deploy application to AWS EC2
- Add Kubernetes deployment
- Add monitoring using Prometheus and Grafana
- Implement multi-stage Docker builds
- Add security scanning in CI pipeline

---

# Author

Harshavardhan Bhosale

---

# License

This project is licensed under the ISC License.