# Ansible Variables and Precedence (Collections)

- Follow _prereq.md_
- To be able to connect to AWS > we need _access_key_ & _secret_access_key_. To keep these data secret and not expose directly into Ansible Playbook/Roles, we use _Ansible-Vault_ to store them
- AWS Console > Top right > Username > Security Credentials > Create Access Key
- While creating Vault, configure the vault.pass file. This variable is defined as per the .yaml file
  ```
  ec2_access_key: <access_key>
  ec2_secret_key: <secret_access_key>
  ```
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
  cd /etc/ansible/hosts

  # execute the playbook
  ansible-playbook -i inventory.ini ec2_create.yaml --vault-password-file vault.pass
  ```
