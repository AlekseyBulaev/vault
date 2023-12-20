## Conditional Jobs & Steps
[doc](https://docs.github.com/en/actions/using-jobs/using-conditions-to-control-job-execution)

```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

[contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)

```YAML
- name: Test code
  id: run-tests
  run: npm run test
- name: Upload test report
  if: failure() && steps.run-tests.outcome == 'failure'
```
---

## Special Conditional Functions

- failure() = returns true when any previous step or job failed
- success() =returns true when none of the previous steps have failed
- always() = causes the step to always execute, even when cancelled
- cancelled() = returns true if the workflow has been cancelled

---
```YAML
- name: Test code
  continue-on-error: true
```
---
## Matrix Strategies

[doc](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs)

```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        version: [10, 12, 14]
        os: [ubuntu-latest, windows-latest]
        include:
          - version: 16
            os: ubuntu-latest
        exclude:
          - version: 10
            os: windows-latest
	runs-on: ${{ matrix.os }}
```
---

## Reusable Workflows

[doc](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

```YML
on: workflow_call
```

```YAML
deploy: 
  needs: build
  uses:./.github/workflows/reusable.yml
```
