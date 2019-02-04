# ansible-simple-demo
Extremely basic playbook and role demo.

* The 'demo.yml' playbook contains a single play
* This play has a task block to include the 'demo' role.
* This block also has a tag that can be called or skipped
* This block also has a conditional with a variable that can be used to skip
* The role is a debug statement with a variable

## Call demo playbook
```
[vvaldez@localhost ansible-simple-demo]$ ansible-playbook demo.yml 
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does
not match 'all'


PLAY [Demo Play] **********************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [localhost]

TASK [include_role : demo] ************************************************************************************

TASK [demo : debug] *******************************************************************************************
ok: [localhost] => {
    "msg": "Hello World from Ansible, variable is: 'my_data'"
}

PLAY RECAP ****************************************************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0   
```

## Change the variable with the -e (extra-vars) option
```
[vvaldez@localhost ansible-simple-demo]$ ansible-playbook demo.yml -e my_variable=test
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does
not match 'all'


PLAY [Demo Play] **********************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [localhost]

TASK [include_role : demo] ************************************************************************************

TASK [demo : debug] *******************************************************************************************
ok: [localhost] => {
    "msg": "Hello World from Ansible, variable is: 'test'"
}

PLAY RECAP ****************************************************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0   
```

## Set the variable 'demo' to False which will prevent the role from running
```
[vvaldez@localhost ansible-simple-demo]$ ansible-playbook demo.yml -e my_variable=test -e demo=False
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does
not match 'all'


PLAY [Demo Play] **********************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [localhost]

TASK [include_role : demo] ************************************************************************************
skipping: [localhost]

PLAY RECAP ****************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0   
```

## Skip the demo tag which will prevent the role from running
```
[vvaldez@localhost ansible-simple-demo]$ ansible-playbook demo.yml -e my_variable=test --skip-tags=demo
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does
not match 'all'


PLAY [Demo Play] **********************************************************************************************

TASK [Gathering Facts] ****************************************************************************************
ok: [localhost]

PLAY RECAP ****************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0   
```
