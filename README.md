# Github-Actions-and-CI-CD-Advanced-Concepts-and-Best-Practises

### LESSON 1 : Best Practises For GitHub Actions

**Objectives**:
- Understand how to write maintainable GitHub Actions workflows.
- Learn about code organization and creating modular workflows.

---
**Writing Maintainable Workflows**:

1) Use Clear and Descriptive Names:
- Name your workflows,jobs, and steps descriptively for easy understanding

- Example `name: Build and Test Node.js Application`

2) Document Your Workflows:
- Use comments within the YAML file to explain the purpose and functionality of complex steps.

**Code Organisation and Modular Workflows**:

1) Modularize Common Tasks:
- Create reusable workflows or actions for common tasks.
- Use `uses` to reference other actions or workflows

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Install Dependencies
      run: npm install
    # Modularize tasks like linting, testing etc.
```

2) Organise Workflow Files
  - Store workflow in the ` .github/workflows` directory
  - Use seperate files for different workflows eg `build.yml` `deploy.yml`.


### LESSON 2: Performance Optimization

**Objectives**:
 
 - Optimize the execution time of workflows
 - Implement caching to speed up builds.

 **Optimizing workflow execution time**.

 1) Parallelize Jobs
 - Break your workflow into multiple jobs that can run in parallel.
 - Use `strategy.matrix` for testing across multiple environments.

 **Caching dependencies for faster builds**.

 1) Implement Caching:

- Use the `actions/cache` actions to cache dependencies and build workflow.

```yaml
- uses: actions/cache@v2
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: ${{ runner.os }}-node-
# This caches the npm modules based on the hash of 'package-lock.json'.
```

### LESSON 3: Security Considerations

**Objectives**:

- Implement security best practises in GitHub Actions
- Secure secrets and sensitive information.


**Implementing Security Best Practises**

1) Least Priviledge Principle
- Grant minimum permissions neccessary for the workflows.
- Regularly review and update permissions

2) Audit and Monitor Workflow Runs
- Regularly check workflow run logs for unexpected behavior.

**Securing Secrets and Sensitive Information**

1) Use Encrypted secrets
- Store sensitive information like tokens and keys in **GitHub Encrypted Secrets**.


```yaml
env:
  ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
# Use secrets as environment variables in your workflow.
```

2) Avoid Hardcoding Sensitive Information
 
- Never hardcode sensitive details like passwords directly in your workflow files.



