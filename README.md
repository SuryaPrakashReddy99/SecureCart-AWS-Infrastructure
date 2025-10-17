# SecureCart-AWS-Infrastructure
# SecureCart - Enterprise AWS Infrastructure

[AWS](https://img.shields.io/badge/AWS-Cloud-orange)(https://aws.amazon.com/)
[CloudFront](https://img.shields.io/badge/CloudFront-CDN-blue)(https://aws.amazon.com/cloudfront/)
[WAF](https://img.shields.io/badge/WAF-Security-red)(https://aws.amazon.com/waf/)
[Auto Scaling](https://img.shields.io/badge/Auto%20Scaling-Scalability-green)(https://aws.amazon.com/autoscaling/)
[License](https://img.shields.io/badge/License-MIT-yellow.svg)(LICENSE)

Project Overview

SecureCart is a production-ready, globally-distributed e-commerce platform built on AWS with enterprise-grade security, performance, and scalability features. This project demonstrates advanced cloud architecture skills and real-world infrastructure implementation.

Key Achievements
0.400s global load time** via CloudFront CDN (WebPageTest verified)
75.44% malicious traffic blocked** by AWS WAF (57 out of 70 requests)
Auto scaling** from 1-4 instances based on 70% CPU threshold
0.02s response time** through Application Load Balancer
Global reach** with 400+ CloudFront edge locations
2.43% CPU utilization** demonstrating efficient resource usage

Global Users → Route 53 DNS → CloudFront CDN → AWS WAF → ALB → Auto Scaling Group → RDS MySQL ↓ ↓ ↓ ↓ ↓ 400+ Edge Locations Security Load Dynamic Database Filtering Balance Scaling (Private)


### Infrastructure Components
- **🌐 VPC**: Custom multi-AZ network (10.0.0.0/16)
- **🖥️ EC2**: Auto Scaling Group with Amazon Linux 2023, PHP 8.4.10
- **🗄️ RDS**: MySQL 8.0.42 in private subnets with encryption
- **⚖️ ALB**: Application Load Balancer with health checks
- **🌍 CloudFront**: Global CDN with edge caching (E2CQUEUGP7QLMU)
- **🛡️ WAF**: Web Application Firewall with 4 managed rule groups
- **🌐 Route 53**: DNS management and domain routing

### Network Architecture
- **Public Subnets**: 10.0.1.0/24, 10.0.2.0/24 (ALB tier)
- **Private Subnets**: 10.0.3.0/24, 10.0.4.0/24 (App/DB tier)
- **Availability Zones**: ap-southeast-1a, ap-southeast-1b
- **Security Groups**: Defense-in-depth network security

## 📊 Performance Results

### Global CDN Performance (WebPageTest - USA)
| Metric | Result | Grade |
|--------|--------|-------|
| Time to First Byte | 0.000s | A+ |
| Start Render | 0.400s | A+ |
| Speed Index | 0.400s | A+ |
| Cumulative Layout Shift | 0 | Perfect |
| Total Blocking Time | 0.000s | A+ |
| Overall Performance | A+ | Excellent |

### Infrastructure Monitoring
| Component | Metric | Value |
|-----------|--------|-------|
| EC2 CPU | Utilization | 2.43% |
| ALB | Response Time | 0.02s |
| ALB | Active Connections | 42 |
| ALB | Data Processed | 39.4k bytes |
| ALB | Peak LCU | 20 units |

## 🛡️ Security Implementation

### AWS WAF Analytics (Real Data)
| Security Metric | Count | Percentage |
|----------------|-------|------------|
| Total Requests | 70 | 100% |
| Blocked Requests | 57 | 75.44% |
| Allowed Requests | 13 | 7.69% |
| Captcha Challenges | 0 | 0% |

### Security Features
- **OWASP Top 10 Protection**: Core Rule Set implementation
- **SQL Injection Prevention**: Advanced SQLi rule set
- **Linux OS Protection**: OS-specific exploit prevention
- **IP Reputation Filtering**: Malicious IP blocking
- **Network Segmentation**: Private subnet isolation
- **VPC Endpoints**: Secure management access

### WAF Rule Groups
1. **AWSManagedRulesCommonRuleSet** (700 capacity)
2. **AWSManagedRulesSQLiRuleSet** (200 capacity)
3. **AWSManagedRulesLinuxRuleSet** (200 capacity)
4. **AWSManagedRulesAmazonIpReputationList** (25 capacity)

## 🚀 Quick Start

### Prerequisites
- AWS CLI configured with appropriate permissions
- Domain name (optional, for custom domain setup)
- Basic understanding of AWS services

### Architecture Deployment
```bash
# Clone repository
git clone https://github.com/SuryaPrakashReddy99/SecureCart-AWS-Infrastructure.git
cd SecureCart-AWS-Infrastructure

# Deploy VPC and networking
aws cloudformation create-stack --stack-name securecart-vpc --template-body file://infrastructure/cloudformation/vpc-network.yaml

# Deploy Auto Scaling Group
aws cloudformation create-stack --stack-name securecart-asg --template-body file://infrastructure/cloudformation/ec2-autoscaling.yaml

# Deploy Application Load Balancer
aws cloudformation create-stack --stack-name securecart-alb --template-body file://infrastructure/cloudformation/alb-loadbalancer.yaml

# Deploy RDS Database
aws cloudformation create-stack --stack-name securecart-rds --template-body file://infrastructure/cloudformation/rds-database.yaml

# Deploy WAF Security
aws cloudformation create-stack --stack-name securecart-waf --template-body file://infrastructure/cloudformation/waf-security.yaml

# Deploy CloudFront CDN
aws cloudformation create-stack --stack-name securecart-cdn --template-body file://infrastructure/cloudformation/cloudfront-cdn.yaml

 Monitoring & Observability
CloudWatch Dashboards
Infrastructure Overview: CPU, memory, network metrics
Security Analytics: WAF blocked/allowed requests
Performance Metrics: Response times, throughput
Auto Scaling Events: Scaling activities and triggers
Key Performance Indicators
Availability: 99.9%+ uptime target
Response Time: <100ms target (achieved 20ms)
CPU Utilization: <70% for scaling trigger
Security: >90% attack block rate (achieved 75.44%)

export AWS_REGION=ap-southeast-1
export VPC_CIDR=10.0.0.0/16
export DOMAIN_NAME=suryainfo.life
export AUTO_SCALING_MIN=1
export AUTO_SCALING_MAX=4
export CPU_THRESHOLD=70
