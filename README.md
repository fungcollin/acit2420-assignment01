# Creating a Remote Server with Digital Ocean
This guide will take you step by step on creating an Arch Linux server on DigitalOcean. We will generate SSH keys, create a droplet, and configure the droplet using a cloud-init file for user creation, package installation, and SSH configration.
<p> By the end, you will have learned to create and configure a secure Arch Linux server. </p>

## 1: Create SSH Keys
### What is a SSH Key?
<p> A SSH key is to provide secure, password less authentication to access your server. They are an alternative security to passwords. </p>

### __Keynotes:__
* Ensure you have `.ssh` directory in your home directory.
* Using DigitalOcean web to create and setup a Arch Linux droplet

### Step 1:
<p> Open terminal and run the command below: </p>

```bash
ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"
``` 

<p>This command would generate a SSH key using the ed25519 algorithm. 
Save the key to the default location when prompted. 

* `ssh-keygen`: command for generating SSH keys</br>
* `~`:  represents current user's home directory</br> 
* `-f`: represents filename and file path</br>
* `-t` represents algorithsm to encrpyt</br> 
* `-c`: represents a comment to the key</br>
</p>
<p>If the above command does not work, you may need to enter the full path:</br></p>

```bash
ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"
```
Upon successful generation of the SSH key, you will get this response: 

![Relative](/assets/ssh_001.png)

### Step 2: Navigate to .ssh directory
```bash
cd ~/.ssh
```

### Step 3: Use ls to list all files within the .ssh directory ensuring that do-key and do-key.pub was created successfully and avaliable
```bash
ls
```
![Relative](/assets/ssh_002.png)

*  `do-key` is a private key (__DO NOT__ share this).
* `do-key.pub` is a public key (Share this and use for the server).

## Upload Arch Linux image and setup `cloud-init` on DigitalOcean web

### Step 1: Click on `Droplets` in the drop down menu, `Create`:

![Relative](/assets/droplet_001.png)

### Step 2: Select a datacenter that is nearets to your designated region: 

![Relative](/assets/droplet_002.png)

### Step 3: Upload an Arch Linux custom image by clicking `Add image`:

![Relative](/assets/droplet_003.png)

### Step 4: Select `Upoad Image` of chosen Arch Linux image:

![Relative](/assets/droplet_004.png)

### Step 5: Select Droplet Type and CPU options of choice:

![Relative](/assets/droplet_005.png)

### Step 6: Add SSH Key by selecting the `SSH Key` authentication method:

![Relative](/assets/droplet_006.png)

### Step 7: Enter the below code to `Add Initialization scripts` under `Advanced Options`:
```bash
#cloud-config
users:
  - name: user-name #change me
    primary_group: group-name #change me
    groups: wheel
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-ed25519 ...

packages:
  - ripgrep
  - rsync
  - neovim
  - fd
  - less
  - man-db
  - bash-completion
  - tmux

disable_root: true
```
Be sure to change your `user-name`, `group-name`, and enter the created `ssh-authorized-keys

`Users` specify we are adding a user

* `name` specify username

* `primary_group` specifies the primary group

* `groups` specify additional group

* `sudo: ['ALL=(ALL) NOPASSWD:ALL']` allows a user unrestricted sudo access

* `shell` specifies the path of the shell

* `ssh-authorized-keys` specifies the keys that are added to the user's authorized keys file

* `ssh-ed25519 <Your Public Key> <Your Email>` is your public key

* `packages` specify installing the following packages on the first boot

* `disable_root: true` specify we disable connect to the droplet via SSH as root user
</br>


![Relative](/assets/droplet_007.png)



## Connect using SSH keys

### Step 1: Copy the Droplet's IPv4 Address from Digital Ocean
### Step 2: Open your terminal and run the command:
```bash
ssh -i ~/.ssh/id_ed25519 <user-name-here>@<ip-address-here>
```
### Step 3: Connect to the drop using the command:
```bash
ssh <hostname>
```

## References
[Cloud-Init Set-up](https://wiki.archlinux.org/title/Cloud-init)</br>
[Cloud Configuration for Intial Server Setup](https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup)</br>
[SSH Connection](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server)