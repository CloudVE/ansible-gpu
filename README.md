Install Nvidia CUDA drivers and toolkit for `containerd` and `rke`.
This playbook assumes Ubuntu 20.04 and a host environment created by CloudMan.

This was tested on AWS G4 instance types.

Before running the playbook, install dependent roles
```
ansible-galaxy install -r requirements.yml -p roles
```

To run, update the `inventory` to include the IP address of the new VM and the
ssh key pair. Then run
```
ansible-playbook -i inventory playbook.yml
```
