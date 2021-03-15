### Release Drafter Action
Release Drafter Action is lightweight github action release drafter to help you to automate your release draft using merge event as the trigger. The version will increment automatically with some spec below 
```
Major = unlimited
Minor = max 99 -> after reach the max will back to 0 and then increment the major version
Patch = max 99 -> after reach the max will back to 0 and thne increment the minor version
```

### How To Use
1. Open Your Repo, create labels on your repo, for example `learning-git`. This label will be use as service indentifier on the github action script.
2. Create github action script on your repo 
```
.github
    workflows
        release_drafter.yml
```
Put below code on your `release_drafter.yml`
```
name: Create Release
on:
  pull_request:
    types: [closed]

jobs:
  release_drafter_job:
    runs-on: ubuntu-latest
    name: Just Create Release
    steps:
    - name: Release Drafter
      env:
          REPO: 'LearningGit'
          OWNER: 'hengkyawijaya'
          GITHUB_TOKEN: ${{ secrets.USER_TOKEN }}
      id: release_drafter
      uses: hengkyawijaya/release-drafter-action@v0.0.5
      with:
        service: 'learning-git'
        prefix: 'v'
        postfix: ''
```
3. Open repo setting > secrets, then add new secret, with last step we need USER_TOKEN secret. Put the value inside it.
4. Try your github action by creating test branch, then merge it to main/master
5. Magic will happen, your draft release created automatically

Sample Repo that using this github action
https://github.com/hengkyawijaya/LearningGit

Made with <span style="color: #e25555;">&hearts;</span> by hengkyawijaya
