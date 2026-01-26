# Deployment: Production

> **System**: Tech Registry Portal
>
> **Environment**: Production
>
> **Cloud Provider**: GitHub (Microsoft) + VPN/Internal Network
>
> **Owner**: Technology Governance Team / IT Infrastructure Team
>
> **Last Updated**: 2026-01-26

## Overview

This document describes how **Tech Registry Portal** is deployed in the **Production** environment, mapping containers to infrastructure nodes and documenting deployment artifacts.

The Tech Registry Portal leverages a **JAMstack architecture** with **GitHub as the backend infrastructure**. The static web application is hosted on GitHub Pages with global CDN, the data repository is stored in Git with GitHub API access, and the notification service runs serverless on GitHub Actions.

**Audience**: Software architects, developers, infrastructure architects, DevOps, operations/support staff.

## Environment Summary

| Attribute | Value |
|-----------|-------|
| Environment | Production |
| Region(s) | Global (GitHub Pages CDN), VPN-restricted access |
| High Availability | Yes (GitHub Pages CDN, GitHub infrastructure) |
| Auto-scaling | Yes (GitHub Pages, GitHub Actions) |
| Estimated Monthly Cost | $0 (GitHub Pages free for public repos, or included in GitHub Enterprise) |

## Deployment Diagram

```mermaid
C4Deployment
    title Deployment Diagram - Tech Registry Portal [Production]

    Deployment_Node(internal_network, "Corporate Network", "VPN/Internal Network") {
        Deployment_Node(user_device, "User Device", "Laptop/Desktop") {
            Deployment_Node(browser, "Web Browser", "Chrome/Firefox/Safari") {
                Container(spa_runtime, "Web Application (Runtime)", "Vue.js SPA", "Runs in browser, renders UI")
            }
        }
    }

    Deployment_Node(github_infrastructure, "GitHub Infrastructure", "Microsoft/GitHub Cloud") {
        Deployment_Node(github_pages_cdn, "GitHub Pages CDN", "Global CDN") {
            Container(spa_static, "Web Application (Static Assets)", "HTML/CSS/JS", "Served via CDN")
        }

        Deployment_Node(github_repo, "GitHub Repository", "Git Storage") {
            ContainerDb(data_repo, "Data Repository", "Git repo with JSON files", "Technology catalog data")
        }

        Deployment_Node(github_api_cluster, "GitHub API", "REST + GraphQL APIs") {
            Container(github_api, "GitHub API Service", "GitHub Backend", "Data access, PR management")
        }

        Deployment_Node(github_oauth_service, "GitHub OAuth", "OAuth 2.0 Provider") {
            Container(oauth, "OAuth Service", "OAuth 2.0 + PKCE", "User authentication")
        }

        Deployment_Node(github_actions, "GitHub Actions", "Serverless CI/CD") {
            Deployment_Node(actions_runner, "Actions Runner", "Ubuntu (latest)") {
                Container(notification_service, "Notification Service", "Node.js (GitHub Actions)", "Email digests, changelog")
            }
        }
    }

    Deployment_Node(internal_infra, "Internal Infrastructure", "On-Premise/Private Cloud") {
        Deployment_Node(analytics_server, "Analytics Server", "Linux VM") {
            Container(matomo, "Matomo Analytics", "PHP/MySQL", "Web analytics tracking")
        }

        Deployment_Node(vpn_gateway, "VPN Gateway", "Network Appliance") {
            Container(vpn_service, "VPN Service", "VPN/Firewall", "Network access control")
        }
    }

    Deployment_Node(email_infra, "Email Infrastructure", "Corporate SMTP") {
        Container(smtp_server, "SMTP Service", "SMTP Server", "Email delivery")
    }

    Rel(user_device, vpn_service, "Connects via VPN", "VPN protocol")
    Rel(browser, spa_static, "Loads static assets", "HTTPS/443")
    Rel(spa_runtime, github_api, "API calls (read data, create PRs)", "HTTPS REST/GraphQL")
    Rel(spa_runtime, oauth, "Authenticate user", "HTTPS OAuth 2.0")
    Rel(spa_runtime, matomo, "Send analytics events", "HTTPS")
    Rel(github_api, data_repo, "Read/write technology data", "Git protocol")
    Rel(notification_service, github_api, "Fetch PRs, commit history", "REST API")
    Rel(notification_service, data_repo, "Write changelog, read subscriptions", "Git commit")
    Rel(notification_service, smtp_server, "Send email digests", "SMTP/587")
```

## Infrastructure Overview

### Cloud Resources (GitHub Infrastructure)

| Resource | Service | Configuration | Purpose |
|----------|---------|---------------|---------|
| Static Hosting | GitHub Pages | CDN-backed, HTTPS by default | Serve static web application assets (HTML, CSS, JavaScript) |
| Data Storage | GitHub Repository | Private repository with Git storage | Store technology catalog as JSON files with version control |
| Backend API | GitHub REST/GraphQL API | Managed service, rate limits apply | Read/write data, manage Pull Requests, user authentication |
| Authentication | GitHub OAuth | OAuth 2.0 with PKCE flow | User authentication and authorization |
| Serverless Compute | GitHub Actions | Scheduled workflows + PR triggers | Run notification service for email digests and changelog |
| Schema Storage | GitHub Repository | JSON Schema files in `/schemas` directory | Store validation schemas for technology records |
| CI/CD Validation | GitHub Actions | Workflow on PR events | Validate JSON files against schemas before merge |

### Internal Resources

| Resource | Service | Configuration | Purpose |
|----------|---------|---------------|---------|
| Network Access Control | VPN Gateway | Corporate VPN + Firewall | Restrict portal access to internal network only (first security layer) |
| Web Analytics | Matomo | Self-hosted PHP/MySQL stack | Track portal usage, adoption metrics, search queries |
| Email Delivery | Corporate SMTP | SMTP server (port 587, TLS) | Deliver weekly digest emails to subscribers |

### Networking

| Component | Configuration | Purpose |
|-----------|---------------|---------|
| VPN/Internal Network | Corporate network boundary | Restrict portal access to authorized organization members |
| GitHub Pages CDN | Global CDN (GitHub infrastructure) | Deliver static assets with low latency worldwide |
| HTTPS Everywhere | TLS 1.2+ for all connections | Encrypt all data in transit |
| No Custom VPC | N/A (leveraging GitHub infrastructure) | No custom network configuration needed |

## Container to Infrastructure Mapping

| Container | Deployment Node | Instances | Configuration |
|-----------|-----------------|-----------|---------------|
| Web Application (SPA) | GitHub Pages CDN | N/A (CDN-distributed) | Static files (HTML, CSS, JS) served globally via CDN |
| Web Application (Runtime) | User's Web Browser | 1 per user session | Vue.js SPA executes in browser, OAuth token in memory |
| Data Repository | GitHub Repository | 1 (Git storage) | Private repository with JSON files, managed by GitHub |
| Notification Service | GitHub Actions Runner | 1 per workflow execution (serverless) | Node.js on Ubuntu (latest), triggered by schedule or PR merge |

## Deployment Nodes Detail

### GitHub Pages CDN

| Property | Value |
|----------|-------|
| Type | GitHub Pages (CDN-backed static hosting) |
| Build Process | GitHub Actions workflow builds Vue.js SPA, deploys to `gh-pages` branch |
| URL | `https://{org-name}.github.io/{repo-name}` (or custom domain) |
| HTTPS | Enabled by default (GitHub-provided certificate) |
| Caching | CDN caching with cache headers from build |
| Access Control | VPN/Internal Network required (enforced at DNS or network level) |

**Containers Deployed**:
- Web Application (Static Assets): HTML, CSS, JavaScript bundles from Vite build

**Build Artifacts**:
- `index.html` (SPA entry point)
- `/assets/` (JS bundles, CSS, images)
- `/schemas/` (JSON Schemas for client-side validation)

---

### User Web Browser

| Property | Value |
|----------|-------|
| Type | Client-side runtime environment |
| Supported Browsers | Chrome 90+, Firefox 88+, Safari 14+, Edge 90+ |
| JavaScript Engine | Modern ES2020+ support required |
| Local Storage | Not used for sensitive data (OAuth tokens in memory only) |
| Security | Content Security Policy (CSP) enforced by SPA |

**Containers Deployed**:
- Web Application (Runtime): Vue.js SPA with Pinia stores, VueQuery, Vue Router

**Runtime Dependencies**:
- Ajv (JSON Schema validator) - bundled in SPA
- Octokit (GitHub API client) - bundled in SPA
- Vue.js 3 runtime - bundled in SPA

---

### GitHub Repository (Data Storage)

| Property | Value |
|----------|-------|
| Type | Git repository (private) |
| Storage | GitHub-managed Git storage |
| Backup | GitHub automatic backup (99.9% SLA) |
| Version Control | Full Git commit history serves as audit trail |
| Access Control | GitHub repository permissions (read/write/merge) |
| Data Format | JSON files with frontmatter, JSON Schema definitions |

**Data Structure**:
```
/technologies/
  mongodb.json
  postgresql.json
  react.json
  ...
/schemas/
  technology.schema.json
  proposal.schema.json
  ...
/config/
  subscribers.json
  notification-settings.json
/CHANGELOG.md
```

---

### GitHub API Cluster

| Property | Value |
|----------|-------|
| Type | Managed GitHub API service |
| Endpoints | REST API v3, GraphQL API v4 |
| Rate Limits | 5,000 requests/hour (authenticated), 60 requests/hour (unauthenticated) |
| Authentication | OAuth tokens (fine-grained permissions) |
| Availability | 99.9% SLA (GitHub) |

**API Usage**:
- **REST API**: CRUD operations on repository files, Pull Request management, user profile
- **GraphQL API**: Bulk operations, efficient data fetching with custom queries

---

### GitHub OAuth Service

| Property | Value |
|----------|-------|
| Type | OAuth 2.0 Provider (GitHub-managed) |
| Flow | Authorization Code with PKCE |
| Token Storage | Client-side memory (Pinia store), never localStorage |
| Scopes Requested | `repo` (read/write repository), `user` (read user profile) |
| Token Expiration | GitHub default (no refresh tokens for public clients) |

---

### GitHub Actions Runner (Notification Service)

| Property | Value |
|----------|-------|
| Type | GitHub Actions serverless runner |
| Operating System | Ubuntu (latest) |
| Runtime | Node.js 20.x |
| Trigger | Scheduled (weekly cron), PR merge events |
| Execution Time | < 2 minutes per workflow run |
| Concurrency | 1 workflow at a time (sequential execution) |

**Containers Deployed**:
- Notification Service: Node.js scripts for changelog generation and email digests

**Workflow Schedule**:
- **PR Merge**: Triggered on `pull_request: closed` with `merged: true`
- **Weekly Digest**: Cron schedule `0 9 * * 5` (Fridays at 9 AM UTC)

---

### Matomo Analytics Server

| Property | Value |
|----------|-------|
| Type | Self-hosted analytics server |
| Operating System | Linux VM (Ubuntu/RHEL) |
| Runtime | PHP 8.x + MySQL 8.x |
| Access | Internal network only |
| Data Retention | 90 days (configurable) |

**Analytics Tracked**:
- Page views, user sessions
- Search queries (technology discovery)
- Proposal submissions
- Technology detail page views (adoption signals)

---

### VPN Gateway

| Property | Value |
|----------|-------|
| Type | Network appliance or VPN service |
| Protocol | Corporate VPN (IPsec, OpenVPN, or similar) |
| Access Control | Organization employees only |
| Integration | Portal access requires VPN connection (enforced at DNS or network level) |

---

## Infrastructure Nodes

### DNS Configuration

| Record | Type | Value | TTL | Access Control |
|--------|------|-------|-----|----------------|
| tech-registry.internal.company.com | CNAME | {org-name}.github.io | 300 | Internal DNS only (VPN required) |

### Firewall / Network Access Control

| Rule | Source | Destination | Protocol | Action |
|------|--------|-------------|----------|--------|
| Portal Access | Corporate Network (VPN) | GitHub Pages CDN | HTTPS/443 | Allow |
| Portal Access | External Networks | GitHub Pages CDN | HTTPS/443 | Deny (enforced at DNS or network level) |
| Analytics | SPA (user browser) | Matomo Server | HTTPS/443 | Allow (internal network) |
| Email Delivery | GitHub Actions | SMTP Server | SMTP/587 | Allow |

---

## Security Configuration

### Authentication & Authorization

| Aspect | Implementation |
|--------|----------------|
| User Authentication | GitHub OAuth with PKCE flow (no client secret) |
| Token Storage | Pinia store (memory only), never persisted to localStorage or cookies |
| Authorization | GitHub repository permissions (write access = submit proposals, merge access = approve proposals) |
| Session Management | OAuth token expires per GitHub defaults, user must re-authenticate |

### Secrets Management

| Secret | Storage | Rotation | Access |
|--------|---------|----------|--------|
| GitHub Actions SMTP credentials | GitHub Actions Secrets | Manual (90 days recommended) | GitHub Actions workflows only |
| GitHub OAuth Client ID | Public (embedded in SPA) | N/A (public) | Public |
| Matomo API Token | GitHub Actions Secrets (if automated analytics) | Manual | GitHub Actions workflows only |

### Content Security Policy (CSP)

Enforced by SPA `index.html` meta tag:

```html
<meta http-equiv="Content-Security-Policy" content="
  default-src 'self';
  script-src 'self';
  style-src 'self' 'unsafe-inline';
  connect-src 'self' https://api.github.com https://matomo.internal.company.com;
  img-src 'self' data: https://*.githubusercontent.com;
  font-src 'self';
">
```

### Network Security

| Layer | Protection |
|-------|------------|
| Network Access Control | VPN/Internal Network required (first security layer) |
| Transport Encryption | TLS 1.2+ for all HTTPS connections |
| GitHub API Authentication | OAuth tokens with fine-grained permissions |
| Matomo Analytics | Internal network only, no external tracking |

---

## Deployment Artifacts

### Container Images

| Container | Artifact Type | Location | Tag Strategy |
|-----------|---------------|----------|--------------|
| Web Application (SPA) | Static files | GitHub Pages branch (`gh-pages`) | Git SHA, semver tag |
| Notification Service | Node.js scripts | Repository `/notifications` directory | No separate versioning (executed from main branch) |

### Configuration Files

| File | Location | Purpose |
|------|----------|---------|
| `vite.config.ts` | `/src/vite.config.ts` | Vite build configuration, base URL, output directory |
| `notifications.yml` | `/.github/workflows/notifications.yml` | GitHub Actions workflow for notification service |
| `deploy.yml` | `/.github/workflows/deploy.yml` | GitHub Actions workflow for SPA deployment to GitHub Pages |
| `subscribers.json` | `/config/subscribers.json` | Email subscription list for weekly digests |
| `notification-settings.json` | `/config/notification-settings.json` | Email template settings, SMTP configuration |
| `technology.schema.json` | `/schemas/technology.schema.json` | JSON Schema for technology records |
| `proposal.schema.json` | `/schemas/proposal.schema.json` | JSON Schema for proposal submissions |

### Infrastructure as Code

| Tool | Location | Scope |
|------|----------|-------|
| GitHub Actions YAML | `/.github/workflows/` | CI/CD pipelines (build, test, deploy, notifications) |
| Vite Config | `/vite.config.ts` | Build configuration, base URL, plugins |
| Package.json | `/package.json` | Dependencies, build scripts, type generation scripts |

---

## CI/CD Pipeline

### Pipeline Overview

```
Code Push → Build → Test → JSON Schema Validation → Deploy to GitHub Pages
                                                   ↓
                                           Run E2E Tests → Monitor
```

### Build & Deploy Workflow

**Workflow File**: `.github/workflows/deploy.yml`

| Stage | Tool | Actions |
|-------|------|---------|
| **Checkout** | GitHub Actions | Checkout repository code |
| **Install Dependencies** | npm | Install Node.js dependencies (Vue.js, TypeScript, Vite, etc.) |
| **Generate Types** | json-schema-to-typescript | Generate TypeScript types from JSON Schemas |
| **Type Check** | TypeScript Compiler | Ensure all types are valid |
| **Lint** | ESLint | Check code quality |
| **Unit Tests** | Vitest | Run unit tests for components and composables |
| **JSON Schema Validation** | Ajv CLI | Validate all technology JSON files against schemas |
| **Build SPA** | Vite | Build production bundle (minified, tree-shaken) |
| **Deploy to GitHub Pages** | GitHub Actions | Push build artifacts to `gh-pages` branch |

### Notification Workflow

**Workflow File**: `.github/workflows/notifications.yml`

| Stage | Tool | Actions |
|-------|------|---------|
| **Trigger** | GitHub Actions | PR merge event or weekly cron schedule |
| **Checkout** | GitHub Actions | Checkout repository code |
| **Install Dependencies** | npm | Install Node.js dependencies (Octokit, Nodemailer, etc.) |
| **Generate Changelog** | Node.js Script | Fetch commits since last update, write to `CHANGELOG.md` (on PR merge) |
| **Build Digest** | Node.js Script | Fetch merged PRs from past 7 days, build HTML email (on weekly schedule) |
| **Send Email** | Nodemailer | Send email digest to subscribers via SMTP |
| **Commit Changelog** | Git | Commit updated `CHANGELOG.md` to repository (on PR merge) |

### Deployment Strategy

| Aspect | Strategy |
|--------|----------|
| Deployment Type | **Direct Push** (no staging environment) |
| Rollback | Git revert commit, redeploy previous version |
| Zero Downtime | GitHub Pages CDN handles seamless updates |
| Canary / Blue-Green | Not applicable (static site, CDN caching handles gradual rollout) |

### CI/CD Triggers

| Trigger | Workflow | Actions |
|---------|----------|---------|
| Push to `main` | `deploy.yml` | Build and deploy SPA to GitHub Pages |
| Pull Request | `deploy.yml` | Build and run tests (no deploy) |
| PR Merged to `main` | `notifications.yml` | Generate changelog, commit to repository |
| Weekly Schedule (Fridays 9 AM UTC) | `notifications.yml` | Build and send email digest |

---

## Scaling Configuration

### Static Hosting (GitHub Pages CDN)

| Aspect | Configuration |
|--------|---------------|
| Auto-scaling | Automatic (GitHub Pages CDN scales globally) |
| Capacity | Unlimited (CDN-backed) |
| Traffic Limits | GitHub Pages soft limit: 100 GB/month bandwidth, 10 builds/hour |
| Performance | Global CDN with edge caching, < 100ms latency worldwide |

### GitHub API Rate Limits

| User Type | Rate Limit | Mitigation |
|-----------|------------|------------|
| Authenticated Users | 5,000 requests/hour | VueQuery caching (5-minute staleTime), pagination to reduce requests |
| GitHub Actions | 1,000 requests/hour | Batch operations with GraphQL API to reduce request count |

### GitHub Actions Compute Limits

| Aspect | Limit | Current Usage |
|--------|-------|---------------|
| Concurrent Workflows | 20 (free tier), unlimited (Enterprise) | ~1 workflow at a time |
| Workflow Execution Time | 6 hours max | < 2 minutes per workflow (well within limits) |
| Storage for Artifacts | 500 MB (free tier) | Not applicable (no artifacts stored) |

### Notification Service

| Aspect | Configuration |
|--------|---------------|
| Execution Frequency | Weekly (Fridays 9 AM UTC) + per PR merge | Low frequency, no scaling concerns |
| Email Batch Size | Up to 1,000 subscribers per digest | Current architecture supports up to ~1,000 subscribers |
| Scalability Limit | SMTP rate limits (~1,000 emails/hour) | If exceeding 1,000 subscribers, migrate to email service provider (SendGrid, Mailgun) |

---

## Monitoring & Observability

| Aspect | Tool | Configuration | Alerts |
|--------|------|---------------|--------|
| **SPA Uptime** | GitHub Pages Status Page | Monitor GitHub Pages service status | No custom alerts (rely on GitHub status page) |
| **GitHub Actions** | GitHub Actions UI | View workflow run history, logs, success/failure | Email notification on workflow failure (GitHub default) |
| **Analytics Tracking** | Matomo | Self-hosted analytics dashboard | No real-time alerts (weekly digest reviews usage trends) |
| **API Rate Limits** | GitHub API Response Headers | Check `X-RateLimit-Remaining` header in SPA | Display warning to user if rate limit approaching |
| **JSON Schema Validation Errors** | GitHub Actions Logs | Log validation errors on PR, block merge if invalid | PR status check fails, blocks merge |

### Key Metrics

| Metric | Source | Purpose |
|--------|--------|---------|
| Page Load Time | Matomo | Monitor SPA performance |
| Search Query Volume | Matomo | Track technology discovery patterns |
| Proposal Submission Rate | GitHub API (PR count) | Measure community engagement |
| Proposal Approval Time | GitHub API (PR merge time) | Track governance workflow efficiency |
| Technology Adoption (page views) | Matomo | Identify popular technologies |
| Workflow Execution Success Rate | GitHub Actions | Monitor notification service health |
| Email Delivery Success Rate | GitHub Actions Logs | Track digest delivery |

---

## Disaster Recovery

| Aspect | Strategy | RTO | RPO |
|--------|----------|-----|-----|
| **SPA (GitHub Pages)** | Re-deploy from Git history | < 5 minutes | 0 (Git version control) |
| **Data Repository** | Git commit history (GitHub backup) | < 1 minute | 0 (Git version control, GitHub backup) |
| **GitHub API Outage** | SPA displays cached data (VueQuery cache), read-only mode | N/A (degrades gracefully) | N/A |
| **Notification Service Failure** | Retry on next workflow run (weekly digest, manual changelog update) | < 7 days (next scheduled run) | 0 (data in Git) |
| **Matomo Analytics Downtime** | Analytics tracking fails, no impact on portal functionality | N/A (non-critical) | N/A |
| **Full GitHub Outage** | No immediate recovery (dependent on GitHub infrastructure) | Dependent on GitHub | < 1 hour (GitHub backup and recovery) |

### Backup Strategy

| Component | Backup Method | Frequency | Retention |
|-----------|---------------|-----------|-----------|
| Technology Data | Git commit history + GitHub backup | Every commit | Indefinite (Git history) |
| JSON Schemas | Git commit history + GitHub backup | Every commit | Indefinite (Git history) |
| Subscription Config | Git commit history + GitHub backup | Every commit | Indefinite (Git history) |
| Matomo Analytics Data | Database backup (if configured) | Daily (recommended) | 90 days |

### Recovery Procedures

**Scenario 1: Corrupted SPA Deployment**
1. Identify last known good Git commit
2. Re-run GitHub Actions deploy workflow from that commit
3. GitHub Pages CDN serves updated build (< 5 minutes)

**Scenario 2: Accidental Data Deletion (Technology Records)**
1. Identify commit before deletion via Git history
2. Revert commit or restore files from Git history
3. Submit PR to restore data, merge to main
4. Changes live immediately (Git-backed)

**Scenario 3: GitHub Outage**
1. Monitor GitHub Status Page for updates
2. SPA degrades gracefully (shows cached data if available)
3. Wait for GitHub service restoration
4. No data loss (GitHub has enterprise-grade backup)

---

## Environment Differences

The Tech Registry Portal has a **single production environment** (no separate staging or development environments for deployment). Development and testing occur locally or in PR preview environments.

| Aspect | Local Development | PR Preview (Optional) | Production |
|--------|-------------------|----------------------|------------|
| Hosting | Local dev server (Vite) | GitHub Pages (branch preview) | GitHub Pages (main) |
| Data Source | Mock data or local JSON files | Production data (GitHub API) | Production data (GitHub API) |
| Authentication | GitHub OAuth (development app) | GitHub OAuth (production app) | GitHub OAuth (production app) |
| Analytics | Disabled or test instance | Disabled | Enabled (Matomo) |
| Network Access | No VPN required | VPN required (if preview enabled) | VPN required |
| GitHub API | Development credentials or personal tokens | Production credentials | Production credentials |
| Notification Service | Not triggered (local testing only) | Not triggered (manual testing only) | Triggered (scheduled + PR merge) |

---

## Performance Considerations

### Static Asset Delivery

| Asset Type | Optimization | Performance |
|------------|--------------|-------------|
| JavaScript Bundles | Vite code splitting, tree-shaking, minification | < 200 KB total (gzipped) |
| CSS | Vite CSS minification, scoped styles | < 50 KB total (gzipped) |
| Images | Lazy loading, modern formats (WebP) | On-demand loading |
| Fonts | Self-hosted, preloaded in HTML | < 100 KB total |

### API Performance

| Operation | Strategy | Performance |
|-----------|----------|-------------|
| Initial Data Load | VueQuery with pagination (50 items per page) | < 1 second (first page) |
| Search/Filtering | Client-side filtering on cached data | < 100ms (instant) |
| Technology Detail | VueQuery cache (5-minute staleTime) | < 500ms (cache hit: instant) |
| Proposal Submission | GitHub API PR creation (single request) | < 2 seconds |

### Caching Strategy

| Layer | Cache Type | Duration | Invalidation |
|-------|------------|----------|--------------|
| CDN | GitHub Pages CDN | Cache headers from build | New deployment clears cache |
| VueQuery | In-memory cache (browser) | 5 minutes (staleTime) | Manual refresh, new data fetch |
| Browser | HTTP caching (static assets) | 1 year (immutable assets) | Asset hash in filename forces new download |

---

## Cost Analysis

| Component | Service | Estimated Monthly Cost |
|-----------|---------|------------------------|
| GitHub Pages | Hosting (CDN) | $0 (free for public repos, or included in GitHub Enterprise) |
| GitHub API | API usage | $0 (included in GitHub plan) |
| GitHub Actions | CI/CD + Notification Service | $0 (2,000 minutes/month free tier, current usage ~200 minutes/month) |
| GitHub Repository | Storage | $0 (included in GitHub plan) |
| Matomo Analytics | Self-hosted (internal infrastructure) | Included in existing infrastructure costs |
| SMTP Server | Email delivery | Included in existing infrastructure costs |
| VPN Gateway | Network access control | Included in existing infrastructure costs |
| **Total** | | **$0** (leveraging existing GitHub and internal infrastructure) |

**Cost Scalability**:
- If GitHub Actions usage exceeds 2,000 minutes/month: ~$0.008/minute (GitHub Actions pricing)
- If subscriber count exceeds 1,000: Consider email service provider (SendGrid: ~$15/month for 5,000 emails)

---

## Related Documentation

- System Context: `../system-context.md`
- System Landscape: `../system-landscape.md`
- Container Diagram: `../system-container.md`
- Component Diagrams: `../components/web-application.md`, `../components/notification-service.md`
- Product Requirements: `../../product/product-requirement.md`
- GitHub Actions Workflows: `/.github/workflows/`
- Infrastructure Code: GitHub repository (`.github/workflows/`, `vite.config.ts`, `package.json`)
