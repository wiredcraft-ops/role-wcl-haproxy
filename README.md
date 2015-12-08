role-wcl-haproxy
================

This Ansible Role install and configure haproxy. Strongly based on https://github.com/kefniark/ansible-haproxy-role
Some modification in the way the template are managed.

Documentation:
-------------------------

To see all available options, you can look to the [Documentation](https://github.com/kefniark/ansible-haproxy-role/blob/master/docs/main.yml).

This project also contains two examples :
 - A reverse proxy for a pre installed web server : [Exemple 1](https://github.com/kefniark/ansible-haproxy-role/blob/master/docs/exemple-simple-server.yml)
 - A load balancer in front of web servers : [Exemple 2](https://github.com/kefniark/ansible-haproxy-role/blob/master/docs/exemple-loadbalancer.yml)

To make this Role more reusable, it contains 3 different tags :
 - haproxy_install : install haproxy on the host (apt/yum/...)
 - haproxy_configure : task which create the /etc/haproxy/haproxy.cfg
 - haproxy_service : tasks used to start/reload the service when there is a modification

Example Playbook
-------------------------

```yaml
- hosts: all
  remote_user: root
  roles:
   - role: haproxy
     haproxy_frontends:
     - name: loadbalancer
       bind: '*:8080'
       default_backend: webserver
     haproxy_backends:
     - name: webserver
       servers:
        - name: backend1
          ip: localhost
          port: 80
```

More Informations
-------------------------

Author: Destrem Kevin

This project is still in development and lot options are missing or not supported.
