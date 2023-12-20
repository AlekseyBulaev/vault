## What Are Containers?

Docker container
- packages that contain code + its execution environment
- advantage: reproducible execution environment & results

Full control over environment & installed software instead of pre-installed

GitHub Actions Runners: 
- containerized job is hosted by the runner
- steps execute inside the container
- we can create Services: utility containers used by our steps (e.g. testing DB)
---
[doc](https://docs.github.com/en/actions/using-jobs/running-jobs-in-a-container)

```YML
name: CI
on:
  push:
    branches: [ main ]
jobs:
  container-test-job:
    runs-on: ubuntu-latest
    container:
      image: node:18
      env:
        NODE_ENV: development
      ports:
        - 80
      volumes:
        - my_docker_volume:/volume_mount
      options: --cpus 1
    steps:
      - name: Check for dockerenv file
        run: (ls /.dockerenv && echo Found dockerenv) || (echo No dockerenv)

```

---
