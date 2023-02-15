# ansible-role-sonarqube

you can run like this, but hopefully in a more ansiblonic fasion :) 

```
# get role and requirements
yum install -y git
pip3 install ansible
git clone https://github.com/rhythmictech/ansible-role-sonarqube.git
ansible-galaxy install -r requirements.yml
sudo yum install java-17-amazon-corretto

# create a playbook that has the variables and executes the roles
cd ..
cat << EOF > playbook.yml
---

- hosts: localhost
  remote_user: root

  vars:
    sonar_version: 9.9.0.65466
    sonar_db_pass: "SECRET"
    sonar_db_host: "mydatabase.rds.amazonaws.com"
    java_version: 1.17
    java_provider: amazon-corretto
    java_use_ansible_yum: false

  roles:
    - role: yumrepos
    - role: ./ansible-role-sonarqube
EOF

# run it
ansible-playbook playbook.yml
```
