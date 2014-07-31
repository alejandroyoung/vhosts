vhosts
======
```

Example playbook
----------------
```yaml
    ---
    - hosts: web
      vars_files:
        - vhosts/vars/main.yml
        - vhosts/vars/{{ ansible_os_family }}.yml
      roles:
        - vhosts
```

Where vars/main.yml contains:
```yaml
   ---
   vhost_parent_root: '/var/www/vhosts'
   vhosts:
       - { site_url: 'site1.com', vhost_home: '{{ vhost_parent_root }}/site1.com', sftp_user: 'site1', sftp_pass: 'sha_512_password' }
       - { site_url: 'site2.com', vhost_home: '{{ vhost_parent_root }}/site2.com', sftp_user: 'site2', sftp_pass: 'sha_512_password' }
```

You can specify as many sites as required.

Password hashing
----------------

Note that the 'sftp_pass' variable takes a hash that is inserted directly into /etc/shadow.
You can use:
```bash
python -c "from passlib.hash import sha512_crypt; print sha512_crypt.encrypt('password')"
```

Todo
----
- Need to add support for Ubuntu versions < 14
- Build in password hashing
