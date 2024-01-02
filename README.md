# On Master Node ( GitLab-Server )

Ensure an internet connection is available.

```
ping google.com -c 5
```

Change the Hostname for the Server
```
hostnamectl set-hostname GitLab-Server
```

Ensure to update the System

Update the Systme
```
sudo yum upgrade -y
```

Reboot the system
```
reboot
```

Install curl, policycoreutils-python, openssh-server, and perl using the Yum package manager.
```
sudo yum install policycoreutils-python-utils.noarch openssh-server perl curl -y
```

Check the status of the SSH daemon using systemctl.
```
sudo systemctl status sshd
```

Check the status of the firewalld service using systemctl.
```
systemctl status firewalld
```

Download and execute the GitLab repository installation script using curl and install GitLab.
```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash
```

Install GitLab  Server, Called mine is 'http://GitLab-Server'
```
sudo EXTERNAL_URL="http://GitLab-Server" yum install -y gitlab-ee
```

Check the status of the GitLab Server service using systemctl.
```
systemctl status gitlab-runsvdir.service
```

Display the initial root password for GitLab, typically found in the specified file.
```
cat /etc/gitlab/initial_root_password
```

Find your ip and open `Google Chrome`, Use Username `root` and Password from the file 

___
___


# On the Runner Node 

Ensure an internet connection is available.

```
ping google.com -c 5
```

Change the Hostname for the Server
```
hostnamectl set-hostname GitLab-<Dev/Prod>
```

Ensure to update the System

Update the Systme
```
sudo yum upgrade -y
```

Reboot the system
```
reboot
```

Download and execute the GitLab Runner repository installation script using curl.
```
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh" | sudo bash
```

Install GitLab Runner using the Yum package manager.
```
sudo yum install gitlab-runner -y
```

Check the status of the GitLab Runner service using systemctl.
```
systemctl status gitlab-runner.service
```

Install openssh-server using the Yum package manager.
```
sudo yum install openssh-server  -y
```

Check the status of the SSH daemon using systemctl.
```
sudo systemctl status sshd
```

Check the status of the firewalld service using systemctl.
```
systemctl status firewalld
```
___
___


# Register the gitlab-runner on 

Add hosts IPs and Hostname in All Nodes
```
vim /etc/hosts
192.168.1.216 GitLab-Server
192.168.1.78  GitLab-Prod
192.168.1.16  GitLab-Dev
```

Register a GitLab Runner with the specified GitLab instance URL, registration token,

Register the GitLab Runner
```
gitlab-runner register
```
Enter the GitLab instance URL: `http://GitLab-Server`  
Enter the registration token:  `GR1348941nEhqC4jxpTHsxHhS4mqT`  
Enter a description for the runner: `GitLab-Runner-Prod`  
Enter tags for the runner (comma-separated): `prod`  
Enter an executor:  `shell`  



Add the gitlab-runner user to the 'wheel' group, providing necessary permissions.
This command assumes that the 'wheel' group is used for elevated privileges.


```
visudo
usermod -aG wheel gitlab-runner OR 
```
Or Add privileges for only user
```
gitlab-runner        ALL=(ALL)       NOPASSWD: ALL
```
___
___

# Install Docker on GitLab-Runner

Install yum-utils package, which provides utilities for managing Yum repositories and packages.
```
sudo yum install -y yum-utils
```

Add the Docker CE repository to the Yum configuration manager.
```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

Install Docker CE, Docker CLI, containerd.io, docker-buildx-plugin, and docker-compose-plugin using Yum.
```
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

Check the status of the Docker service using systemctl.
```
systemctl enable docker.service
systemctl start docker.service
systemctl status docker.service
```

Run the "hello-world" Docker container to verify the Docker installation.
```
sudo docker run hello-world
```
