## ansible

## Trouble shooting
##### msg: SSL Certificate does not belong to
```
trknight78@sinhyeon-yong-ui-MacBook-Pro:~/Documents/workspace/sua_ansible/sua/ansible(ansible⚡) » ansible-playbook -i devhosts deploy.yml -t python                                                                                                                                                                                                                                                                      2 ↵

PLAY [web] ********************************************************************

GATHERING FACTS ***************************************************************
ok: [web]

TASK: [python | python download] **********************************************
failed: [web] => {"failed": true}
msg: SSL Certificate does not belong to www.python.org.  Make sure the url has a certificate that belongs to it or use validate_certs=False (insecure)

FATAL: all hosts have already failed -- aborting
```

- Solution
__"validate_certs=no"__ 구문을 추가한다.
```
- name: python download
  get_url: url=https://www.python.org/ftp/python/{{ python_version }}/Python-{{ python_version }}.tgz
           dest={{ base_tmp }}/Python-{{ python_version }}.tgz
           validate_certs=no
  environment:
    http_proxy: "{{ http_proxy_url }}"
    https_proxy: "{{ http_proxy_url }}"
  tags: [ python ]
```
