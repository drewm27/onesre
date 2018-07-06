---
layout: default
---

# Project Best Practices Checklist

This is a checklist to use to vet projects in the requirements and design document phases. Doing this due diligence in the planning stages of a project can save months or years of migration and development work before realizing a project’s design doesn’t fit the company's needs, could have been easily expanded to cover other use cases, or doesn’t fit into where the infrastructure is headed.

## Project Checklist
### Automation/Time/Cost
1. Is this designed to be used with full hands off automation?
2. Does this project hold state? Would it be better synchronizing from a master source of truth instead?
3. Does it create a competing source of truth that can’t be auto synchronized?
4. How much hands on time will this service require on a monthly basis?
5. How much time/cost will this save us vs the time/cost sunk into implementing it?
6. How long do you expect this project to live before it gets replaced by something better? Keep in mind that no project lives forever. Is there any minor work or design decisions you can change to extend that time?

### Reliability/Uptime
1. Does this design have any single points of failure?
2. Does this design have any persistent read/write data which is difficult to replicate across datacenters?
3. What are the SLA requirements for each portion of this service? 
4. Are there upstream services that this depends on with lower SLAs which will bring down the overall SLA?
5. Which parts of this service require monitoring?

### Documentation
1. Is this service documented well enough to be handed off to a team that knows nothing about it?

### Backups/Logging
1. What data in this service requires backups?

### Data
1. Defining a data retention policy: how much data do we need to retain? And how long do we need to retain it for?

### Security
1. What parts of this service have security implications?
2. Does this service need user authentication? SSO?

### Auditability/Logging
1. How does this service do logging?
2. Where do the logs go?
3. What logging library does the service use?
4. Is it the standard company approved logging library? If not, why not?

### Performance
1. What are the performance requirements of this service?
2. Are we using the right programming languages for performance critical portions of this service?

### Modularity/Code Reuse
1. Is this design modular with well defined interfaces?
2. Are modules in this project generic enough to be used in other projects? 
3. Can modules be swapped out when better ones come along?
4. Are there any additional project scopes or abstractions that could easily be added to this project to prevent it from being a one-trick pony?

### Futureproofing
1. Is this designed for use across multiple network linked datacenters?
2. Does this scale up to multiple billions in revenue?
3. If this service has a paid vendor, are we okay with paying that vendor enough as we scale up?

