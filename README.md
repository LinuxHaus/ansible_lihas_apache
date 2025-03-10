# ansible_lihas_apache
Installs Apache and does basic configuration, can use lihas_dehydrated to request letsencrpt ssl certificates

* local_pages: Makro to direct a domain to a local document root
* external_redirect_domains: Makro to redirect a domain to some other domain
* reverse_proxy: Makro to create reverse proxy for a domain

To run solo:
```
ansible-galaxy install -r requirements.yml
ansible-playbook -i localhost, apache.yml
```
## Role Variables
```
%.config.roles.external_redirect.domains.DOMAINNAME:
  dst: NEWDOMAIN
  method: https, httpok, default https
    # httpok: http stays http, https stays https
%.config.roles.local_pages.domains.DOMAINNAME
  documentroot: DOCUMENTROOT, default: /var/www/html/DOMAINNAME
  phpfpmsocket: Path to PHP-Socket, default /run/php/php-fpm.sock
  pre: []
    array of lines to include in apache configuration before default config
  post: []
    array of lines to include in apache configuration after default config
%.config.roles.rproxy.domains.DOMAINNAME
  target_ip: IP of real host, will de added to /etc/hosts as IP DOMAINNAME
  method: http, https, httpok, default https
    http: target does http only, external rewrite http->https
    https: target does https only, external rewrite http->https
    httpok: http stays http, https stays https
  port: target port for http, default 80, currently only for method http
  pre: []
    array of lines to include in apache configuration before default ProxyPass
  post: []
    array of lines to include in apache configuration after default ProxyPass
%.config.apache.conf.enabled: []
%.config.apache.conf.disabled: []
%.config.apache.module.enabled: []
%.config.apache.module.disabled: []
LIHASVARS.apache.features.httpsrewrite: boolean
  default: true
```

## additional configuration from other roles
### enable apache modules
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
### deploy and enable apache conf
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
### deploy and enable apache site
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
