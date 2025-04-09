# Ansible Variables and Precedence (Collections)

- Follow _prereq.md_
- To be able to connect to AWS > we need _access_key_ & _secret_access_key_. To keep these data secret and not expose directly into Ansible Playbook/Roles, we use _Ansible-Vault_ to store them
- AWS Console > Top right > Username > Security Credentials > Create Access Key
  
- While creating Vault, configure the vault.pass file. These variables is defined as per the .yaml file
  
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
  cd ec2/tasks
  vim main.yml

  ---
  - name: start an instance with a public IP address
    amazon.aws.ec2_instance:
      name: "ansible-instance"
      # key_name: "prod-ssh-key"
      # vpc_subnet_id: subnet-013744e41e8088axx
      instance_type: t2.micro
      security_group: default
      region: us-east-1
      aws_access_key: "{{ ec2_access_key }}"  # From vault as defined
      aws_secret_key: "{{ ec2_secret_key }}"  # From vault as defined      
      network:
        assign_public_ip: true
      image_id: ami-04b70fa74e45c3917
      tags:
        Environment: Testing
  
    cd /etc/ansible/hosts

    # execute the playbook
    ansible-playbook -i inventory.ini ec2_create.yaml --vault-password-file vault.pass
  ```



- To variabilize >
  
  ```
  # on Role | ec2 > tasks > main.yml
  instance_type: t2.micro

  # can be re-written as
  instance_type: "{{ type }}"
  
  # define the variable in Role | vars > main.yml [can be in defaults too or in-line tasks >   main.yml]
  type : t2.micro
  ```
