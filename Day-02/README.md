# How to setup Passwordless Authentication

**A**. Control Node > Manage Node via _SSH key_ <br/>
**B**. Control Node > Manage Node via _Password_

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

  # connect with the Manage Node-B
  # it'll ask and save password the first time
  ssh-copy-id ubuntu@54.163.155.60
  ssh ubuntu@54.163.155.60
  ```

