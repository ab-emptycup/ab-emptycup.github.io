---
layout: page
title: Org cleanup
---

A list of all the things that needed to be cleaned up.
The goal is to evolve conventions / processes, so that these things don't get messy again.

### Domain email accounts for old employess

- Google accounts
- Signups for newsletters and services

Learnings:

- Instructions not to use it for personal usecases
- Process to suspend & delete accounts of exiting employees.
- Process to redirect / reject emails received on exiting employee accounts.
- TODO: Gdrive data for employee accounts

### Github repositories

- 95 repositories, 5 needed

Learnings:

- High bias against submodules
- High bias against multiple repositories

### Cloud deployment

- Multiple clouds
- Multiple deployments for a service
- Multiple environments for a service

Learnings:

- Single point billing
- Deploy coliving containerized applications on common infrastructure
- Avoid multiple services
- Avoid multiple service environments
- NEVER mix and match services to environments

### DNS

- Multiple domains
- Combinations of (service, environment) sub domains
- Admin domains
- Validation TXT records for stale services

Learnings:

- Admin should be part of the product / service.
- DNS should be hosted where SSL is automatically renewed irrespective of registrar.
- Avoid multiple domains
- Avoid multiple DNS servers