# ansible-grocy
Ansible Playbook for Grocy App on a docker container running on a Raspberry Pi 4 (4GB) with Ubuntu 20.0.4 OS

# clone the repo
```
git clone git@github.com:acarrasquillo/ansible-grocy.git && \
cd ansible-grocy/
```

# 1st time dev station set up (ubuntu)
```
sudo apt install python3-pip python3-venv -qy && \
python3 -m pip install --user --upgrade pip && \
python3 -m pip install --user virtualenv && \
python3 -m venv env && \
source env/bin/activate
```

# Update Pip
```
(venv) pip install --upgrade pip
```

# Install all python required packages for the Ansible playbook
```
pip install -r requirment.txt
```

# Install Ansible roles
```
ansible-galaxy install geerlingguy.docker geerlingguy.pip
```

# Apply on raspberry pi
```
$ ansible-playbook -i hosts.yml master.yml -l prod

PLAY [all] *************************************************************************************************************
TASK [Gathering Facts] *************************************************************************************************ok: [raspberrypi]

TASK [Update apt cache.] ***********************************************************************************************changed: [raspberrypi]

TASK [debug] ***********************************************************************************************************ok: [raspberrypi] => {
    "msg": "deb [arch=arm64] https://download.docker.com/linux/ubuntu focal stable"
}

TASK [geerlingguy.pip : Ensure Pip is installed.] **********************************************************************
changed: [raspberrypi]

TASK [geerlingguy.pip : Ensure pip_install_packages are installed.] ****************************************************
changed: [raspberrypi] => (item={'name': 'docker'})

TASK [geerlingguy.docker : include_tasks] ******************************************************************************
skipping: [raspberrypi]

TASK [geerlingguy.docker : include_tasks] ******************************************************************************
included: /home/ubuntu/.ansible/roles/geerlingguy.docker/tasks/setup-Debian.yml for raspberrypi

TASK [geerlingguy.docker : Ensure old versions of Docker are not installed.] *******************************************
ok: [raspberrypi]

TASK [geerlingguy.docker : Ensure dependencies are installed.] *********************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : Add Docker apt key.] ************************************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : Ensure curl is present (on older systems without SNI).] *************************************
skipping: [raspberrypi]

TASK [geerlingguy.docker : Add Docker apt key (alternative for older systems without SNI).] ****************************
skipping: [raspberrypi]

TASK [geerlingguy.docker : Add Docker repository.] *********************************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : Install Docker.] ****************************************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : Ensure Docker is started and enabled at boot.] **********************************************
ok: [raspberrypi]

RUNNING HANDLER [geerlingguy.docker : restart docker] ******************************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : include_tasks] ******************************************************************************
included: /home/ubuntu/.ansible/roles/geerlingguy.docker/tasks/docker-compose.yml for raspberrypi

TASK [geerlingguy.docker : Check current docker-compose version.] ******************************************************
ok: [raspberrypi]

TASK [geerlingguy.docker : Delete existing docker-compose version if it's different.] **********************************
skipping: [raspberrypi]

TASK [geerlingguy.docker : Install Docker Compose (if configured).] ****************************************************
changed: [raspberrypi]

TASK [geerlingguy.docker : include_tasks] ******************************************************************************
included: /home/ubuntu/.ansible/roles/geerlingguy.docker/tasks/docker-users.yml for raspberrypi

TASK [geerlingguy.docker : Ensure docker users are added to the docker group.] *****************************************
changed: [raspberrypi] => (item=ubuntu)

PLAY RECAP *************************************************************************************************************
raspberrypi                : ok=18   changed=10   unreachable=0    failed=0    skipped=4    rescued=0    ignored=0
```
