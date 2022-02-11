# Install Ansible Docker
In your Jumpbox, run `sudo docker pull cyberxsecurity/ansible`
Once docker container installs, attach shell

## Review following variables - The following files should already be present in dir: /etc/ansible

### Config File (ansible.cfg)
Line: 107 - remote_user = 'yourusername'

### Host File (hosts)
Line: 25 - match private IPs to your network
Line: 30 - match private IP to elk server