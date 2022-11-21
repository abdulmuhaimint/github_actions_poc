# Github actions PoC

This repo contains code samples and github actions workflow for the continuous integration of a nodejs project.  

**Tools used:**  
* jest (A Javascript testing framework)
* github actions
* nodejs

**Steps to follow**
1) create a \<workflow_name\>.yml file in ./.github/workflows directory
2) define the workflow inside  that file.  
3) push changes to git. 

That's it :smile:, everytime there is an event that is specified in the workflow, for example a pull request to main branch, jobs specified in the workflow will run on a cloud vm.  

if any errors in the ci it will be reported on the pull request page or we can also setup a slack/email/discord etc notification to developer.

**Detailed explanation of workflow yml file**

```yaml
# name of the workflow
name: Node Continuous Integration

# on which event the workflow should run, here it is pull_request to main branch
on:
  pull_request:
    branches: [ main ]

# specify jobs, here test_pull_request is the custom name given to the job
jobs:
  test_pull_request:
    # on which vm to run
    runs-on: ubuntu-latest

    # steps of the job, with uses command we can use pre built github actions.  
    # here actions/checkout, actions/setup-node are two prebuilt actions available on the github actions marketplace.
    # actions/checkout is to copy our github repo to the vm
    # actions/setup-node as the name suggests is used to setup nodejs on the ci vm
    # run command for executing shell commands
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
        with:
          node-version: 12
      - run: npm ci
      - run: npm test
      - run: npm run build

```
**References**  
* <a href="https://www.youtube.com/watch?v=eB0nUzAI7M8" target="_blank" title="5 Ways to DevOps-ify your App - Github Actions Tutorial">Fireship youtube video</a>
* <a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions" target="_blank" title="Github workflow syntax">Github docs</a>





