#git
link: [course](https://pro.academind.com/p/github-actions-the-complete-guide)
slides: [[*** m02 - GitHub Actions ***]]
code : [github](https://github.com/academind/github-actions-course-resources)

## [[*** m02 - GitHub Actions ***]]

Core components
- workflows: defines events + jobs
- jobs: define runner + steps
- step: do the actual work
Defining workflows
- .github\workflows\<file>.yml (on GitHub or locally)
- github actions syntax must be followed
Events/Triggers
- broad variety of events (repository-related & other)
- workflows have at least one (but possible more) event(s)
Runners
- servers (machines) that executes the jobs
- pre-defined runners (with different OS) exist
- we can also create a custom runners
Workflow execution
- workflows are executed when their events are triggered
- github provides detailed insights into job execution (+ logs)
Actions
- we can run shell commands
- we can also use pre-defined actions (official, community or custom)

## [[*** m03 - GitHub Actions ***]]

Available Events
- there are many supported events
- most are repository-related
- but some are more general (schedule)
Activity Types
- the exact type of event that should trigger a workflow
- examples: opening or editing a pull request should trigger the wf
Pull Requests & Forks
- initial approval needed for PR from forked repositories
- avoid spams from untrusted contributors
Cancelling & Skipping
- workflows get cancelled automatically when jobs fail
- cancel manually
- skip via commit messages
Event Filters
- add filters to avoid some executions
- filter based on target branch and / or affected file paths

## [[*** m04 - GitHub Actions ***]]

Artifacts
- jobs often product assets that should be shared or analyzed
- examples: deployable website files, logs, binaries,...
- these assets are referred to as "Artifacts" (or "Job Artifacts")
- gitHub actions provides actions for uploading & downloading
Outputs
- besides artifacts, steps can product and share simple values
- jobs can pick up & share step outputs
Caching
- caching can speed up repeated, slow steps
- the cache action automatically stores & updates cache values (based on a cache key)
- important! - don't use caching for artifacts

## [[*** m05 - GitHub Actions ***]]

Environment Variables
- dynamic values used in code (e.g., database name)
- may differ from workflow to workflow
- can be defined on workflow-, job- or step-level
- can be used in code and in the gitHub actions workflow
- accessible via interpolation and the env context object
Secrets
- some dynamic values should not be exposed anywhere
- examples: database credentials, API keys, ...
- secrets can be stored in Repository-level or via environments
- secrets can be referenced via secrets context object
GitHub Actions Environments
- job can reference different gitHub actions environments
- environments allow us to set up extra protection rules
- we can also store secrets on environment-level

## [[*** m06 - GitHub Actions ***]]

Conditional Jobs & Steps
- control step or job execution with if & dynamic expressions
- change default behavior with failure(), success(), cancelled() or always()
- use continue-on-error to ignore step failure
Matrix Jobs
- run multiple job configurations in parallel
- add or remove individual combinations
- Control whether a single failing job should cancel all other matrix jobs via continue-on-error
Reusable Workflows
- workflows can be reused via the workflow_call event
- reuse any logic (as many jobs & steps as needed)
- work with inputs, outputs and secrets are required

## [[*** m07 - Using Containers ***]]

Containers
- packages of code + execution environment
- great for creating re-usable execution packages & ensuring consistency
- example: same environment for testing + production
Containers for Jobs
- we can run jobs in pre-defined environments
- build our own container images or use public images
- great for jobs that need extra tools or lots of customization
Service Containers
- extra services can be used by steps in jobs
- example: locally running, isolated testing database
- based on custom images or public/community images

## [[*** m08 - Custom Actions ***]]

What & Why
- simplify workflows & avoid repeated steps
- implement logic that solves a problem not solved by any publicly available action
- create & share action with the community 
Composite actions
- create custom action by combining multiple steps
- composite actions are like "workflow excerpts"
- use actions (via **uses**) and commands (via **run**) as needed
JavaScript & Docker Actions
- write action logic in javaScript (NodeJS) with @action/toolkit
- alternatively: create our own action environment with docker
- either way: use inputs, set outputs and perform any logic
## [[*** m09 - Custom Actions ***]]





### Questions:
1. Differences between  `git revert <id>` and `git reset --hard <id>`
	- revert changes of commit by creating a new commit
	- undo changes by deleting all commits since <id>
2.