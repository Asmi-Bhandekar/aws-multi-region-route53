# 🌎 AWS Multi-Region Website using Amazon Route 53

A highly available multi-region website deployed across **AWS Mumbai (`ap-south-1`)** and **AWS Canada Central (`ca-central-1`)**, using **Amazon Route 53 Latency-Based Routing** to direct users to the region with the lowest network latency.

---

## 🚀 Project Overview

This project demonstrates how to deploy the same website in multiple AWS regions and use **Amazon Route 53** to intelligently route incoming user requests.

### Architecture

```text
                         👤 USER
                            |
                            |
                     🌐 Amazon Route 53
                     Latency-Based Routing
                            |
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
       🇮🇳 AWS Mumbai                🇨🇦 AWS Canada
        ap-south-1                   ca-central-1
              │                           │
              ▼                           ▼
        🖥️ Amazon EC2               🖥️ Amazon EC2
              │                           │
              ▼                           ▼
        🌐 Mumbai Website            🌐 Canada Website
```

---

## ☁️ AWS Services Used

| Service                            | Purpose                                   |
| ---------------------------------- | ----------------------------------------- |
| **Amazon EC2**                     | Hosts the website in each AWS region      |
| **Amazon Route 53**                | DNS management and traffic routing        |
| **Route 53 Latency-Based Routing** | Routes users to the lowest-latency region |
| **Route 53 Health Checks**         | Monitors endpoint availability            |
| **Git & GitHub**                   | Source code management                    |
| **HTML & CSS**                     | Website development                       |

---

## 🌍 AWS Regions

### 🇮🇳 Mumbai

**Region:** `ap-south-1`

**Location:** Mumbai, India

The Mumbai EC2 instance hosts the India-region version of the website.

Directory:

```text
Mumbai/
└── index.html
```

---

### 🇨🇦 Canada

**Region:** `ca-central-1`

**Location:** Canada Central

The Canada EC2 instance hosts the Canada-region version of the website.

Directory:

```text
Canada/
└── index.html
```

---

## 📁 Repository Structure

```text
aws-multi-region-route53/
│
├── Mumbai/
│   └── index.html
│
├── Canada/
│   └── index.html
│
└── README.md
```

---

## 🔄 How Traffic Routing Works

When a user accesses the website:

```text
User
  │
  ▼
Route 53
  │
  ├── Latency to Mumbai
  │
  └── Latency to Canada
          │
          ▼
   Lowest latency region
          │
          ▼
      Amazon EC2
          │
          ▼
       Website
```

Route 53 evaluates the configured latency-based records and directs the request toward the AWS region expected to provide the lowest latency.

---

## ❤️ Health Checks

Route 53 health checks are configured for the regional endpoints.

```text
                  Route 53
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
     Mumbai EC2            Canada EC2
       Healthy               Healthy
          │                     │
          └──────────┬──────────┘
                     │
                     ▼
              Traffic Served
```

If a regional endpoint becomes unhealthy, Route 53 can stop routing traffic to that endpoint and use another healthy endpoint according to the configured routing policy.

---

## 🎨 Regional Website Design

Each region has a different visual theme so that the region serving the request can be identified immediately.

### 🇮🇳 Mumbai

```text
AWS Region: ap-south-1
Location: Mumbai
Status: ONLINE
Service: Amazon EC2
Routing: Route 53
```

Theme:

**Deep Navy + Saffron/Orange**

### 🇨🇦 Canada

```text
AWS Region: ca-central-1
Location: Canada Central
Status: ONLINE
Service: Amazon EC2
Routing: Route 53
```

Theme:

**Dark Charcoal + Canadian Red**

---

## 🛠️ Deployment Steps

### 1. Clone the repository

```bash
git clone https://github.com/Suchith-K-git/aws-multi-region-route53.git
cd aws-multi-region-route53
```

### 2. Create EC2 Instance in Mumbai

Use:

```text
Region: ap-south-1
```

Install a web server such as Nginx:

```bash
sudo apt update
sudo apt install nginx -y
```

Copy the Mumbai website:

```bash
sudo cp Mumbai/index.html /var/www/html/index.html
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

### 3. Create EC2 Instance in Canada

Switch AWS region to:

```text
ca-central-1
```

Install Nginx:

```bash
sudo apt update
sudo apt install nginx -y
```

Copy the Canada website:

```bash
sudo cp Canada/index.html /var/www/html/index.html
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

## 🌐 Configure Route 53

Create a hosted zone for your domain.

Create two records using the same domain name.

### Mumbai Record

```text
Record Name: your-domain.com
Routing Policy: Latency
Region: ap-south-1
Value: Mumbai EC2 public IP / endpoint
Health Check: Enabled
```

### Canada Record

```text
Record Name: your-domain.com
Routing Policy: Latency
Region: ca-central-1
Value: Canada EC2 public IP / endpoint
Health Check: Enabled
```

---

## 🧪 Testing

To verify that the setup is working:

### Test Mumbai

Open the Mumbai EC2 public IP:

```text
http://<MUMBAI-EC2-PUBLIC-IP>
```

You should see:

```text
🇮🇳
Mumbai Region
ap-south-1
```

### Test Canada

Open the Canada EC2 public IP:

```text
http://<CANADA-EC2-PUBLIC-IP>
```

You should see:

```text
🇨🇦
Canada Region
ca-central-1
```

### Test Route 53

Open your domain:

```text
http://your-domain.com
```

The request should be routed according to the Route 53 latency-based routing configuration.

---

## 🔐 Security Considerations

The EC2 security groups should allow only the required traffic.

Example:

```text
HTTP   → TCP 80
HTTPS  → TCP 443
SSH    → TCP 22
```

For production environments, SSH should preferably be restricted to trusted IP addresses rather than being open to the entire internet.

---

## 🎯 Key Concepts Demonstrated

* AWS Regions
* Amazon EC2
* Amazon Route 53
* Latency-Based Routing
* Route 53 Health Checks
* DNS
* Multi-Region Deployment
* High Availability
* Regional Failover
* Linux
* Nginx
* Git
* GitHub
* HTML
* CSS

---

## 📈 Future Improvements

The project can be extended with:

* 🔒 HTTPS using AWS Certificate Manager
* ⚖️ Application Load Balancer
* 🔄 Auto Scaling Groups
* 🐳 Docker containerization
* 🔧 Jenkins CI/CD pipeline
* 🏗️ Terraform Infrastructure as Code
* 📊 CloudWatch monitoring
* 🔐 AWS IAM best practices
* 🌐 CloudFront CDN
* 🗄️ Multi-region database architecture

---

## 👨‍💻 Author

**Suchith K**

DevOps Engineer | AWS | Docker | Kubernetes | Jenkins | Linux

GitHub:

https://github.com/Suchith-K-git

---

## ⭐ Project

If you find this project useful, consider giving the repository a ⭐ on GitHub.

**AWS Multi-Region Website • Route 53 • EC2 • High Availability • Latency-Based Routing**
