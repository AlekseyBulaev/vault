## What is "GitHub Actions"?

#### A Workflow Automation Service by GitHub
	- Automated all kinds of repository processes and actions
		- Code Deployment (CI/CD)
		- Code and Repository Management
---
## GitHub Actions: Fundamentals


prerequisites: 

* basic understanding how git works
* gitHub account


---
## Key Elements

- workflows
- jobs
- steps
---
- workflows
	- attached to a gitHub repository
	- contain one or more **Jobs**
	- triggered upon **Events**
---
- jobs
	- Define a **Runner** (execution environment)
	- contain one or more **Steps**
	- run in parallel (default) or sequential
	- can be conditional
---
- steps
	- execute a **shell script** or **Action**
	- can use custom or third-party actions
	- steps are executed in order
	- can be conditional
---
## Practice

Navigate to "Actions" tab in your repository and click "Configure" under "Simple workflow"
![[Pasted image 20231121232835.png]]
---
path: <REPO_NAME>/.github/workflows/<YOUR_NAME_ACTION>.yml

```YAML
name: First Workflow
on: workflow_dispatch
jobs:
	YOUR_JOB_NAME:
		runs-on: ubuntu-latest
		steps:
			- name: YOUR_STEP_NAME
			  run: echo "Hello world!"
			- name: STEP_NAME
			  run: echo "Succedded"
```
---
## Events (Workflow Triggers)
repository-related:
- push (pushing a commit)
- create (a branch or tag was created)
- pull_request (opened, closed,...)
- issues (an issue was opened/closed)
- fork (repository was forked)
- many more
---
## Events (Workflow Triggers)
other:
- workflow_dispatch (manually trigger workflow)
- repository_dispatch (issue or PR comment action)
- schedule (workflow is scheduled)
- workflow_call (can be called by other workflows)
---
	! Run servers doesn't have code from the repository, so we need to get code first/install dependencies

---

## What are Actions?

- a (custom) application that performs a (typically complex) frequently repeated task
- We can build our own actions and we can use official or community Actions
---
instead of
```YAML
run: 
```
write
```YAML
	uses: actions/checkout@v3
	with:
	...
```

[actions/checkout@v3](https://github.com/marketplace/actions/checkout)
---
## Runners

Every job gets its own runner - its own virtual machine  that's totally isolated from other machines and jobs.

[ubuntu-latest](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2204-Readme.md)

---
## Execution sequentially

```YAML
my_second_job:
	needs: my_first_job
	runs-on: ubuntu-latest
	...
```

---
## Using multiple triggers

```YAML
on: [push, workflow_dispatch, ...]
```

---
## GitHub Actions Context

[doc](https://docs.github.com/en/actions/learn-github-actions/contexts)

```YAML
steps:
  - uses: actions/hellow-world-javascript-action@v1.1
    if: "${{ <expression> }}"
```
