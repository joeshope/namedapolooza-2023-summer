# Snyk PR Check Failure Notification 

## Description
The objective of this GitHub Action is to identify when Snyk PR Checks fail. When this occurs, the action will add a Reviewer to the PR so that the issue(s) can be triaged. This will help bridge the gap between AppSec Snyk Admins and Development Team(s).

## Group Members
Morgan Smith, Andrew Southard, Jenny Hinz, and Joe Shope

## Prerequisites
While there are no local software requirements for this project, the following GitHub actions are used:  
[Wait For Commit Statuses Action](https://github.com/marketplace/actions/wait-for-commit-statuses)  
[Add Reviewers Action](https://github.com/marketplace/actions/add-reviewers)

## Getting Started
This project is for use with GitHub repositories and runs as a GitHub action. [GitHub Actions](https://github.com/features/actions)  
This project is intended to be used in conjunction with Snyk PR Checks. If the repository has not yet been imported to Snyk, please do so prior to use. [Import Repository using Snyk UI](https://docs.snyk.io/integrations/git-repository-scm-integrations/github-enterprise-integration)   
It is recommended that branch protection is used for your default branch and that `Require a pull request before merging` is checked. Optionally enabling `Require status checks to pass before merging` will further protect your default branch. [GitHub Branch Protection](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)

### Setup
1. Create a `.github/workflows` directory in your GitHub repository. Copy the 'snyk\_notify\_gh\_action' file into this directory.  
2. `REVIEWERS` - Add a GitHub variable with a comma delimited list of your reviewers to be notified. ex. jhinz1,morgansnyk,joeshope NOTE: These reviewers should be the individuals that usher the PR Check through to merge so Snyk Admin permissions are recommended.  
3. `GITHUB_TOKEN` - Create a repository secret for your GitHub PAT with permissions to add a Commit to the Pull Request as well as access Pull Request commits.  

(Optional) Changes to the 'snyk\_notify\_gh_action' file.   
`checkInterval` - default 13. Amount of delay in seconds between checks - this can be lowered or raised to your needs.  
`ignoreActions` - default 'waitforstatuschecks'. If you utilize additional checks that you would like to be ignored from this flow, add them in a comma delimited list. ex. 'waitforstatuschecks,Other Action'.  
`re-request-when-changes-requested` - default true. When a reviewer has requested for changes, pushing a new commit to this PR will Re-request a review from them. Can be configured to false.   
`re-request-when-approved` - default true. When a reviewer has approved, pushing a new commit to this PR will Re-request a review from them. Can be configured to false.

## Usage
The usage of this GitHub action is simple, it will run during Pull Request to verify that the Snyk PR Checks are successful. If any should fail, it will assign a reviewer which will trigger a GitHub notification to the reviewer.