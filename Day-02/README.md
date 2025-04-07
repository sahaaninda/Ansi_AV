# How to setup Passwordless Authentication

**A**. Control Node > Manage Node via _SSH key_ <br/>
**B**. Control Node > Manage Node via _Password_
**C**. Control Node > Manage Node via manually copying _public key_

Two EC2 Instances have been setup on AWS

**A.**

Setup Passwordless Authentication using SSH Keys on Node-A

- On the control node, copy and save the _awskey.pem_ file
- Control Node > go to the directory where the key file is located

```
chmod 600 awskey.pem
ssh-copy-id -f "-o IdentityFile awskey.pem" ubuntu@54.146.181.156

# e.g. ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>

# connect with the Manage Node-A
ssh ubuntu@54.146.181.156
```

**B.**

Connect with Manage Node-B via Password

- Connect to the EC2 instance [Node-B] using aws key
  ```
  ssh -i awskey.pem ubuntu@54.163.155.60
  ```
- On Node B >
  ```
  sudo vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf

  # set the following to "yes"
  PasswordAuthentication yes

  # restart SSH service
  sudo systemctl restart ssh

  # set a password for user ubuntu
  sudo passwd ubuntu

  # connect with the Manage Node-B
  # it'll ask and save password the first time
  ssh-copy-id ubuntu@54.163.155.60
  ssh ubuntu@54.163.155.60
  ```
- If you're not using EC2 Instances, on any Linux machine >
  ```
  sudo vim /etc/ssh/sshd_config
  # set/uncomment the following to "yes"
  PasswordAuthentication yes

  # restart SSH service
  sudo systemctl restart ssh

  # set a password for user ubuntu
  sudo passwd ubuntu

  # connect with the Manage Node-B
  # it'll ask and save password the first time
  ssh-copy-id ubuntu@54.163.155.60
  ssh ubuntu@54.163.155.60
  ```


**C.**

```
# on the control node [Ubuntu], install ansible
sudo apt update
sudo apt upgrade
sudo apt install ansible
ansible --version

# Create public-private key-pair
# 3 files will be created: authorized_keys, id_rsa, id_rsa.pub
ssh-keygen

sudo apt update && sudo apt install python3 python3-pip -y
pip3 --version
sudo pip3 install --upgrade ansible
ansible --version
```

```
# on the manage node [Ubuntu], create keygen
ssh-keygen

# navigate to the folder where the keys were generated
# copy the "id_rsa.pub" file content from node machine
# paste the public key on target machine > "authorized_keys" file
chmod 600 authorized_keys

sudo apt update && sudo apt install python3 python3-pip -y
sudo apt install python3-six -y
```

```
# on the control node, try ssh
# shall be able to login without any password
ssh ubuntu@34.235.115.x
```
