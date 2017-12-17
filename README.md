This repo is used for exercises in the [Continuous Integration, Delivery or Deployment with Jenkins, Docker and Ansible](http://technologyconversations.com/2015/02/11/continuous-integration-delivery-or-deployment-with-jenkins-docker-and-ansible/) article

```
apt-get install -y software-properties-common
apt-add-repository ppa:ansible/ansible
apt-get update
apt-get install -y ansible
```

```
sudo ansible-playbook ansible/cd.yml -c local -v -i "localhost," 
```
cd ansible/
sudo ansible-playbook cd.yml  -v -i prod


https://github.com/factorydirectparty/Shoportunity.git
emekhanikov@thumbtack.net

sudo rm -rf /var/lib/jenkins/plugins
ls -lah /var/lib/jenkins/plugins

To login t Jenkins use admin/admin then change asap
add new users

TODO
add credentials to jenkins store (my login / pass fo far, then key)

ssh root@50.116.55.235
4FDPjenkins


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
