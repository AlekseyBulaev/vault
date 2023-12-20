## Security Concerns

Script injection
- A value, set outside a workflow, is used in workflow
- example: issue title used in workflow shell command
- workflow / command  behavior could be changed
Malicious Third-party actions
- actions can perform any logic, including potentially malicious logic
- example: a third-party action that reads and exports your secrets
- only use trusted actions and inspect code of unknown / untrusted authors
Permission Issues
- consider avoiding overly permissive permissions
- example: only allow checking out code ("read-only")
- GitHub actions supports fine-grained permissions control
---

## Script Injection Attacks

```YAML
name: Label Issues (Script Injection Example)
on:
  issues:
    types:
      - opened
jobs:
  assign-label:
    runs-on: ubuntu-latest
    steps:
      - name: Assign label
        run: |
          issue_title="${{ github.event.issue.title }}"
          if [[ "$issue_title" == *"bug"* ]]; then
          echo "Issue is about a bug!"
          else
          echo "Issue is not about a bug"
          fi
```
---
```YAML
name: Label Issues (Script Injection Example)
on:
  issues:
    types:
      - opened
jobs:
  assign-label:
    runs-on: ubuntu-latest
    steps:
      - name: Assign label
        env:
          TITLE: ${{ github.event.issue.title }}
        run: |
          if [[ "$TITLE" == *"bug"* ]]; then
          echo "Issue is about a bug!"
          else
          echo "Issue is not about a bug"
          fi
```
---
![[Pasted image 20231127172417.png]]

---

[doc](https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs)

