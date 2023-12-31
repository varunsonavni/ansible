## Ansible

Ansible: Ansible is an open-source automation tool that is used for configuration management, application deployment, and task automation. It simplifies and streamlines IT operations by allowing you to automate repetitive tasks, manage infrastructure as code, and orchestrate complex workflows. Ansible is often used in DevOps and system administration to improve efficiency, consistency, and scalability in managing IT environments.


Here are some key aspects of Ansible: Push Base Model

Agentless Architecture: Ansible operates in an agentless manner, meaning it doesn't require any software or agents to be installed on the target systems. Instead, Ansible relies on SSH for Linux/Unix systems and WinRM (Windows Remote Management) for Windows systems to communicate and execute tasks remotely.

Ansible Playbooks: Ansible uses YAML-formatted files called "playbooks" to define automation tasks and configurations. Playbooks are human-readable and allow you to describe the desired state of your systems. Playbooks contain a series of roles, tasks, and variables to execute actions on target systems. These playbooks can be version-controlled and shared among team members.

Idempotent Operations: Ansible ensures idempotence, meaning you can run the same playbook multiple times without causing unintended changes or errors. Ansible checks the current state of the system and only applies changes if necessary to bring the system to the desired state.

Inventory: Ansible uses an "inventory" file to define the list of target hosts or groups of hosts on which tasks will be executed. You can configure and organize your inventory to specify hosts' IP addresses, hostnames, SSH credentials, and other necessary information.

Modules: Ansible provides a vast library of built-in modules that cover a wide range of tasks, such as installing software, configuring files, managing users, and more. Modules are the building blocks of playbooks and are responsible for performing specific actions on target systems.

Roles: Roles in Ansible are a way to organize and package playbooks and related files for reuse. They allow you to modularize your automation code, making it easier to maintain and share across different projects.

Ad-hoc Commands: In addition to playbooks, Ansible allows you to run ad-hoc commands on target systems directly from the command line. This is useful for quick tasks and one-time operations.

Extensibility: Ansible can be extended through custom modules and plugins, allowing you to integrate it with various third-party tools and services.

Dynamic Inventory: It is a concept where your ansible configuration file will auto-detect new ec2 instances coming around and will manage it by its own, what to pre-install in that ec2.


### ansible command is use to run ad-hoc ansible task, ansible-playbook command is used to run Ansible Playbook file.

### Run an ad-hoc ansible task.
```
ansible -i inventory all -m "shell" -a "df && ps -aux  &&  echo 'hello'"
```

### copy from  remote to remote location i.e remote /usr/app/file -> /home/user/app_copy
```
ansible -i inventory all -m copy -a "src='/home/ubuntu/ansible/test' dest='/home/ubuntu/xxxxx'" 
```

### copy from local to remote
```
ansible -i inventory all -m copy -a "src='/home/ubuntu/devopsmadeeasy' dest='/home/ubuntu/xxxxx' remote_src=true" -vvv  
```

### Run Ad-hoc command to only some group in inverntory file
```
ansible -i inventory2 webserver -m copy -a "src='/home/ubuntu/devopsmadeeasy' dest='/home/ubuntu/xxxxx' remote_src=true" -vvv  
```

### Run Ansible-playbook with inventory2 file
```
ansible-playbook -i inventory2 firstplaybook.yaml
```

### Dry-Run Ansible-playbook with inventory2 file
```
ansible-playbook -i inventory2 firstplaybook.yaml --check
```

### Run complex Ansible-playbook with ansible galaxy roles. It will create a folder kubernetes.
```
ansible-galaxy role init kubernetes
```


### To check configurations of node like IP, memory, CPU, ami etc .
```
ansible -i inventory all -m setup
```

### To Create a new encrypted playbook.
```
ansible-vault create playbookname.yaml  
After that you need to add a password.
Now If you run cat playbookname.yaml it will show in encrypted format (AES256).
```

### To edit a encrypted playbook.
```
ansible-vault edit playbookname.yaml  
```

### To Change the password for a encrypted playbook.
```
ansible-vault rekey playbookname.yaml  
```

### To encrypt exisiting playbook.
```
ansible-vault encrypt playbookname.yaml  
```

### To decrypt exisiting playbook.
```
ansible-vault decrypt playbookname.yaml  
```