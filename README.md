## On Master Node ( GitLab-Server )

# Install curl, policycoreutils-python, openssh-server, and perl using the Yum package manager.
	sudo yum install -y curl policycoreutils-python openssh-server perl

# Check the status of the SSH daemon using systemctl.
	sudo systemctl status sshd

# Check the status of the firewalld service using systemctl.
	systemctl status firewalld

# Download and execute the GitLab repository installation script using curl and install GitLab.
	curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash

# Install GitLab-EE with a specified external URL.
	sudo EXTERNAL_URL="http://GitLab-Server" yum install -y gitlab-ee

# Display the initial root password for GitLab, typically found in the specified file.
	cat /etc/gitlab/initial_root_password

