# Creating a Remote Server with Digital Ocean
This guide will take you step by step on creating an Arch Linux server on DigitalOcean. We will generate SSH keys, create a droplet, and configure the droplet using a cloud-init file for user creation, package installation, and SSH configration.
<p> By the end, you will have learned to create and configure a secure Arch Linux server. </p>

## 1: Create SSH Keys
### What is a SSH Key?
<p> A SSH key is to provide secure, password less authentication to access your server. They are an alternative security to passwords. </p>

## Keynotes
* Ensure you have .ssh directory in your home directory.
* MacOS and Windows will have different commands and will be listed respectively in this order. 

### Step 1
<p> Open terminal and run the command below: </p>

![Relative](/ssh-key01.png)
<p>This command would generate a SSH key using the ed25519 algorithm. 
Save the key to the default location when prompted. </p>

##
<tab<tab>test copy

