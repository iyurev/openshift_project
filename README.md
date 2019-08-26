# COMING SOON....


Role Name
=========

Create or apply changes for OpenShift project 

Requirements
------------

```pip install openshift``` 

For Ansible AWX  you should create new  python virtual environment,  then install kubernetes client packages and his dependencies, 
current requirements.txt from AWX 6.0.0.0 :

```
dictdiffer
jinja2
kubernetes >= 8.0.0, < 9.0.0
urllib3 < 1.25
python-string-utils
ruamel.yaml >= 0.15
six
```

Role Variables
--------------
Description of most "interesting" role variables: 

```egressips``` - list  of EgressIP for  a project
```project_for_postgres```  - create dedicated service account and  SCC for its, it's allowing run postgresql pod 
with any UID .   
```allow_from_projects``` - allow  ANY network traffic from projects in this list
```labels``` - project labels list 
```default_router``` - default value is ```yes``` - it's adding label ```default-router: "yes"``` to project.   
```apply_limit_and_quota_only``` - if ```yes``` - include tasks only for configure project quota . 
 


Example Playbook
----------------

Example playbook :

```
- name: Create (or update ) openshift project
  hosts: "{{ project_list }}"
  gather_facts: no

  tasks:

    - include_role:
        name: openshift_project
      vars:
        project_name: "{{ inventory_hostname }}"

```


Where ```project_list ``` - is ansible inventory host list , variables for every project stored in his host_vars 
file .  

NOTICE!! For ansible group ```all``` - you must configure variable ```ansible_connection: local``` for running all 
tasks on controller machine .  



License
-------

BSD

Author Information
------------------

Igor Yurev  

idyurev@gmail.com 
