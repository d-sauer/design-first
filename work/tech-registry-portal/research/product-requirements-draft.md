# Product Requirements - Draft

Use this document to capture your initial ideas about the Tech Registry Portal before moving to the full product requirements document.

## Step 1: Define the Problem

### 1. What are you building?

**Initial Answer:** A technology repository web portal for managing organizational technology governance and collaboration. The portal enables broader organization to understand the direction of used technologies, manage approved (greenbook) and prohibited (blackbook) technologies, facilitate collaboration on technology proposals, and empower teams to learn about the technology landscape.

**Expand on this:**

- I want to solve a problem of communicating what technologies are allowed to be uses, and what not.
- As well which technologies changes direction of usage and are not obsolete.
- Where today we have this in internal tool LeanIX, but there is no strong emphasis on colaboration where other people can
  propose changes, which will be review by admin. also there is no way to propose changes or new records.
- Also there is no landing pages where news could be added

### 2. Who is it for?

**Consider:**

- Who are your target users/audience?
  Everyone in the IT across all local entities, and central/HQ entity.
- What are their pain points?
  Unclear where to find which technologies they are allowed to use and what are the restrictions.
- What roles will use this portal? (e.g., developers, architects, leadership, etc.)
  This will be used by developers, architects, IT leaders/directors.
- When and where would they use this product?
  They would use it when there is new project and they need to know what technologies they can utilse.
  As well when they deal with obsolescence of application, to understnad which technology is considered obsolete and due to that application should be decomisioned and replaced.
- How frequently would different user types interact with it?
  Engineering teams on weekly basis, leaders on monthly or quarterly basis.

### 3. How do we measure success?

**Define quantifiable outcomes:**

- What metrics indicate the portal is successful?
  Amount of users accessing it on weekly/monthly basis.
  Frequency of new technologies, or proposed changes, as community activities.
- How will you measure adoption?
  By amount of usage and traffic on the web page.
  By noticing change in environment on used and decomissioned technologiws based on current standards.
- What key performance indicators (KPIs) matter?
- What does success look like in 6 months? 1 year?
  IN 6 months, we have 10% of total employees using it. In 1y we have 30% adoption.
  Year after we notice shift in technology choices being more aligned with standards.

## Step 2: Capabilities and Functional Decomposition

### 1. High-Level Capability Domains

**Your capability domains:**

- Technology Catalog Management (greenbook, black book)
- Proposals review (new and update of technology records)
  - Governance & Approval Workflows
- Search & Discovery
- News Landing Page
  - To describe current news around technologies, and to highlight certain elements to pay attention to.

### 2. Main User Flow

**Map out the step-by-step experience for key scenarios:**

**Your main user flows:**

- User Open portal → Browse technologies → View details → Make your call
- User Open portal → Browse technologies → View details → Propose change → Submit for review
- Admin Open portal → Browse Proposals → View details → Propose next step → Approve/Disaprove
- Admin Open portal → Browse technologies → Management of selected technologies → Make bulk changes
- Admin Open portal → Browse technologies with expiration date → Management of selected technologies → Start process of revalidation for bulk
- Admin Open portal → Management → List active work items for revalidation → Continue process of revalidation for bulk
- Admin Open portal → Find Technology → View details → Note exception

### 3. Must-Have Capabilities (MVP)

**Which capabilities are must-have for the first version?**

- Technology Discovery & Search
- Technology Lifecycle Management
- Proposal & Change Management
- Bulk Operations
- Exception Management
- Web Analytics & Monitoring
- Governance & Approval Workflows

**Which capabilities are good-to-have (future)?**

- Notifications & Subscriptions
- AI Chat Interface
- News & Announcements

### 4. Capability Details

#### Capability: Technology Discovery & Search

- **Description:** Enable users to find and explore technologies in the catalog using search and filtering.
- **Inputs:** Search query, filter criteria (status, category, lifecycle stage, approval status, greenbook, blackbook)
- **Outputs:** Filtered list of technologies with key metadata, detailed technology view
- **Behavior:** Full-text search across technology names and descriptions; filter by greenbook/blackbook status, lifecycle stage, and ownership; sorting by relevance, name, date or technology category.

#### Capability: Technology Lifecycle Management

- **Description:** Track and manage the complete lifecycle of technologies from introduction through deprecation.
- **Inputs:** Technology record with status, dates, lifecycle stage, owner, classification
- **Outputs:** Technology catalog with lifecycle visibility, status reports, expiration alerts
- **Behavior:** Display lifecycle stages (active, deprecating, deprecated); track approval dates and expiration dates; highlight technologies requiring revalidation; manage lifecycle transitions

#### Capability: Proposal & Change Management

- **Description:** Allow users to submit proposals for new technologies or changes to existing records that are reviewed by administrators.
- **Inputs:** Proposal form with technology details, change rationale, submitter information
- **Outputs:** GitHub pull request, proposal status updates, change history
- **Behavior:** Submit proposals via form → creates GitHub PR; track proposal status (draft, submitted, under review, approved, rejected); maintain version history; allow comments/feedback

#### Capability: Bulk Operations

- **Description:** Enable administrators to perform batch operations on multiple technologies efficiently.
- **Inputs:** Selected technology records, operation type (edit, status change, revalidation), new values
- **Outputs:** Updated technology records, operation audit log
- **Behavior:** Bulk select technologies by criteria; apply consistent updates across multiple records; trigger revalidation workflows for expiring technologies; maintain audit trail of all bulk changes

#### Capability: Exception Management

- **Description:** Record and track exceptions for technologies approved to be used outside standard governance policies.
- **Inputs:** Technology record, exception rationale, exception end date, approver
- **Outputs:** Exception record linked to technology, exception status, audit trail
- **Behavior:** Create exceptions with justification and approval; mark exceptions as active/expired; track exception approver and dates; link exceptions to technology records for visibility

#### Capability: Web Analytics & Monitoring

- **Description:** Track user engagement and adoption metrics to measure portal success.
- **Inputs:** User page views, search queries, proposal submissions, user identification
- **Outputs:** Analytics dashboard, adoption reports, usage trends
- **Behavior:** Collect page traffic and user visit frequency; track most viewed technologies; measure proposal submission rate; calculate adoption percentage by user group; generate monthly/quarterly reports

#### Capability: Governance & Approval Workflows

- **Description:** Provide administrators with tools to review, approve, or reject technology proposals and changes.
- **Inputs:** Submitted proposals, reviewer comments, approval decision
- **Outputs:** Approved/rejected proposals, change notifications, updated catalog
- **Behavior:** Admin dashboard shows pending proposals; reviewers can view proposal details and request changes; approve/reject with comments; approved proposals automatically update catalog; maintain decision audit trai

## Step 3: Constraints & Considerations

### Technical Constraints

- What existing systems must this integrate with?
  No Integration wit hexisting system
  Integration with other systems will be through deep links, no live integrations.
- Are there specific technology requirements or restrictions?
  This will be static web page hosted on GitHub Pages
- What are the performance/scalability requirements?
  Static web page, not expecting big amount of users. Probably 2-3 concurrent users

### Organizational Constraints

- What approval processes exist?
- Who are the stakeholders?
  Technology Director, Engineering Director
- What are the security/compliance requirements?
  We must do data classification that is stored, as those are company related data and about their systems. so it's not a public data.
  Only generic technology infomration is public data.

### User Experience Constraints

- What devices/platforms must be supported?
  it should be reactive web page, supporting to show infomration on desktop and mobile phone in the browser.
- Are there accessibility requirements?
  Yes, but not strict.
- What about internationalization/localization?
  No needed, content need to be in english.

## Notes & Open Questions

[Capture any additional thoughts, concerns, or questions that arise during this draft phase]
