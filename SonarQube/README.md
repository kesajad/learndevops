# SonarQube
## What is SonarQube?
-  SonarQube is a self-managed, automatic code review tool that systematically helps you deliver Clean Code.
-  SonarQube integrates into your existing workflow and detects issues in your code to help you perform continuous code inspections of your projects.
-  The product analyses 30+ different programming languages and integrates into your Continuous Integration (CI) pipeline of DevOps platforms to ensure that your code meets high-quality standards.

### 1 Onboard SonarQube Extension in Azure DevOps
- Onboard an Extension for SonarQube in Azure DevOps

### 2 Create a Linux VM
- Create a linux VM for SonarQube
- Encapsulated file for Docker Installation
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- Run SonarQube as a Docker Container
```
sudo docker run -d --name sonarqube -p 9000:9000 sonarqube
```
- Default login : admin & passwd: admin

### 3 Integrate SonarQube in Azure Pipelines - Classic Pipeline (Optional)
-  We need to add 3 tasks
1. Prepare Analysis Configuration
2. Run Code Analysis
3. Publish Quality Gate Result
   
![image](https://github.com/kesajad/learndevops/assets/99335234/0187057c-0a24-4e37-a613-1830ad9f237d)

### 4 Integrate SonarQube in Azure Pipelines - YAML Pipeline
-  Build pipelines can be configured as mentioned below
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
      - task: SonarQubePrepare@6
        inputs:
          SonarQube: 'sonarqube-connection'
          scannerMode: 'CLI'
          configMode: 'manual'
          cliProjectKey: 'clone_yt_YAML'
          cliProjectName: 'clone_yt_YAML'
          cliSources: '.'
      - task: SonarQubeAnalyze@6
        inputs:
          jdkversion: 'JAVA_HOME_17_X64'
      - task: SonarQubePublish@6
        inputs:
          pollingTimeoutSec: '300'
      - task: PublishBuildArtifacts@1
        inputs:
          PathtoPublish: 'build'
          ArtifactName: 'drop'
          publishLocation: 'Container'
```
## Projects in SonarQube
-  Final Summary of the Dashboard
![image](https://github.com/kesajad/learndevops/assets/99335234/b726fd13-0917-46c2-89a2-4f88fb195b27)


