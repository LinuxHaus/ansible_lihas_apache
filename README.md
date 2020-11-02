# ansible_lihas_apache
Installs Apache and does basic configuration

# additional configuration from other roles
## enable apache modules
This role can be called to only enable a few modules from other modules. To do this, call it like this:
```
- name: enable apache modules
  include_role:
    name: lihas_apache
    tasks_from: enable_modules.yml
  include_role:
    name: lihas_apache
  vars:
    apache_modules_enabled: []
```
## deploy and enable apache conf
This role can be called to only enable a few config files from other modules. To do this, call it like this:
```
- name: enable apache conf
  include_role:
    name: lihas_apache
    tasks_from: enable_conf.yml
  include_role:
    name: lihas_apache
  vars:
    apache_conf_enabled: []
```
## deploy and enable apache site
This role can be called to only enable a few sites from other modules. To do this, call it like this:
```
- name: enable apache site
  include_role:
    name: lihas_apache
    tasks_from: enable_site.yml
  include_role:
    name: lihas_apache
  vars:
    apache_site_enabled: []
```
