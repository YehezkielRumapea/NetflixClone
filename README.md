# Netflix Clone - DevSecOps Project

Proyek DevSecOps end-to-end untuk membangun dan deploy aplikasi Netflix clone menggunakan cloud-native tools dan security best practices di AWS.

## Overview

Aplikasi Netflix clone berbasis Node.js yang di-deploy menggunakan Docker container pada AWS EC2 dengan integrasi penuh security scanning, CI/CD automation, dan real-time monitoring. Proyek ini mendemonstrasikan praktik DevSecOps modern dengan kombinasi tools development, security, dan operations.

## Arsitektur

Aplikasi ini menggunakan arsitektur tiga layer:

- **Application Layer**: Node.js app yang berjalan dalam Docker container
- **CI/CD Layer**: Jenkins pipeline untuk automated build, test, dan deployment
- **Monitoring Layer**: Prometheus dan Grafana untuk metrics collection dan visualization

Semua komponen di-host pada AWS EC2 instances dengan security groups yang terkonfigurasi untuk akses terkontrol.

## Tools & Technologies

| Component | Purpose | Port |
|-----------|---------|------|
| **AWS EC2** | Infrastructure hosting | - |
| **Docker** | Application containerization | - |
| **Jenkins** | CI/CD automation dan orchestration | 8080 |
| **SonarQube** | Static code analysis dan code quality checking | 9000 |
| **Trivy** | Container image vulnerability scanning | - |
| **OWASP Dependency-Check** | Dependency security vulnerability scanning | - |
| **Prometheus** | Metrics collection dan time-series database | 9090 |
| **Grafana** | Metrics visualization dan monitoring dashboard | 3000 |
| **Node Exporter** | System metrics exporter untuk Prometheus | 9100 |
| **Docker Hub** | Container registry untuk image storage | - |

## Key Features

### Security Integration

- **Static Code Analysis**: SonarQube melakukan analisis kualitas kode dan mendeteksi vulnerability
- **Dependency Scanning**: OWASP Dependency-Check memeriksa dependencies untuk known security issues
- **Container Scanning**: Trivy scan Docker images untuk vulnerabilities sebelum deployment
- **Quality Gates**: Pipeline otomatis fail jika tidak memenuhi security standards

### CI/CD Pipeline

Pipeline Jenkins yang terotomasi dengan stages:

1. **Clean Workspace** - Membersihkan workspace sebelum build
2. **Git Checkout** - Clone repository dari GitHub
3. **SonarQube Analysis** - Static code analysis
4. **Quality Gate Check** - Validasi quality standards
5. **OWASP Dependency Scan** - Security check untuk dependencies
6. **Docker Build** - Build container image
7. **Trivy Image Scan** - Vulnerability scan untuk Docker image
8. **Docker Push** - Push image ke Docker Hub
9. **Deploy Container** - Deploy aplikasi ke EC2 instance

### Monitoring Stack

- **Prometheus**: Mengumpulkan metrics dari EC2 instances, Jenkins, dan aplikasi
- **Grafana**: Dashboard visual untuk monitoring real-time
- **Node Exporter**: Export system metrics (CPU, memory, disk, network)
- **Pre-built Dashboards**: 
  - Node Exporter Dashboard untuk system metrics
  - Jenkins Dashboard untuk CI/CD metrics

### Email Notifications

Jenkins terintegrasi dengan Gmail SMTP untuk mengirim notifikasi:
- Build status (success/failure)
- Security scan reports
- Quality gate violations
- Deployment status

## Infrastructure Requirements

- **Jenkins Server**: AWS EC2 t2.large instance (2 vCPU, 8GB RAM)
- **Monitoring Server**: AWS EC2 t2.medium instance (2 vCPU, 4GB RAM)
- **Elastic IPs**: Untuk persistent IP addressing
- **Security Groups**: Configured untuk minimal required ports (22, 80, 443, 8080, 9000, 9090, 3000, 8081)

## Application Details

- **Tech Stack**: Node.js 16
- **API Integration**: TMDB API untuk fetch movie data
- **Containerization**: Dockerfile dengan Node.js base image
- **Deployment**: Docker container running on port 8081

## Security Best Practices

- Minimal port exposure melalui security groups
- Credentials disimpan di Jenkins Credentials Manager
- HTTPS ready untuk production deployment
- Regular automated security scanning
- Quality gates enforcement di CI/CD pipeline
- Docker user permission management untuk Jenkins

## Monitoring Capabilities

- **Infrastructure Monitoring**: CPU, memory, disk usage dari EC2 instances
- **Application Monitoring**: Container health, application metrics
- **Jenkins Monitoring**: Build statistics, job execution times
- **Alerting**: Grafana alerts untuk threshold violations

## DevSecOps Workflow

1. Developer push code ke GitHub repository
2. Jenkins automatically trigger pipeline
3. SonarQube analyze code quality dan security
4. OWASP scan dependencies untuk vulnerabilities
5. Docker build image dari source code
6. Trivy scan image untuk container vulnerabilities
7. Jika semua checks passed, push image ke Docker Hub
8. Deploy container ke EC2 instance
9. Prometheus collect metrics dari deployed application
10. Grafana visualize metrics di dashboard
11. Email notification sent untuk build status

## Cost Considerations

Proyek ini memerlukan paid AWS resources:
- t2.large instances: ~$0.09/hour
- t2.medium instances: ~$0.05/hour
- Elastic IPs: Free ketika attached
- Estimated monthly cost: $60-80 untuk continuous running

## Prerequisites

- AWS Account dengan billing enabled
- TMDB API Key (free registration)
- Docker Hub account
- Gmail account untuk notifications
- Basic knowledge tentang Linux, Docker, dan Git

## Troubleshooting Tips

- Docker permission issues: Add Jenkins user ke docker group
- SonarQube memory issues: Increase VM max map count
- Port conflicts: Check security group configurations
- Jenkins build failures: Review console output dan logs
- Monitoring gaps: Verify Prometheus targets status

## Resources

- TMDB API: Movie data provider
- Jenkins Documentation: CI/CD automation
- SonarQube Docs: Code quality platform
- Trivy Documentation: Container security scanner
- Prometheus Docs: Metrics collection
- Grafana Docs: Visualization platform

