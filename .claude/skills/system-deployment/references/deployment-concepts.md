# C4 Deployment Reference

## What is a Deployment Diagram?

Maps **logical containers** to **physical/virtual infrastructure** for a specific environment. Shows WHERE software runs, not WHAT it does.

Based on UML deployment diagrams, simplified for C4 model.

## Key Elements

### Deployment Node

Where container instances run. **Can be nested**.

| Type | Examples |
|------|----------|
| Physical | Bare metal server, network device, mobile device |
| Virtual | VM, EC2 instance, Compute Engine |
| Containerized | Docker container, Kubernetes pod |
| Execution Environment | Tomcat, IIS, Node.js runtime, JVM |
| PaaS | Heroku dyno, App Engine, Azure App Service |
| Serverless | Lambda function, Cloud Function |

### Infrastructure Node

Supporting infrastructure (not running application code):

- Load balancers (ALB, NLB, HAProxy, nginx)
- CDN (CloudFront, Cloudflare, Akamai)
- DNS (Route53, Cloud DNS)
- Firewalls, WAF
- API Gateways
- VPCs, Subnets, Security Groups
- Managed services (SQS, SNS, Pub/Sub)

### Container Instance

A running instance of a container from the container diagram.

**Important**: Show instances, not just container definitions. If you have 3 API servers, show that.

## Deployment Node Hierarchy

Typical nesting (outside → inside):

```
Cloud Provider / Data Center
  └── Region
       └── Availability Zone
            └── VPC / Network
                 └── Subnet
                      └── Compute Instance (VM, Pod)
                           └── Runtime Environment
                                └── Container Instance
```

### AWS Example

```
AWS
  └── us-east-1
       └── us-east-1a
            └── VPC (10.0.0.0/16)
                 └── Private Subnet (10.0.2.0/24)
                      └── EC2 (t3.large)
                           └── Docker
                                └── API Service
```

### Kubernetes Example

```
GCP
  └── us-central1
       └── GKE Cluster
            └── Node Pool
                 └── Node (n2-standard-4)
                      └── Pod
                           └── Container (API)
```

## Mermaid C4Deployment Syntax

```mermaid
C4Deployment
    title Deployment Diagram - System Name [Environment]

    Deployment_Node(alias, "Name", "Technology/Description") {
        %% Nested nodes
        Deployment_Node(inner, "Inner Node", "Description") {
            %% Container instances
            Container(c1, "Container Name", "Technology", "Description")
            ContainerDb(db1, "Database", "Technology", "Description")
        }
    }

    %% Relationships
    Rel(from, to, "Label", "Protocol/Port")
```

## Environment Types

Create **separate diagrams** for each environment:

| Environment | Purpose | Typical Differences |
|-------------|---------|---------------------|
| Development | Local/dev testing | Single instances, mock services |
| Staging | Pre-production validation | Production-like, smaller scale |
| Production | Live traffic | Full scale, HA, monitoring |
| DR | Disaster recovery | Standby, may be cold/warm/hot |

## What to Include

**Always include**:
- All containers from container diagram
- Deployment nodes with technology
- Instance counts and key specs
- Communication protocols and ports
- Load balancers and entry points

**Include when relevant**:
- CDN, DNS
- Security groups, firewalls
- Message brokers (if managed service)
- Caches (if managed service)

**Don't include**:
- Internal component details
- Business logic
- Detailed security policies (separate doc)
- Cost breakdowns (separate doc)

## Properties to Document

### For Deployment Nodes

| Property | Example |
|----------|---------|
| Instance type | t3.large, n2-standard-4 |
| Count | x2, x4, auto-scale 2-8 |
| OS / Runtime | Ubuntu 22.04, Amazon Linux 2023 |
| Region / Zone | us-east-1a |
| Memory / CPU | 8GB RAM, 4 vCPU |
| Storage | 100GB gp3 |

### For Databases

| Property | Example |
|----------|---------|
| Engine version | PostgreSQL 15.4 |
| Instance class | db.r6g.large |
| Storage | 500GB, gp3, 3000 IOPS |
| Multi-AZ | Yes/No |
| Replicas | 1 read replica |
| Backup | 7-day retention |

## Common Patterns

### High Availability

```
Region
  ├── AZ-1
  │    ├── Web Server (x2)
  │    └── DB Primary
  └── AZ-2
       ├── Web Server (x2)
       └── DB Standby
```

### Blue-Green Deployment

```
Load Balancer
  ├── Blue Environment (current)
  │    └── App Servers (v1.2.3)
  └── Green Environment (new)
       └── App Servers (v1.2.4)
```

### Microservices on Kubernetes

```
K8s Cluster
  └── Namespace: production
       ├── Deployment: api (3 replicas)
       ├── Deployment: worker (2 replicas)
       └── StatefulSet: cache (3 replicas)
```

## Artifacts & Configuration

Document alongside deployment:

| Artifact Type | Examples |
|---------------|----------|
| Container Images | ECR/GCR/Docker Hub URLs, tag strategy |
| Config Files | docker-compose.yml, k8s manifests, task definitions |
| Infrastructure as Code | Terraform, CloudFormation, Pulumi |
| Secrets | Secrets Manager, Vault, K8s secrets |
| CI/CD | Pipeline definitions, deployment scripts |

## Cloud Provider Icons

Use official icons in diagrams for clarity:

- **AWS**: [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/)
- **Azure**: [Azure Icons](https://docs.microsoft.com/en-us/azure/architecture/icons/)
- **GCP**: [Google Cloud Icons](https://cloud.google.com/icons)

Always include a **legend** explaining icons used.

## Relationship to Other C4 Diagrams

```
Container Diagram (Level 2)
    Shows: WHAT containers exist (logical)
    ↓ MAPS TO
Deployment Diagram (Supplementary)
    Shows: WHERE containers run (physical)
```

The deployment diagram uses the **same containers** from the container diagram, but shows their **instances** mapped to infrastructure.

## Common Mistakes

1. **Mixing environments**: One diagram per environment
2. **Missing instances**: Show actual count, not just "1"
3. **No protocols**: Always label communication with protocol/port
4. **Outdated**: Infrastructure changes fast; automate if possible
5. **Too detailed**: Keep high-level; link to IaC for details
6. **No legend**: Especially with cloud icons

## Automation Considerations

Deployment diagrams go stale quickly. Consider:

- Generating from Terraform/CloudFormation
- Syncing with cloud provider APIs
- Using Structurizr DSL with deployment model
- CI/CD validation of diagram accuracy
