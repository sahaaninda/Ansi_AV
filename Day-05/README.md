# Ansible Galaxy - Write less code, Use existing roles from galaxy

- Using Roles from Ansible Galaxy marketplace
- We choose this example: <https://galaxy.ansible.com/ui/standalone/roles/bsmeding/docker/documentation/>
  ```
  # copy the URL from Ansible Galaxy
  ansible-galaxy role install bsmeding.docker

  # gets installed in the following directory
  cd /root/.ansible/roles

  cd /etc/ansible/hosts/
  vim docker-playbook.yaml

  ---
  - hosts: all
    become: true
    roles:
      - bsmeding.docker

  # execute the playbook
  ansible-playbook -i inventory.ini docker-playbook.yaml

  # ssh into control node to verify Docker installation
  ```

