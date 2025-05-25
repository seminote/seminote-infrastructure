# 🏗️ Seminote Infrastructure

> **Infrastructure as Code (IaC) for deploying and managing the complete Seminote platform across AWS, Azure, and Google Cloud with edge computing, hybrid architecture orchestration, and automated scaling**

[![Terraform](https://img.shields.io/badge/Terraform-1.6+-purple.svg)](https://terraform.io/)
[![AWS](https://img.shields.io/badge/AWS-Multi--Service-orange.svg)](https://aws.amazon.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-1.28+-blue.svg)](https://kubernetes.io/)
[![Helm](https://img.shields.io/badge/Helm-3.x-blue.svg)](https://helm.sh/)

## 🎯 Overview

The Seminote Infrastructure repository provides comprehensive Infrastructure as Code (IaC) solutions for deploying, managing, and scaling the entire Seminote piano learning platform across multiple cloud providers with edge computing capabilities and hybrid architecture orchestration.

### 🚀 Key Features

- 🌐 **Multi-Cloud Deployment**: AWS, Azure, Google Cloud support
- ⚡ **Edge Computing**: AWS Wavelength, Azure Edge Zones, GCP Edge
- 🔄 **Hybrid Architecture**: Seamless cloud-edge integration
- 📈 **Auto-Scaling**: Dynamic resource allocation based on demand
- 🔐 **Security First**: Zero-trust networking and encryption
- 📊 **Observability**: Comprehensive monitoring and logging
- 🚀 **CI/CD Integration**: Automated deployment pipelines

## 🏗️ Architecture Overview

### Infrastructure Components

1. **Core Cloud Services**
   - Kubernetes clusters (EKS, AKS, GKE)
   - Container registries and image management
   - Load balancers and API gateways
   - Database clusters (RDS, CosmosDB, Cloud SQL)

2. **Edge Computing Infrastructure**
   - AWS Wavelength zones
   - Azure Edge Zones
   - Google Cloud Edge locations
   - Edge-to-cloud connectivity

3. **Networking & Security**
   - VPC/VNet configuration
   - Service mesh (Istio)
   - Zero-trust security policies
   - TLS/SSL certificate management

4. **Data & Storage**
   - Object storage (S3, Blob, Cloud Storage)
   - Database replication and backup
   - Data lake for analytics
   - CDN for content delivery

5. **Monitoring & Observability**
   - Prometheus and Grafana
   - Centralized logging (ELK stack)
   - Distributed tracing
   - Alert management

## 🛠️ Technology Stack

### Infrastructure as Code
- **Terraform 1.6+** - Primary IaC tool
- **CloudFormation** - AWS-specific templates
- **ARM Templates** - Azure Resource Manager
- **Deployment Manager** - Google Cloud deployment

### Container Orchestration
- **Kubernetes 1.28+** - Container orchestration
- **Helm 3.x** - Package management
- **Kustomize** - Configuration management
- **ArgoCD** - GitOps deployment

### Cloud Providers
- **AWS** - Primary cloud provider
- **Azure** - Secondary cloud and edge
- **Google Cloud** - ML services and edge
- **Multi-cloud** - Disaster recovery and redundancy

### Monitoring & Observability
- **Prometheus** - Metrics collection
- **Grafana** - Visualization and dashboards
- **Jaeger** - Distributed tracing
- **Fluentd** - Log aggregation

## 🚀 Getting Started

### Prerequisites
- Terraform 1.6+ installed
- Cloud provider CLI tools (AWS CLI, Azure CLI, gcloud)
- kubectl and helm installed
- Docker for local testing

### Initial Setup

```bash
# Clone the repository
git clone https://github.com/seminote/seminote-infrastructure.git
cd seminote-infrastructure

# Install required tools
make install-tools

# Configure cloud provider credentials
aws configure  # For AWS
az login       # For Azure
gcloud auth login  # For Google Cloud

# Initialize Terraform
terraform init

# Review and customize variables
cp terraform.tfvars.example terraform.tfvars
# Edit terraform.tfvars with your configuration

# Plan the deployment
terraform plan

# Apply the infrastructure
terraform apply
```

### Environment Configuration

```hcl
# terraform.tfvars
# Global Configuration
project_name = "seminote"
environment  = "production"
region       = "us-east-1"

# AWS Configuration
aws_account_id = "123456789012"
aws_regions = [
  "us-east-1",
  "us-west-2",
  "eu-west-1"
]

# Edge Computing
enable_edge_computing = true
wavelength_zones = [
  "us-east-1-wl1-bos-wlz-1",
  "us-west-2-wl1-las-wlz-1"
]

# Kubernetes Configuration
kubernetes_version = "1.28"
node_groups = {
  general = {
    instance_types = ["m5.large", "m5.xlarge"]
    min_size      = 2
    max_size      = 10
    desired_size  = 3
  }
  ml_workloads = {
    instance_types = ["p3.2xlarge"]
    min_size      = 0
    max_size      = 5
    desired_size  = 1
  }
}

# Database Configuration
database_config = {
  engine         = "postgres"
  engine_version = "15.4"
  instance_class = "db.r6g.large"
  multi_az       = true
  backup_retention = 7
}

# Monitoring
enable_monitoring = true
monitoring_config = {
  prometheus_retention = "30d"
  grafana_admin_password = "secure-password"
  alert_email = "alerts@seminote.com"
}
```

## 📁 Repository Structure

```
seminote-infrastructure/
├── terraform/                    # Terraform configurations
│   ├── modules/                  # Reusable Terraform modules
│   │   ├── aws/                  # AWS-specific modules
│   │   │   ├── eks/              # EKS cluster module
│   │   │   ├── rds/              # RDS database module
│   │   │   ├── wavelength/       # AWS Wavelength module
│   │   │   └── vpc/              # VPC networking module
│   │   ├── azure/                # Azure-specific modules
│   │   │   ├── aks/              # AKS cluster module
│   │   │   ├── edge-zones/       # Azure Edge Zones module
│   │   │   └── vnet/             # Virtual network module
│   │   ├── gcp/                  # Google Cloud modules
│   │   │   ├── gke/              # GKE cluster module
│   │   │   ├── edge/             # GCP Edge module
│   │   │   └── vpc/              # VPC module
│   │   └── shared/               # Cross-cloud modules
│   │       ├── monitoring/       # Monitoring stack
│   │       ├── security/         # Security policies
│   │       └── networking/       # Network configuration
│   ├── environments/             # Environment-specific configs
│   │   ├── development/          # Dev environment
│   │   ├── staging/              # Staging environment
│   │   └── production/           # Production environment
│   └── global/                   # Global resources
├── kubernetes/                   # Kubernetes manifests
│   ├── base/                     # Base configurations
│   ├── overlays/                 # Environment overlays
│   │   ├── development/
│   │   ├── staging/
│   │   └── production/
│   └── helm-charts/              # Custom Helm charts
│       ├── seminote-backend/
│       ├── seminote-realtime/
│       ├── seminote-ml/
│       └── seminote-edge/
├── cloudformation/               # AWS CloudFormation templates
├── scripts/                      # Automation scripts
│   ├── deploy.sh                 # Deployment script
│   ├── destroy.sh                # Cleanup script
│   ├── backup.sh                 # Backup script
│   └── monitoring-setup.sh       # Monitoring setup
├── docs/                         # Documentation
│   ├── architecture.md           # Architecture documentation
│   ├── deployment-guide.md       # Deployment guide
│   └── troubleshooting.md        # Troubleshooting guide
└── Makefile                      # Common tasks
```

## 🌐 Multi-Cloud Deployment

### AWS Infrastructure
```hcl
# terraform/modules/aws/main.tf
module "vpc" {
  source = "./modules/aws/vpc"

  cidr_block           = var.vpc_cidr
  availability_zones   = var.availability_zones
  enable_nat_gateway   = true
  enable_vpn_gateway   = false

  tags = local.common_tags
}

module "eks" {
  source = "./modules/aws/eks"

  cluster_name     = "${var.project_name}-${var.environment}"
  cluster_version  = var.kubernetes_version
  vpc_id          = module.vpc.vpc_id
  subnet_ids      = module.vpc.private_subnet_ids

  node_groups = var.node_groups

  tags = local.common_tags
}

module "rds" {
  source = "./modules/aws/rds"

  identifier     = "${var.project_name}-${var.environment}-db"
  engine         = var.database_config.engine
  engine_version = var.database_config.engine_version
  instance_class = var.database_config.instance_class

  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.database_subnet_ids

  tags = local.common_tags
}
```

### Azure Infrastructure
```hcl
# terraform/modules/azure/main.tf
resource "azurerm_resource_group" "main" {
  name     = "${var.project_name}-${var.environment}-rg"
  location = var.azure_region

  tags = local.common_tags
}

module "aks" {
  source = "./modules/azure/aks"

  resource_group_name = azurerm_resource_group.main.name
  location           = azurerm_resource_group.main.location
  cluster_name       = "${var.project_name}-${var.environment}-aks"

  kubernetes_version = var.kubernetes_version
  node_pools        = var.azure_node_pools

  tags = local.common_tags
}

module "edge_zones" {
  source = "./modules/azure/edge-zones"

  resource_group_name = azurerm_resource_group.main.name
  edge_zones         = var.azure_edge_zones

  tags = local.common_tags
}
```

### Google Cloud Infrastructure
```hcl
# terraform/modules/gcp/main.tf
module "gke" {
  source = "./modules/gcp/gke"

  project_id     = var.gcp_project_id
  region         = var.gcp_region
  cluster_name   = "${var.project_name}-${var.environment}-gke"

  kubernetes_version = var.kubernetes_version
  node_pools        = var.gcp_node_pools

  labels = local.common_labels
}

module "edge_locations" {
  source = "./modules/gcp/edge"

  project_id      = var.gcp_project_id
  edge_locations  = var.gcp_edge_locations

  labels = local.common_labels
}
```

## ⚡ Edge Computing Setup

### AWS Wavelength Configuration
```hcl
# terraform/modules/aws/wavelength/main.tf
resource "aws_ec2_carrier_gateway" "main" {
  vpc_id = var.vpc_id

  tags = merge(var.tags, {
    Name = "${var.project_name}-carrier-gateway"
  })
}

resource "aws_subnet" "wavelength" {
  for_each = toset(var.wavelength_zones)

  vpc_id            = var.vpc_id
  availability_zone = each.value
  cidr_block        = cidrsubnet(var.vpc_cidr, 8, index(var.wavelength_zones, each.value) + 100)

  tags = merge(var.tags, {
    Name = "${var.project_name}-wavelength-${each.value}"
    Type = "Wavelength"
  })
}

resource "aws_route_table" "wavelength" {
  for_each = aws_subnet.wavelength

  vpc_id = var.vpc_id

  route {
    cidr_block         = "0.0.0.0/0"
    carrier_gateway_id = aws_ec2_carrier_gateway.main.id
  }

  tags = merge(var.tags, {
    Name = "${var.project_name}-wavelength-rt-${each.key}"
  })
}
```

### Edge Node Deployment
```yaml
# kubernetes/base/edge-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: seminote-edge
  labels:
    app: seminote-edge
    tier: edge
spec:
  replicas: 3
  selector:
    matchLabels:
      app: seminote-edge
  template:
    metadata:
      labels:
        app: seminote-edge
        tier: edge
    spec:
      nodeSelector:
        node-type: edge
      containers:
      - name: seminote-edge
        image: seminote/edge:latest
        ports:
        - containerPort: 8080
        env:
        - name: EDGE_ZONE
          valueFrom:
            fieldRef:
              fieldPath: metadata.annotations['topology.kubernetes.io/zone']
        - name: CLOUD_ENDPOINT
          value: "https://api.seminote.com"
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
```

## 📊 Monitoring & Observability

### Prometheus Configuration
```yaml
# kubernetes/base/monitoring/prometheus.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
      evaluation_interval: 15s

    rule_files:
      - "/etc/prometheus/rules/*.yml"

    scrape_configs:
      - job_name: 'kubernetes-pods'
        kubernetes_sd_configs:
          - role: pod
        relabel_configs:
          - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
            action: keep
            regex: true
          - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
            action: replace
            target_label: __metrics_path__
            regex: (.+)

      - job_name: 'seminote-backend'
        static_configs:
          - targets: ['seminote-backend:8080']
        metrics_path: /actuator/prometheus

      - job_name: 'seminote-edge'
        kubernetes_sd_configs:
          - role: endpoints
        relabel_configs:
          - source_labels: [__meta_kubernetes_service_name]
            action: keep
            regex: seminote-edge
```

### Grafana Dashboards
```json
{
  "dashboard": {
    "title": "Seminote Platform Overview",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])",
            "legendFormat": "{{service}}"
          }
        ]
      },
      {
        "title": "Response Time",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          }
        ]
      },
      {
        "title": "Edge Latency",
        "type": "singlestat",
        "targets": [
          {
            "expr": "avg(edge_processing_latency_ms)",
            "legendFormat": "Average Latency (ms)"
          }
        ]
      }
    ]
  }
}
```

## 🔐 Security & Compliance

### Network Security
```hcl
# terraform/modules/shared/security/main.tf
resource "aws_security_group" "app_sg" {
  name_prefix = "${var.project_name}-app-"
  vpc_id      = var.vpc_id

  # Allow inbound HTTPS
  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Allow inbound HTTP (redirect to HTTPS)
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Allow all outbound traffic
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = var.tags
}

# WAF Configuration
resource "aws_wafv2_web_acl" "main" {
  name  = "${var.project_name}-waf"
  scope = "CLOUDFRONT"

  default_action {
    allow {}
  }

  rule {
    name     = "RateLimitRule"
    priority = 1

    action {
      block {}
    }

    statement {
      rate_based_statement {
        limit              = 2000
        aggregate_key_type = "IP"
      }
    }

    visibility_config {
      cloudwatch_metrics_enabled = true
      metric_name                = "RateLimitRule"
      sampled_requests_enabled   = true
    }
  }

  tags = var.tags
}
```

### SSL/TLS Configuration
```hcl
# terraform/modules/shared/security/ssl.tf
resource "aws_acm_certificate" "main" {
  domain_name               = var.domain_name
  subject_alternative_names = ["*.${var.domain_name}"]
  validation_method         = "DNS"

  lifecycle {
    create_before_destroy = true
  }

  tags = var.tags
}

resource "aws_route53_record" "cert_validation" {
  for_each = {
    for dvo in aws_acm_certificate.main.domain_validation_options : dvo.domain_name => {
      name   = dvo.resource_record_name
      record = dvo.resource_record_value
      type   = dvo.resource_record_type
    }
  }

  allow_overwrite = true
  name            = each.value.name
  records         = [each.value.record]
  ttl             = 60
  type            = each.value.type
  zone_id         = var.route53_zone_id
}
```

## 🚀 Deployment Automation

### Makefile Commands
```makefile
# Makefile
.PHONY: help install-tools plan apply destroy validate format

help: ## Show this help message
	@echo 'Usage: make [target]'
	@echo ''
	@echo 'Targets:'
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "  %-15s %s\n", $$1, $$2}' $(MAKEFILE_LIST)

install-tools: ## Install required tools
	@echo "Installing required tools..."
	@which terraform >/dev/null || (echo "Please install Terraform" && exit 1)
	@which kubectl >/dev/null || (echo "Please install kubectl" && exit 1)
	@which helm >/dev/null || (echo "Please install Helm" && exit 1)
	@echo "All tools are installed!"

validate: ## Validate Terraform configuration
	terraform validate
	terraform fmt -check

format: ## Format Terraform files
	terraform fmt -recursive

plan: validate ## Plan Terraform deployment
	terraform plan -var-file="terraform.tfvars"

apply: validate ## Apply Terraform configuration
	terraform apply -var-file="terraform.tfvars" -auto-approve

destroy: ## Destroy infrastructure
	terraform destroy -var-file="terraform.tfvars" -auto-approve

deploy-k8s: ## Deploy Kubernetes resources
	kubectl apply -k kubernetes/overlays/$(ENV)

deploy-monitoring: ## Deploy monitoring stack
	helm upgrade --install prometheus prometheus-community/kube-prometheus-stack \
		--namespace monitoring --create-namespace \
		-f kubernetes/base/monitoring/values.yaml

backup: ## Create infrastructure backup
	./scripts/backup.sh

restore: ## Restore from backup
	./scripts/restore.sh $(BACKUP_FILE)
```

### Deployment Scripts
```bash
#!/bin/bash
# scripts/deploy.sh

set -e

ENVIRONMENT=${1:-development}
REGION=${2:-us-east-1}

echo "Deploying Seminote infrastructure to $ENVIRONMENT in $REGION..."

# Validate prerequisites
if ! command -v terraform &> /dev/null; then
    echo "Terraform is required but not installed."
    exit 1
fi

if ! command -v kubectl &> /dev/null; then
    echo "kubectl is required but not installed."
    exit 1
fi

# Set up environment
export TF_VAR_environment=$ENVIRONMENT
export TF_VAR_region=$REGION

# Deploy infrastructure
echo "Deploying Terraform infrastructure..."
cd terraform/environments/$ENVIRONMENT
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars" -auto-approve

# Get cluster credentials
echo "Configuring kubectl..."
aws eks update-kubeconfig --region $REGION --name seminote-$ENVIRONMENT

# Deploy Kubernetes resources
echo "Deploying Kubernetes resources..."
cd ../../../kubernetes
kubectl apply -k overlays/$ENVIRONMENT

# Deploy monitoring
echo "Deploying monitoring stack..."
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack \
    --namespace monitoring --create-namespace \
    -f base/monitoring/values.yaml

echo "Deployment completed successfully!"
echo "Access Grafana at: https://grafana.$ENVIRONMENT.seminote.com"
echo "Access Prometheus at: https://prometheus.$ENVIRONMENT.seminote.com"
```

## 🔄 CI/CD Pipeline

### GitHub Actions Workflow
```yaml
# .github/workflows/infrastructure.yml
name: Infrastructure Deployment

on:
  push:
    branches: [main, develop]
    paths: ['terraform/**', 'kubernetes/**']
  pull_request:
    branches: [main]
    paths: ['terraform/**', 'kubernetes/**']

env:
  TF_VERSION: 1.6.0
  AWS_REGION: us-east-1

jobs:
  validate:
    name: Validate Infrastructure
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Terraform Format Check
        run: terraform fmt -check -recursive

      - name: Terraform Validate
        run: |
          cd terraform/environments/development
          terraform init -backend=false
          terraform validate

      - name: Kubernetes Manifest Validation
        run: |
          kubectl --dry-run=client apply -k kubernetes/overlays/development

  plan:
    name: Plan Infrastructure
    runs-on: ubuntu-latest
    needs: validate
    if: github.event_name == 'pull_request'
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}

      - name: Terraform Plan
        run: |
          cd terraform/environments/development
          terraform init
          terraform plan -var-file="terraform.tfvars"

  deploy-dev:
    name: Deploy to Development
    runs-on: ubuntu-latest
    needs: validate
    if: github.ref == 'refs/heads/develop'
    environment: development
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Deploy Infrastructure
        run: ./scripts/deploy.sh development

  deploy-prod:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: validate
    if: github.ref == 'refs/heads/main'
    environment: production
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Deploy Infrastructure
        run: ./scripts/deploy.sh production
```

## 🧪 Testing & Validation

### Infrastructure Tests
```bash
#!/bin/bash
# scripts/test-infrastructure.sh

set -e

ENVIRONMENT=${1:-development}

echo "Testing infrastructure for $ENVIRONMENT environment..."

# Test Kubernetes cluster connectivity
echo "Testing Kubernetes cluster..."
kubectl cluster-info
kubectl get nodes

# Test application deployments
echo "Testing application deployments..."
kubectl get deployments -A
kubectl get services -A

# Test monitoring stack
echo "Testing monitoring stack..."
kubectl get pods -n monitoring

# Test edge nodes
echo "Testing edge nodes..."
kubectl get nodes -l node-type=edge

# Performance tests
echo "Running performance tests..."
kubectl run --rm -i --tty load-test --image=busybox --restart=Never -- \
  wget -qO- http://seminote-backend.default.svc.cluster.local:8080/health

echo "All tests passed!"
```

### Terraform Tests
```hcl
# tests/terraform_test.go
package test

import (
    "testing"
    "github.com/gruntwork-io/terratest/modules/terraform"
    "github.com/stretchr/testify/assert"
)

func TestTerraformInfrastructure(t *testing.T) {
    terraformOptions := &terraform.Options{
        TerraformDir: "../terraform/environments/development",
        VarFiles:     []string{"terraform.tfvars"},
    }

    defer terraform.Destroy(t, terraformOptions)
    terraform.InitAndApply(t, terraformOptions)

    // Test VPC creation
    vpcId := terraform.Output(t, terraformOptions, "vpc_id")
    assert.NotEmpty(t, vpcId)

    // Test EKS cluster
    clusterName := terraform.Output(t, terraformOptions, "cluster_name")
    assert.Equal(t, "seminote-development", clusterName)

    // Test RDS instance
    dbEndpoint := terraform.Output(t, terraformOptions, "db_endpoint")
    assert.NotEmpty(t, dbEndpoint)
}
```

## 🤝 Contributing

This project is currently in the foundation phase. Development guidelines and contribution processes will be established as the project progresses.

### Development Workflow
```bash
# 1. Create feature branch
git checkout -b feature/new-infrastructure-component

# 2. Make changes and validate
make validate
make plan

# 3. Test changes
./scripts/test-infrastructure.sh development

# 4. Commit and push
git add .
git commit -m "feat: add new infrastructure component"
git push origin feature/new-infrastructure-component

# 5. Create pull request
# Pull request will trigger validation and planning
```

## 📄 License

Copyright © 2024-2025 Seminote. All rights reserved.

---

**Part of the Seminote Piano Learning Platform**
- 🎹 [iOS App](https://github.com/seminote/seminote-ios)
- ⚙️ [Backend Services](https://github.com/seminote/seminote-backend)
- 🌐 [Real-time Services](https://github.com/seminote/seminote-realtime)
- 🤖 [ML Services](https://github.com/seminote/seminote-ml)
- 🚀 [Edge Services](https://github.com/seminote/seminote-edge)
- 🏗️ [Infrastructure](https://github.com/seminote/seminote-infrastructure) (this repository)
- 📚 [Documentation](https://github.com/seminote/seminote-docs)
