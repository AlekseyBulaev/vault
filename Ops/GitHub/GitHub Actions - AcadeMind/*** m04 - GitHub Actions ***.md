## Understanding Job Artifacts

![[Pasted image 20231122221304.png]]

---
## Uploading Job Artifacts

[doc](https://github.com/actions/upload-artifact)
```YAML
  ...
    - name: upload-artifacts
      uses: actions/upload-artifact@v3
      with:
        name: YOUR_NAME
        path: |
          path/to/artifact
          other/path
```

---
## Downloading Artifacts

[doc](https://github.com/actions/download-artifact)

```YAML
  - uses: actions/download-artifact@v3
    with:
      name: my-artifact
      path: ~/download/path
```

---

## Understanding Job Outputs

Simple values => 
- typically used for reusing a value in a different jobs
- example: name of a file generated in a previous build step

---

## Setting an environment variable

[doc](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-environment-variable)
```YAML
steps:
  - name: Set the value
    id: step_one
    run: |
      echo "action_state=yellow" >> "$GITHUB_ENV"
  - name: Use the value
    id: step_two
    run: |
      printf '%s\n' "$action_state" # This will output 'yellow'
```

---
## Caching Dependency

[doc](https://github.com/actions/cache)

```YAML
- name: Cache dependencies
        uses: actions/cache@v3
        with:
          path: ~/.npm
          key: deps-node-modules-${{ hashFiles('**/package-lock.json') }}
      - name: Install dependencies
        run: npm ci
```

---
