# ansibleborn
---
- hosts: webserver
  tasks:
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest
        
    - copy:
        src: /ansible/myansible.html
        dest: /var/www/html/myansible.html

    - name: Adding mod_rewrite
      apache2_module: name=rewrite state=present
      notify:
        - restart apache2

    - name: clone my ansible born
      git: repo=https://github.com/newtechs19/ansibleborn.git dest=/var/www/html/myansible update=no
