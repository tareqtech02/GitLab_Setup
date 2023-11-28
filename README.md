## On Master Node ( GitLab-Server )

Install curl, policycoreutils-python, openssh-server, and perl using the Yum package manager.
```
sudo yum install -y curl policycoreutils-python openssh-server perl
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

Install GitLab-EE with a specified external URL.
```
sudo EXTERNAL_URL="http://GitLab-Server" yum install -y gitlab-ee
```


Display the initial root password for GitLab, typically found in the specified file.
```
cat /etc/gitlab/initial_root_password
```

___
___


## On the Runner Node 

Download and execute the GitLab Runner repository installation script using curl.
```
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh" | sudo bash
```

Install GitLab Runner using the Yum package manager.
```
sudo yum install gitlab-runner
```

Check the status of the GitLab Runner service using systemctl.
```
systemctl status gitlab-runner.service
```
___
___

## Install Docker on GitLab-Runner

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
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Check the status of the Docker service using systemctl.
```
systemctl status docker
```

Run the "hello-world" Docker container to verify the Docker installation.
```
sudo docker run hello-world
```
___
___
## Register the gitlab-runner on 


Register a GitLab Runner with the specified GitLab instance URL, registration token,

# gitlab-runner register:
Enter the GitLab instance URL: `http://GitLab-Server`  
Enter the registration token:  `GR1348941nEhqC4jxpTHsxHhS4mqT`  
Enter a description for the runner: `gitrunner-prod`  
Enter an executor:  `shell`  



Add the gitlab-runner user to the 'wheel' group, providing necessary permissions.
This command assumes that the 'wheel' group is used for elevated privileges.
```
usermod -aG wheel gitlab-runner
```



Run a Docker container
```
docker run -dit --name web -p 80:80 tareqtech/index01
