# Challenge 2 - Braindump

## Release Pipeline Configuration
In our pipelines we need to create a production environment to be able to protect this. For that we need to update our `ordering`, `frontend` and `catalog` pipline to include a job that targets a environment `production`

We can create environments in te settings page of our repository. 

Find some more info on how to create environments and target them [here on GitHub](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)

## Branch Protection Rules
To make sure nobody can just commit to the main branch without a review or Pull Request, we needs to set up some branch protection rules

Make sure you check the right things to get optimal protection

- Restrict deletions
- Require linear history
- Require a pull request before merging
  - Require Approvals: 1
  - Dismiss stale pull request approvals when new commits are pushed
  - Require review from Code Owners
  - Require approval of the most recent reviewable push
  - Require conversation resolution before merging
- Block force pushes

The new Branch rulesets look like the ideal feature for this task.](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets). 

## Codeowners Setup
To be sure that the right people review the right things, we can use CODEOWNERS. Set this up that our team is the reviewer. 
[More info can be found on GitHub](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners). I 
Don't forget to protect the `CODEOWNERS` file itself from unauthorised changes.

## Rebase Strategy Implementation

There a many ways how you can merge changes to the codebase. In the past it has been rough finding what's going on with all these people comitting code on branches and then merging it. Let's try and keep a clean history!

Looks like GitHub will allow us to configure this desired merge method.  Let's disable merge commits and implement Rebase.

More info on merge strategies can be [found here](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/about-merge-methods-on-github) 
