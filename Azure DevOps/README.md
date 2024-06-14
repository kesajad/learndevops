# WhiteBoard
## Day 1
![Azure DevOps](https://github.com/kesajad/learndevops/assets/99335234/40e4b79b-9123-4a20-a048-ee60c28c4cca)
## Day 2
![Azure DevOps (1)](https://github.com/kesajad/learndevops/assets/99335234/7fb6b3fc-7b0f-4ecd-bc6b-89ce3cafef8b)
## Day 3
![null](https://github.com/kesajad/learndevops/assets/99335234/43041b1c-43be-49d6-affc-e663ec19b87d)
## Day 4
![null (1)](https://github.com/kesajad/learndevops/assets/99335234/3a332386-c7e5-4615-8d99-7d02be7b9189)

# Azure DevOps CI CD
## Service Principle?

![image](https://github.com/kesajad/learndevops/assets/99335234/da85790a-512b-46b4-9c0d-7e20837ee984)

## CI CD Automation - Work Flow
![image](https://github.com/kesajad/learndevops/assets/99335234/f6e9328b-2ca4-474c-945b-2ef169b0f719)

## Blue Green Deployment
![image](https://github.com/kesajad/learndevops/assets/99335234/a8f6b50f-6b97-4d77-8ff6-9e1ba5af0922)

### YAML Pipeline in the demo
YAML Pipeline for NodeJS Web App
```
trigger: 
- main

stages:
- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: Npm@1
      inputs:
        command: 'install'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'

    
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: 'build'
        ArtifactName: 'drop'
        publishLocation: 'Container'

- stage: Deploy 
  jobs:
  - job: Deploy
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: DownloadBuildArtifacts@1
      inputs:
        buildType: 'current'
        downloadType: 'single'
        artifactName: 'drop'
        downloadPath: '$(System.ArtifactsDirectory)'
    - task: AzureRmWebAppDeployment@4
      inputs:
        ConnectionType: 'AzureRM'
        azureSubscription: 'Test-SP'
        appType: 'webAppLinux'
        WebAppName: 'GuruSchools'
        packageForLinux: '$(System.ArtifactsDirectory)/drop'
        RuntimeStack: 'STATICSITE|1.0'
```
