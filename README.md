# ansible-grocy
Ansible Playbook for Grocy App on Ubuntu 20.4

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
