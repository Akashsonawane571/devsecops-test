# 🔐 DevSecOps CI/CD Pipeline with Automated Security Scans

This project demonstrates a *complete DevSecOps pipeline* integrating security into every stage of CI/CD.  
It uses *OWASP Juice Shop* as a test application to run automated security checks, containerize the app, and deploy it to AWS — all triggered on each code push to GitHub.

---

## 🚀 Project Overview

Whenever a developer pushes code to the repository:
1. *Jenkins* triggers an automated pipeline.
2. Multiple *security scans* are executed:
   - *Secrets scanning* – Detect hardcoded credentials using *TruffleHog*
   - *Software Composition Analysis (SCA)* – Detect vulnerable dependencies with *OWASP Dependency-Check*
   - *Static Application Security Testing (SAST)* – Analyze source code with *SonarQube*
   - *Dynamic Application Security Testing (DAST)* – Scan the running application with *OWASP ZAP* and *Nikto*
3. Application is *built as a Docker image* and pushed to Docker Hub.
4. Image is *deployed to AWS EC2* using Docker.
5. All reports are uploaded to *DefectDojo* for centralized vulnerability tracking.

---

## 🛠 Tools & Technologies

| Category | Tool |
|----------|------|
| CI/CD | Jenkins |
| VCS | Git, GitHub |
| Secret Scanning | TruffleHog |
| SCA | OWASP Dependency-Check |
| SAST | SonarQube |
| DAST | OWASP ZAP, Nikto |
| Containerization | Docker |
| Cloud Deployment | AWS EC2 |
| Vulnerability Management | DefectDojo |

---

## 📂 Repository Structure

devsecops-test/ 
│── Jenkinsfile     # CI/CD Pipeline definition 
│── juice-shop/     # Sample application for testing 
│── README.md       # Project documentation

---

---

## ⚙ Pipeline Workflow

1. *Clone Repository* – Jenkins pulls the latest code from GitHub.
2. *Secrets Scan* – TruffleHog detects API keys, passwords, or other sensitive strings.
3. *SCA* – Dependency-Check scans project dependencies for known vulnerabilities (CVE database).
4. *SAST* – SonarQube analyzes code quality and security issues.
5. *Build* – Maven builds the project.
6. *Docker Build & Push* – Docker image is built and pushed to Docker Hub.
7. *Deploy to AWS* – EC2 instance runs the latest Docker image.
8. *DAST* – OWASP ZAP and Nikto test the live application.
9. *Upload Reports* – All findings are uploaded to DefectDojo.

---

## 📹 Demo Video Post
📌 [Watch Demo](#)

https://www.linkedin.com/posts/akash-sonawane-2a532221b_devsecops-cicd-jenkins-activity-7359938069644349440-L8x2?utm_source=share&utm_medium=member_desktop&rcm=ACoAADdmBR0Bv6OFCu3NgssXE7UEYKlpOlm-Ghs

---

## 📌 How to Run This Project

1. *Install Jenkins* with required plugins:
   - Git, Pipeline, SSH Agent, SonarQube Scanner
2. *Setup Tools*:
   - TruffleHog
   - OWASP Dependency-Check
   - SonarQube
   - Docker
   - ZAP Proxy
   - Nikto
   - DefectDojo
3. *Configure Jenkins Credentials*:
   - Docker Hub (dockerhub)
   - AWS EC2 SSH Key (ec2-ssh-key)
   - SonarQube Token (newtoken)
   - DefectDojo API Token (DEFECTDOJO_API_TOKEN)
4. *Run Pipeline* by pointing Jenkins to the Jenkinsfile in this repository.

---

## 📄 Disclaimer
This project uses *OWASP Juice Shop* only for *educational and testing purposes*.  
Do *not* run security scans against systems you don’t own or have permission to test.

---

## 👨‍💻 Author
*Akash Sonawane*  
GitHub: [Akashsonawane571](https://github.com/Akashsonawane571)  
LinkedIn: www.linkedin.com/in/akash-sonawane-2a532221b


