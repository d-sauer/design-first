# Deployment: {Environment Name}

> **System**: {System Name}
> 
> **Environment**: {Production | Staging | Development | DR}
> 
> **Cloud Provider**: {AWS | Azure | GCP | On-Premise | Hybrid}
> 
> **Owner**: {DevOps/Platform Team}
> 
> **Last Updated**: {Date}

## Overview

This document describes how **{System Name}** is deployed in the **{Environment}** environment, mapping containers to infrastructure nodes and documenting deployment artifacts.

**Audience**: Software architects, developers, infrastructure architects, DevOps, operations/support staff.

## Environment Summary

| Attribute | Value |
|-----------|-------|
| Environment | {Production} |
| Region(s) | {us-east-1, eu-west-1} |
| High Availability | {Yes/No} |
| Auto-scaling | {Yes/No} |
| Estimated Monthly Cost | {$X,XXX} |

## Deployment Diagram

```mermaid
C4Deployment
    title Deployment Diagram - {System Name} [{Environment}]

    Deployment_Node(cloud, "{Cloud Provider}", "Cloud Platform") {
        Deployment_Node(region, "{Region}", "AWS Region") {
            Deployment_Node(vpc, "VPC", "10.0.0.0/16") {
                
                Deployment_Node(az1, "Availability Zone 1", "us-east-1a") {
                    Deployment_Node(web_subnet, "Public Subnet", "10.0.1.0/24") {
                        Deployment_Node(web_server, "Web Server", "EC2 t3.medium x2") {
                            Container(web_instance, "Web Application", "React SPA", "Serves UI")
                        }
                    }
                    
                    Deployment_Node(app_subnet, "Private Subnet", "10.0.2.0/24") {
                        Deployment_Node(app_server, "App Server", "ECS Fargate") {
                            Container(api_instance, "API Service", "Node.js", "REST API")
                        }
                    }
                    
                    Deployment_Node(db_subnet, "Data Subnet", "10.0.3.0/24") {
                        Deployment_Node(db_primary, "Database Primary", "RDS PostgreSQL") {
                            ContainerDb(db_instance, "Database", "PostgreSQL 15", "Primary")
                        }
                    }
                }
                
                Deployment_Node(az2, "Availability Zone 2", "us-east-1b") {
                    Deployment_Node(db_standby, "Database Standby", "RDS PostgreSQL") {
                        ContainerDb(db_replica, "Database", "PostgreSQL 15", "Read Replica")
                    }
                }
            }
        }
    }

    Deployment_Node(cdn, "CDN", "CloudFront") {
        Container(static, "Static Assets", "S3", "Images, JS, CSS")
    }

    Rel(cdn, web_server, "Routes to", "HTTPS")
    Rel(web_instance, api_instance, "API calls", "HTTPS/443")
    Rel(api_instance, db_instance, "Reads/writes", "PostgreSQL/5432")
    Rel(db_instance, db_replica, "Replicates", "PostgreSQL")
```

## Infrastructure Overview

### Cloud Resources

| Resource | Service | Configuration | Purpose |
|----------|---------|---------------|---------|
| Compute | {EC2 / ECS / EKS / Lambda} | {Instance type, count} | {Run application code} |
| Database | {RDS / Aurora / DynamoDB} | {Instance class, storage} | {Data persistence} |
| Cache | {ElastiCache Redis} | {Node type, cluster mode} | {Session/data caching} |
| Storage | {S3} | {Storage class, lifecycle} | {Static assets, backups} |
| CDN | {CloudFront} | {Price class, origins} | {Global content delivery} |
| Load Balancer | {ALB / NLB} | {Type, listeners} | {Traffic distribution} |

### Networking

| Component | Configuration | Purpose |
|-----------|---------------|---------|
| VPC | {10.0.0.0/16} | {Network isolation} |
| Public Subnets | {10.0.1.0/24, 10.0.4.0/24} | {Internet-facing resources} |
| Private Subnets | {10.0.2.0/24, 10.0.5.0/24} | {Application tier} |
| Data Subnets | {10.0.3.0/24, 10.0.6.0/24} | {Database tier} |
| NAT Gateway | {Per AZ} | {Outbound internet for private subnets} |
| Security Groups | {See Security section} | {Firewall rules} |

## Container to Infrastructure Mapping

| Container | Deployment Node | Instances | Configuration |
|-----------|-----------------|-----------|---------------|
| Web Application | {EC2 Auto Scaling Group} | {2-4} | {t3.medium, 50GB EBS} |
| API Service | {ECS Fargate} | {2-8} | {1 vCPU, 2GB RAM} |
| Background Worker | {ECS Fargate} | {1-4} | {0.5 vCPU, 1GB RAM} |
| Database | {RDS PostgreSQL} | {1 primary + 1 replica} | {db.r6g.large, 500GB gp3} |
| Cache | {ElastiCache Redis} | {2 nodes} | {cache.r6g.large} |
| Message Queue | {Amazon SQS} | {N/A (managed)} | {Standard queue} |

## Deployment Nodes Detail

### {Web Server Node}

| Property | Value |
|----------|-------|
| Type | EC2 Auto Scaling Group |
| Instance Type | t3.medium |
| AMI | Amazon Linux 2023 |
| Min/Max Instances | 2 / 4 |
| Scaling Trigger | CPU > 70% |
| Storage | 50GB gp3 EBS |
| Security Group | sg-web-public |

**Containers Deployed**:
- Web Application (nginx + React build)

---

### {Application Server Node}

| Property | Value |
|----------|-------|
| Type | ECS Fargate |
| CPU | 1 vCPU |
| Memory | 2 GB |
| Min/Max Tasks | 2 / 8 |
| Scaling Trigger | Request count |
| Platform | Linux/ARM64 |

**Containers Deployed**:
- API Service (Node.js Express)

---

### {Database Node}

| Property | Value |
|----------|-------|
| Type | RDS PostgreSQL |
| Engine Version | 15.4 |
| Instance Class | db.r6g.large |
| Storage | 500 GB gp3 |
| Multi-AZ | Yes |
| Read Replicas | 1 |
| Backup Retention | 7 days |
| Maintenance Window | Sun 03:00-04:00 UTC |

---

## Infrastructure Nodes

### Load Balancer

| Property | Value |
|----------|-------|
| Type | Application Load Balancer |
| Scheme | Internet-facing |
| Listeners | HTTPS:443 |
| Target Groups | web-tg, api-tg |
| Health Check | /health, 30s interval |
| SSL Certificate | ACM (*.example.com) |

### CDN

| Property | Value |
|----------|-------|
| Service | CloudFront |
| Origins | S3 (static), ALB (dynamic) |
| Price Class | PriceClass_100 |
| Cache Policy | CachingOptimized |
| SSL | TLS 1.2+ |

### DNS

| Record | Type | Value | TTL |
|--------|------|-------|-----|
| example.com | A | ALB alias | 300 |
| api.example.com | A | ALB alias | 300 |
| cdn.example.com | CNAME | CloudFront | 3600 |

---

## Security Configuration

### Security Groups

| Name | Inbound Rules | Outbound Rules |
|------|---------------|----------------|
| sg-alb | 443 from 0.0.0.0/0 | All to VPC |
| sg-web | 80 from sg-alb | 443 to sg-api |
| sg-api | 3000 from sg-web | 5432 to sg-db |
| sg-db | 5432 from sg-api | None |

### Secrets Management

| Secret | Storage | Rotation |
|--------|---------|----------|
| Database credentials | AWS Secrets Manager | 30 days |
| API keys | AWS Secrets Manager | Manual |
| SSL certificates | ACM | Auto-renewal |

---

## Deployment Artifacts

### Container Images

| Container | Image Repository | Tag Strategy |
|-----------|------------------|--------------|
| Web Application | {ECR: xxx.dkr.ecr.region.amazonaws.com/web} | {git SHA, semver} |
| API Service | {ECR: xxx.dkr.ecr.region.amazonaws.com/api} | {git SHA, semver} |
| Background Worker | {ECR: xxx.dkr.ecr.region.amazonaws.com/worker} | {git SHA, semver} |

### Configuration Files

| File | Location | Purpose |
|------|----------|---------|
| {docker-compose.yml} | {/deploy/docker/} | {Local development} |
| {task-definition.json} | {/deploy/ecs/} | {ECS task definition} |
| {nginx.conf} | {/deploy/nginx/} | {Web server config} |

### Infrastructure as Code

| Tool | Location | Scope |
|------|----------|-------|
| Terraform | {/infrastructure/terraform/} | {AWS resources} |
| Helm Charts | {/infrastructure/helm/} | {Kubernetes resources} |
| CloudFormation | {/infrastructure/cfn/} | {Networking, IAM} |

---

## CI/CD Pipeline

### Pipeline Overview

```
Code Push → Build → Test → Security Scan → Deploy to Staging → Integration Tests → Deploy to Production
```

### Deployment Process

| Stage | Tool | Actions |
|-------|------|---------|
| Build | {GitHub Actions} | {Build images, run unit tests} |
| Security | {Snyk / Trivy} | {Scan dependencies, container images} |
| Deploy Staging | {ArgoCD / AWS CodeDeploy} | {Deploy to staging environment} |
| Integration Test | {Postman / k6} | {API tests, load tests} |
| Deploy Production | {ArgoCD / AWS CodeDeploy} | {Blue-green deployment} |
| Rollback | {Automated} | {On health check failure} |

---

## Scaling Configuration

### Auto-scaling Rules

| Resource | Metric | Scale Out | Scale In | Cooldown |
|----------|--------|-----------|----------|----------|
| Web Servers | CPU | > 70% | < 30% | 300s |
| API Tasks | Request Count | > 1000/min | < 200/min | 60s |
| Workers | Queue Depth | > 100 messages | < 10 messages | 120s |

### Capacity Limits

| Resource | Minimum | Maximum | Current |
|----------|---------|---------|---------|
| Web Instances | 2 | 4 | 2 |
| API Tasks | 2 | 8 | 3 |
| Worker Tasks | 1 | 4 | 1 |
| Database Connections | - | 100 | ~30 |

---

## Monitoring & Observability

| Aspect | Tool | Configuration |
|--------|------|---------------|
| Metrics | {CloudWatch / Datadog} | {Custom dashboards} |
| Logging | {CloudWatch Logs / ELK} | {30-day retention} |
| Tracing | {X-Ray / Jaeger} | {Sampling 10%} |
| Alerting | {PagerDuty / Opsgenie} | {See runbooks} |

---

## Disaster Recovery

| Aspect | Strategy | RTO | RPO |
|--------|----------|-----|-----|
| Database | {Multi-AZ + Read Replica} | {< 5 min} | {< 1 min} |
| Application | {Multi-AZ Auto Scaling} | {< 2 min} | {N/A} |
| Static Assets | {S3 Cross-Region Replication} | {< 1 min} | {< 15 min} |
| Full Region Failover | {Route53 Failover} | {< 15 min} | {< 5 min} |

---

## Environment Differences

| Aspect | Development | Staging | Production |
|--------|-------------|---------|------------|
| Instance Count | 1 | 2 | 2-8 |
| Database | Single instance | Single instance | Multi-AZ |
| Cache | Local Redis | ElastiCache (1 node) | ElastiCache (2 nodes) |
| CDN | None | CloudFront | CloudFront |
| SSL | Self-signed | ACM | ACM |
| Monitoring | Basic | Full | Full + Alerting |

---

## Related Documentation

- System Context: `../system-context.md`
- Container Diagram: `../system-container.md`
- Component Diagrams: `../components/`
- Runbooks: `../runbooks/`
- Infrastructure Code: `{link to IaC repository}`
