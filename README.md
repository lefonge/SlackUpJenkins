# SlackUpJenkins
Slack integration in Jenkins to remotely invoke Jenkins jobs from a Slack channel

**Author:** Marco Da Pieve

---

## Contents

1. [Project Scope](#project-scope)
2. [Procedure](#procedure)
   - [Requirements](#requirements)
     - [Platform Setup AWS EC2 Instance](#platform-setup-aws-ec2-instance)
     - [Java Installation](#java)
     - [Jenkins Installation](#jenkins)
     - [Jenkins First Setup](#jenkins-first-setup)
   - [Create a GitHub Repository](#create-a-github-repository)
   - [Slack Configuration](#slack-configuration)
     - [Create a Slack Channel](#create-a-slack-channel)
     - [Integrate Jenkins into Slack](#integrate-jenkins-into-slack)
   - [Jenkins Notification Configuration](#jenkins-notification-configuration)
   - [Create a Jenkins Job](#create-a-jenkins-job)
   - [Testing Slack Notification](#testing-slack-notification)
   - [Triggering Builds from Slack](#triggering-builds-from-slack)
     - [Pipedream Solution](#pipedream-solution)
     - [Slash Command Integration Solution](#slash-command-integration-solution)
3. [Conclusion](#conclusion)

---

## Project Scope

To create a Slack channel, receive Jenkins build notifications, and use it to invoke Jenkins jobs remotely by configuring slash commands in Slack.

---

## Procedure

### Requirements

#### Platform Setup AWS EC2 Instance

1. Set up an AWS EC2 instance running Ubuntu 24.04.
2. Ensure that the instance is accessible via SSH and a public IP for communication between Jenkins and Slack.

Follow [this guide](https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/) to install Jenkins on AWS, ensuring the instance's security group allows inbound traffic.

#### Java Installation

1. Install OpenJDK 17 using:

```bash
sudo apt -y install fontconfig openjdk-17-jre
java -version
```

Verify the installation with `java -version`.

#### Jenkins Installation

1. Add the Jenkins repository:

```bash
wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt-get update
```

2. Install Jenkins:

```bash
sudo apt-get -y install jenkins
```

3. Verify Jenkins is running:

```bash
systemctl status jenkins
```

#### Jenkins First Setup

1. Access Jenkins via `http://<public-ip>:8080`.
2. Retrieve the admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

3. Install recommended plugins, create an admin user, and complete the setup.

### Create a GitHub Repository

1. Log in to [GitHub](https://github.com/).
2. Create a repository and add necessary files, including a `README.md`.

### Slack Configuration

#### Create a Slack Channel

1. Create a new Slack channel and name it appropriately.
2. Use this channel for Jenkins notifications.

#### Integrate Jenkins into Slack

1. Add the "Jenkins CI" app in Slack via the "Integrations" tab.
2. Obtain the integration token and configure Jenkins for Slack notifications.

### Jenkins Notification Configuration

1. Install the "Slack Notification" plugin in Jenkins.
2. Configure Slack workspace and credentials in Jenkins settings.
3. Test the Slack connection to confirm successful integration.

### Create a Jenkins Job

1. Create a freestyle Jenkins job.
2. Configure source code management with a GitHub repository.
3. Add build steps and enable Slack notifications under "Post-build Actions."

### Testing Slack Notification

1. Trigger a build and check Slack for notifications.
2. Test error scenarios by introducing intentional build failures.

### Triggering Builds from Slack

#### Pipedream Solution

1. Set up a [Pipedream](https://pipedream.com/) webhook to handle Slack slash commands.
2. Configure it to send HTTP POST requests to Jenkins.

#### Slash Command Integration Solution

1. Configure Slack's legacy integration with slash commands.
2. Use the integration token to trigger builds in Jenkins.

---

## Conclusion

The integration of Slack with Jenkins using modern and legacy approaches streamlines build notifications and remote job triggers, enhancing team collaboration and productivity.
