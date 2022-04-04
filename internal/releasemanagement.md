---
title: Release Management
description: Release and Process
published: true
date: 2022-04-01T01:48:55.762Z
tags: 
editor: markdown
dateCreated: 2022-03-17T06:51:01.450Z
---

# Release Management V1

## Roles and Responsibilities

1. **Developer**
- Keeps feature/issue branch up-to-date with the latest development branch
- Adheres to the guidelines, criteria for the release
- Responsible for keeping the branches and the trunk green all the time
2. **Release Master/Engineer**
- Serves as a guard (temporary) for development branch. Ensures that commits have adhered to the criteria prior merging
- Merges changes between development-staging and staging-production branches when needed (except for the feature-development)
- Prepares release package

## Types of Branches

1. Feature/Issue
**Purpose**: This branch contains a specific feature implemented or an issue fixed by the feature/issue owner  
**Frequency of Commit**: Everyday
**Environment**: local environment

1. Testing
**Purpose**: This branch contains any features implemented and issues fixed by the team. 
**Condition of Commit**: Every time a new feature has been implemented and/or an issue has been fixed 
**Environment**: https://test.saito.io/

1. Staging
**Purpose**: This branch contains features and issues for the upcoming release
**Condition of Commit**: For features and/or issues that passed the testing in Development branch and is/are planned for the upcoming release
**Environment**: https://staging.saito.io/

1. Production
**Purpose**: This branch contains the latest stable version of the source code
**Condition of Commit**: Every release and/or (EXCEPTION:) a critical issue needs to be released
**Environment**: https://saito.io/arcade/

## General Guideline

1. Keep your feature/issue branch updated daily based on the latest development branch
1. Only commit on the development branch completed and locally tested features and/or issues
1. Only commit on the staging environment the features and/or issues planned for the upcoming release

## Criteria before merging changes to a branch

A list of checklist for each branches have been created before you can merge a feature and/or issue to a specific branch. This ensures the quality of the commits and reduces the breakage on the source code.

1. Testing
- Locally passed unit test and basic manual test
- At least 80% unit test code coverage
- Reviewed and signoffed by another developer
2. Staging
- Feature and/or issue is part of the upcoming release
- No Critical and Major issues open from Development branch
- Passed CI Testing (Future)
3. Production
- Passed end to end testing in Staging
- Passed usability testing in Staging
- No Critical and Major issues open
- Passed Performance Test (Future)

## Roll out Checklist
- No open critical and major issue
- Passed the 2 days Early adopters User Testing (Monitoring period)
- Release Communication Content prepared
- Signoff from Leads (Sanka - Rust, Dan - Appspace) on the result of the Monitoring Period

## Release Cadence

We are aiming to release every 2 weeks.

- **Week 1-2**
Implement and Test in Feature & Development Branch
- **Week 2** 
Merge Test Branch to Staging Branch
- **Week 3** 
	Test Staging Branch and Fix Issues
	Merge Staging to Production
  Beta Test/Stability Test
  Release communication

Note: Week 3 (Testing) will be in parallel with the Sprint Development Cadence
  

