##Master Node ( GitLab-Server )

sudo yum install -y curl policycoreutils-python openssh-server perl

sudo systemctl status sshd

systemctl status firewalld

curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash

192.168.1.216 GitLab-Server
192.168.1.78  GitLab-Prod
192.168.1.16  GitLab-Dev

sudo EXTERNAL_URL="http://GitLab-Server" yum install -y gitlab-ee

cat /etc/gitlab/initial_root_password


## Add in Windws
c:\Windows\System32\Drivers\etc\hosts
192.168.1.216 GitLab-Server



stages:
	  - build
Tasks1:
	   stage: build
	   script:
		        - logger "Hello From GitLab Stage 'Build'"
