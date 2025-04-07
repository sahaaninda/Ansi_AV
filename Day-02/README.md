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
