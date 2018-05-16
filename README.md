
# What is it?
The project contains Ansible script for fully automated deployment of server with all required for development infrastructure.
It deploys:
- IRC server.
- GitLab with existing projects.
- Trac with all tickets.
- Jenkins with all required jobs
- SonarQube.
- LDAP - to store access to GitLab, Trac, Jenkins and SonarQuibe in single place for easy user's management 
(IRC has separate config because doesn't suppport LDAP).

All services has fully configured access for developers.
Service should have backup mechanism, all data should be stored outside on durable storage (e,g, Amazon S3).
Backup data should be used by the Ansible script in case need to reprovision another machine.

# How to use it?
To run Ansible script on any machine you need to install Ansible on it:
```
apt-get install -y software-properties-common
apt-add-repository ppa:ansible/ansible
apt-get update
apt-get install -y ansible
```

To deploy environment on Kattar, please create ansible/kattare/inventory file (similar to ansible/lxctest/inventory)
but with server ssh-user user/password and url.

Then you can run scripts:
```
cd ansible
ansible-playbook playbook.yml -v -i kattare
```

# How to update/test it?
It is useful to test script against some fresh machine with preinstalled particular Linux version.
One of the way is ti use LXC container it allows to create very fast fresh instance of required Linux.
lxc folder has Vagrant file to create container with Ubuntu 14.04 because we have it on Katare server.
So need to install vagrant and lxc on developer's machine.
1. To install vagrant it is better to take fresh version from https://www.vagrantup.com/downloads.html
2. To install lxc
```
sudo apt-get update
sudo apt-get install lxc
```
3. Install vagrant lxc-provider
```
vagrant plugin install vagrant-lxc
```

To create container and run Ansible scripts against it:

```
cd lxc
vagrant up
cd ../ansible
ansible-playbook playbook.yml -v -i kattare
```

-----------------------
sudo rm -rf /var/lib/jenkins/plugins
ls -lah /var/lib/jenkins/plugins

To login t Jenkins use admin/admin then change asap
add new users

---
Jenkins GitHub integration
1. install github plugin
2. Create Freestyle Project
2. Go to Job configurations and tick "GitHub project".
2. Provide "Project url" (e.g. https://github.com/mekhanikov/Shoportunity/)
2. In "Build Triggers" sections tick "GitHub hook trigger for GITScm polling".
2. go to "Manage Jenkins->Configure System" to GitHub section
3. Press most bottom "Advanced..." button.
4. "Additional actions" select in dropdown menu: "Convert login and password to token"
5. Add GitHub Server and provide generated token to Credentials dropdown.
6. Press "Re-register hooks for all jobs" button (should see "Called re-register hooks for 1 items").

Jenkins GitHub integration:
1 login to Jenkins
2 Jenkins -> New Item
3 Create "GitHub Organization" project
4 with name "factorydirectparty"
5 Go to project configurations
6 "GitHub Organization" section
7 Add credentials
8 Select "factorydirectparty" (or Jenkins?)
9 Provide login/pass for admin of the repo
10 Press "Save" button.
11 Go to GitHub, to project settings check Webhooks. 
It should have:
- Payload URL: http://50.116.55.235:8080/github-webhook/
- Content type: application/json
- Which events would you like to trigger this webhook?
  tick "Let me select individual events."
  select: 
  - Push
  - Pull request

Now on each commit or Jenkins job will bw triggered automaticaly by GitHub.
Jenkins will create Job per each branch automatically.
Jenkins will send build statuses to GitHub, so statuses will be show for erach commit.

This repo is used for exercises in the [Continuous Integration, Delivery or Deployment with Jenkins, Docker and Ansible](http://technologyconversations.com/2015/02/11/continuous-integration-delivery-or-deployment-with-jenkins-docker-and-ansible/) article

