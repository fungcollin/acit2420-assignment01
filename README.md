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

### Step 3: Upload an Arch Linux custom image by clicking `Add image`

![Relative](/assets/droplet_003.png)

### 

![Relative](/assets/droplet_004.png)

![Relative](/assets/droplet_005.png)

![Relative](/assets/droplet_006.png)

![Relative](/assets/droplet_007.png)


## Connect using SSH keys

## References
https://wiki.archlinux.org/title/Cloud-init

