# Jenkins Free-style-project

# DevOps CI/CD Freestyle Project using Jenkins, Docker, and SonarQube

## 📌 Objective

The goal of this project is to design and implement a fully automated CI/CD pipeline using **Jenkins Freestyle Jobs**, hosted on **AWS EC2**, with **Docker** for containerization and **SonarQube** for code quality analysis. It automates build, test, analysis, and deployment to enhance development efficiency and reliability.

---

## 🧰 Tools & Technologies

| Tool       | Purpose                                |
|------------|----------------------------------------|
| GitHub     | Source code version control            |
| Docker     | Containerization of the application    |
| Jenkins    | Automate CI/CD pipeline                |
| SonarQube  | Static code analysis & quality checks  |
| Nginx      | Static file web server (frontend app)  |
| AWS EC2    | Cloud hosting platform                 |

---

## ☁️ Hosting Environment

- **Cloud Platform**: AWS EC2  
- **Instance Type**: t2.medium (2 vCPU, 4GB RAM)  
- **OS**: Ubuntu 22.04 LTS  
- **Security Group Ports Opened**:
  - `22`: SSH  
  - `8080`: Jenkins  
  - `8000`: Web Application  
  - `9000`: SonarQube  

---

## 📁 Project Structure

Jenkins-FreeStyle-Project/
├── Dockerfile
├── README.md
├── index.html
├── style.css
└── test-file

yaml
Copy
Edit

---

## ⚙️ Setup & Installation

### 1. Install Docker
```bash
sudo apt update
sudo apt install docker.io -y
sudo usermod -aG docker $USER && newgrp docker
2. Install SonarQube (Dockerized)
bash
Copy
Edit
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community
3. Install Java & Jenkins
bash
Copy
Edit
sudo apt update -y
sudo apt install openjdk-17-jre openjdk-17-jdk -y
java --version

# Add Jenkins key and repo
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update -y
sudo apt-get install jenkins -y
🐳 Docker: Build & Push Image
Dockerfile (Frontend)
dockerfile
Copy
Edit
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY . .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
Build & Push
bash
Copy
Edit
docker build -t freestyle .
docker tag freestyle:latest ghanshyamramole/freestyle:v1
docker push ghanshyamramole/freestyle:v1
🔍 SonarQube Setup
Access SonarQube at http://<EC2-PUBLIC-IP>:9000

Create a project manually

Select Jenkins as CI agent

Copy project key

Create auth token for Jenkins integration

🤖 Jenkins Freestyle Job Configuration
Job Type: Freestyle Project

Source Code Management:

Git Repo URL & branch

Add Git credentials

Build Triggers:

GitHub hook trigger for GITScm polling

Build Steps:

SonarQube Analysis using scanner with project key

Execute Shell:

bash
Copy
Edit
docker run -d --name freestyle -p 8000:80 ghanshyamramole/freestyle:v1
✅ Output Validation
Access App:
bash
Copy
Edit
curl http://<EC2-PUBLIC-IP>:8000
Jenkins Output Console:
Clone → Build → Sonar Analysis → Docker Push → Deploy

🔗 Links
GitHub Repo: Jenkins Freestyle Project

DockerHub: ghanshyamramole/freestyle

LinkedIn: Ghanshyam Ramole

📘 Conclusion
This project demonstrates a real-world DevOps pipeline integrating Jenkins, Docker, and SonarQube to automate the CI/CD process. Hosted on AWS EC2, it ensures scalable deployment, consistent environments, and continuous code quality monitoring.
