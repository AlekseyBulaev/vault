## Event Activity Types & Filters

More detailed control over when a workflow event will be triggered
- pull_request Event -> opened/closed/edited
- push Event -> filter based on target branch
---
## Using Activity Types
 ```YAML
name: Activity Type
on:
  pull-request:
    types: 
      - opened
      - edited
  worlflow_dispatch:
```
---
## Using Event Filters
```YML
name: Activity Type
on:
  push:
    branches: 
      - main
      - 'feature/**'
    paths-ignore:
      - '.github/workflows/*'
```
---
## A Note About Fork PR Workflows 
By default, PR based on Forks do NOT trigger a workflow
- reason: Everyone can fork & open pull requests
- malicious workflow runs & excess cost could be caused

=>

First-time contributors must be approved manually

---
## Cancelling and Skipping Workflow Runs

cancelling
- by default, workflows get cancelled if Jobs fail
- by default, a job fails if at least one step fails
- we can also cancel workflows manually
skipping
- by default, all matching events start a workflow
- exceptions for "push" & "pull_request"
- [skip](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs) with proper commit message
```BASH
git commit -m "some changes [skip ci]"
```
