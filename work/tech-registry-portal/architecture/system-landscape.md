# Enterprise Architecture Landscape

The Enterprise Architecture Landscape encompasses the systems and platforms that support technology governance, enterprise architecture management, and project delivery across the organization. This ecosystem enables IT professionals to discover approved technologies, architects to maintain technology standards, and leadership to govern the technology landscape effectively.

The landscape consists of three primary systems: **LeanIX** serves as the comprehensive enterprise architecture management platform, **Tech Registry Portal** provides community-facing technology discovery and collaborative governance, and the **Project Management Platform** tracks project delivery and work items across the organization.

## LeanIX (Enterprise Architecture Management)

LeanIX is the enterprise architecture management platform that maintains the comprehensive view of the organization's technology landscape, including applications, technologies, business capabilities, and their relationships.

### Capabilities
- Enterprise architecture modeling and visualization
- Technology and application portfolio management
- Business capability mapping
- Architecture roadmaps and planning
- Compliance and risk management
- Survey-based data collection from stakeholders

### Interactions

- **Tech Registry Portal**
  LeanIX serves as the authoritative source of technology data. The Tech Registry Portal deep-links to LeanIX records for detailed enterprise architecture context, but does not synchronize data bidirectionally. The portal provides a more accessible, collaborative interface for technology discovery and governance workflows.

- **Project Management Platform**
  LeanIX receives project and initiative data to understand technology roadmaps and planned changes. Projects reference architecture decisions and technology standards documented in LeanIX.

## Tech Registry Portal (Technology Governance & Discovery)

The Tech Registry Portal is a lightweight, community-facing web platform that enables IT professionals to discover approved technologies, understand technology lifecycle and governance decisions, and collaboratively propose changes to technology standards.

### Capabilities
- Technology discovery and search (greenbook/blackbook classifications)
- Technology lifecycle management with revalidation workflows
- Community-driven proposal and change management
- Governance approval workflows (standard and fast-track)
- Bulk operations for administrative efficiency
- Exception management for governance flexibility
- Web analytics and adoption tracking

### Interactions

- **LeanIX**
  The Tech Registry Portal provides deep links to LeanIX technology records for users seeking comprehensive enterprise architecture context. Technology data originates from manual entry and proposal workflows within the portal, not synchronized from LeanIX.

- **Project Management Platform**
  Projects may reference technology standards and decisions documented in the Tech Registry Portal when planning technology choices. The portal provides transparent visibility into approved and prohibited technologies to guide project teams.

- **VPN/Internal Network**
  Access to the Tech Registry Portal is secured through VPN and internal network access, ensuring only authorized organization members can view technology governance information.

## Project Management Platform (Work & Delivery Tracking)

The Project Management Platform (e.g., Jira, Azure DevOps) tracks projects, work items, sprints, and delivery across development teams and the organization.

### Capabilities
- Project and work item tracking
- Sprint and iteration planning
- Team collaboration and workflow management
- Delivery metrics and reporting
- Integration with development tools and CI/CD pipelines

### Interactions

- **LeanIX**
  Projects and initiatives logged in the Project Management Platform feed into LeanIX for architecture roadmap planning and impact analysis.

- **Tech Registry Portal**
  Development teams reference the Tech Registry Portal when making technology decisions for their projects, ensuring alignment with organizational technology standards and governance policies.

## Landscape Summary

The Enterprise Architecture Landscape supports a **top-down and bottom-up approach** to technology governance:

- **LeanIX** provides the comprehensive, strategic view for architects and leadership
- **Tech Registry Portal** offers an accessible, collaborative interface for day-to-day technology decisions and community engagement
- **Project Management Platform** tracks the execution of work and projects that leverage governed technologies

This separation allows the Tech Registry Portal to focus on **community-driven collaboration and transparency** while LeanIX maintains **comprehensive enterprise architecture management**. The two systems complement each other, with the portal providing the accessible front door to technology governance and LeanIX serving as the strategic enterprise architecture platform.
