## Environment Variables & Secrets

```JS
const password = process.env.DB_PASSWORD
```

You can add environment variables on:
- workflow level
- jobs level
- steps level
[doc](https://docs.github.com/en/actions/learn-github-actions/variables#naming-conventions-for-environment-variables)

---
```yaml
env:
  DAY_OF_WEEK: Monday

jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - name: "Say Hello Mona it's Monday"
        if: ${{ env.DAY_OF_WEEK == 'Monday' }}
        run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Mona

```

---
## Understanding & Using Secrets

[doc](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions)

- we can store secrets on organization level
- we can store secrets on repository level
```yaml
env:
  PASSWORD: ${{ secrets.PASSWORD }}
```

---
![[Pasted image 20231124214320.png]]

---

## Environment

[doc](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)

```yaml
name: Deployment

on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: deploy
        # ...deployment-specific steps
```

---

