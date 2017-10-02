This repo is used for exercises in the [Continuous Integration, Delivery or Deployment with Jenkins, Docker and Ansible](http://technologyconversations.com/2015/02/11/continuous-integration-delivery-or-deployment-with-jenkins-docker-and-ansible/) article

```
apt-get install -y software-properties-common
apt-add-repository ppa:ansible/ansible
apt-get update
apt-get install -y ansible
```

```
sudo ansible-playbook ansible/cd.yml -c local -v
```