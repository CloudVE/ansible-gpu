Install Nvidia Cuda drivers, Docker, and Nvidia Docker runtime.
This was tested on AWS G4 instance types.

Before running the playbook, install dependent roles
```
ansible-galaxy install -r requirements.yml -p roles
```

The `nvidia_docker` role requires a couple of modifications. Edit
`handlers/main.yml` to set
```
state: restarted
```

Then, edit `tasks/ubuntu-pre-install.yml` to specify additional packages in the
`install packages` task that are required for K8s:

```
- name: install packages
  apt:
    name:
      - nvidia-container-runtime
      - nvidia-container-toolkit
      - nvidia-docker2
    state: present
    update_cache: yes
  notify: reload docker
  environment: "{{proxy_env if proxy_env is defined else {}}}"
```

To run, update the `inventory` to include the IP address of the new VM and the
ssh key pair. Then run
```
ansible-playbook -i inventory playbook.yml
```
