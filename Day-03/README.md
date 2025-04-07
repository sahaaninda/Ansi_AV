# Writing First Ansible Playbook

- navigate to cd /etc/ansible/hosts
- consdering "_inventory.ini_" file is already created with the manage nodes
- create the file "_first-playbook.yaml_" > code is in this repo
- create the file "_index.html_" > code is in this repo
- run ansible playbook
  ```
  ansible-playbook -i inventory.ini first-playbook.yaml
  ```
- on manage node, test
  ```
  sudo systemctl status apache2
  
  # access the public ip to check the index.html site
  ```
