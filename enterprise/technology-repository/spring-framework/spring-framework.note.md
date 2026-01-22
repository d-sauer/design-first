# Overview

This document contains notes, decisions, and updates related to the Spring Framework technology in our organization.

# Notes

## 2026-01

### Technology Registration
- Spring Framework registered as a Standard technology with global scope
- Primary use case: Web application development
- Organization currently uses multiple versions (Spring 5.x and 6.x) across different projects
- License: Apache License 2.0 (open source)
- Maintained by VMware Tanzu

### Key Decisions
- Approved as global standard for Java-based web application development
- Multiple version support acknowledged due to existing project dependencies
- Future projects should target Spring Framework 6.x where possible (Java 17+ requirement)

### Migration Considerations
- Projects on older Spring versions should plan migration to Spring Framework 6.x
- Note: Spring Framework 6.x requires Java 17+ and Jakarta EE 10 (jakarta namespace)
- Spring Framework 5.x still under active support for existing applications

### Related Technologies
- Spring Boot (built on top of Spring Framework)
- Spring Security (security framework)
- Spring Data (data access)
- Spring Cloud (microservices and cloud-native features)
