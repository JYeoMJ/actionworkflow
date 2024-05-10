# actionworkflow
GitHub Action Workflow Tutorial
***
## Github Actions Workflow Tutorial

### What is Github Actions?

* Built-in automation platform within GitHub for defining workflows triggered by events in repository
* Task automation for streamlining development process
* Used for CI/CD Continuous Integration & Deployment
* GitHub Actions provides a **seperate workfow envrionment**, note files generated within workflow are not automatically commited to repository.


### Overview:

1. Create GitHub repository
2. Prepare Python Files (`model.py` file)
3. Create requirements.txt with all python dependencies
4. Configure GitHub Actions
	* Create a `.github/workflows` directory within repository root
	* Create workflow `python-app.yml` file within `.github/workflows`.
5. Running the Workflow
***
### Workflow file creation

Explanation of `python-app.yaml` file:

* Workflow runs on every push to main branch
* Uses the `actions/checkout@v3` action to check out the code
* Installs dependencies from `requirements.txt`
* Runs `model.py` to train model

```yaml
name: Python application

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Python 3.8
      uses: actions/setup-python@v4
      with:
        python-version: 3.8
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Run the script
      run: |
        python model.py
```
 
Validation of YAML file: [Validate-YAML](https://onlineyamltools.com/validate-yaml)
***
### Triggering Workflow

Push codes to main branch of GitHub repository:

```git
git add model.py requirements.txt python-app.yml
git commit -m "Added YAML workflow file"
git push origin main
```

Monitor workflow in "Actions" tab of repository for workflow execution.




