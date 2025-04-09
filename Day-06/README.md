# Ansible Variables and Precedence (Collections)

- Follow _prereq.md_
- To be able to connect to AWS > we need _access_keys_ & _secret_id_. To keep these data secret and not expose directly into Ansible Playbook/Roles, we use _Ansible-Vault_ to store them
- Create a yaml and role
  ```
  vim ec2_create.yaml

  ---
  - hosts: localhost
    connection: local
    roles:
      - ec2

  # create a role
  ansible-galaxy role init ec2
  
  ```
