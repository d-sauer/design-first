---
name: system-deployment
description: Documenting how containers are deployed to infrastructure using C4 model deployment diagrams. Use when mapping software to physical/virtual/cloud infrastructure, documenting deployment environments (dev/staging/prod), planning infrastructure changes, capturing scaling and redundancy patterns, or documenting deployment artifacts and configurations. Shows all containers from system-container mapped to infrastructure nodes.
---

# System Deployment Skill

Create C4 model deployment diagrams to show how software containers are deployed onto infrastructure within specific environments.

## Key Concepts

**Deployment Node**: Where container instances run. Can be nested. Types:
- **Physical**: Servers, devices, data centers
- **Virtual**: VMs, IaaS (EC2, Compute Engine)
- **Containerized**: Docker, Kubernetes pods
- **Execution Environment**: App servers, database servers, IIS, JVM
- **PaaS**: Heroku, App Engine, Azure App Service

**Infrastructure Node**: Supporting infrastructure:
- Load balancers, CDNs, API gateways
- DNS services, firewalls, WAF
- VPCs, subnets, security groups

**Container Instance**: A running instance of a container from the container diagram.

**Deployment Environment**: A specific runtime context (Development, Staging, Production, DR).

## Workflow

### Step 1: Confirm Work Context

- Confirm relevant work item: `/work`
- Verify system-container documentation exists at `work/{work-item}/architecture/system-container.md`
- Identify which environment(s) to document

### Step 2: Define Environment Scope

For each environment to document:
- **Name**: Production, Staging, Development, DR, etc.
- **Purpose**: What this environment is used for
- **Differences**: How it differs from other environments

### Step 3: Identify Deployment Nodes

Map the infrastructure hierarchy:

```
Cloud Provider / Data Center
  └── Region / Availability Zone
       └── VPC / Network
            └── Subnet / Security Group
                 └── Compute (VM, Container, Serverless)
                      └── Runtime (App Server, Container Runtime)
```

For each node capture:
- **Name**: Descriptive name (e.g., "Web Server", "Primary DB")
- **Type**: Physical, VM, Container, PaaS, Serverless
- **Technology**: Specific tech (e.g., "Ubuntu 22.04", "AWS EC2 t3.large")
- **Properties**: Instance count, RAM, CPU, storage, region

### Step 4: Map Container Instances

For each container from system-container.md:
- Which deployment node(s) does it run on?
- How many instances?
- Any environment-specific configuration?

### Step 5: Document Infrastructure Nodes

Capture supporting infrastructure:
- Load balancers (ALB, NLB, nginx)
- CDN (CloudFront, Cloudflare)
- DNS (Route53, Cloud DNS)
- Firewalls, WAF, security groups
- Message brokers, caches (if managed services)

### Step 6: Map Communication Paths

Document how nodes communicate:
- Protocols (HTTPS, TCP, gRPC)
- Ports
- Network paths (internal vs external)

### Step 7: Document Artifacts & Configuration

Capture deployment artifacts:
- Container images and registries
- Configuration files and secrets management
- Infrastructure as Code references
- CI/CD pipeline references

### Step 8: Generate Output

Create documentation using template: `./templates/system-deployment.md`

Output location: `work/{work-item}/architecture/deployment/{environment}.md`

## Notation Guidelines

| Element | Representation |
|---------|----------------|
| Deployment Node | Nested boxes (can contain other nodes) |
| Infrastructure Node | Box with infrastructure icon |
| Container Instance | Box inside deployment node |
| Communication | Arrow with protocol label |
| Cloud Provider Icons | AWS/Azure/GCP icons in legend |

## Quality Checklist

- [ ] Environment is clearly named and scoped
- [ ] All containers from container diagram are mapped
- [ ] Deployment nodes show technology and properties
- [ ] Infrastructure nodes (LB, DNS, etc.) included
- [ ] Communication protocols documented
- [ ] Instance counts and scaling noted
- [ ] Artifacts and configurations documented
- [ ] Diagram has legend explaining icons
