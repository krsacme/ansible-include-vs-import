
A repository to demonstrate the difference in using vars with `include_role`
and `import_role`.

Usage
=====

```
git clone https://github.com/krsacme/ansible-include-vs-import.git
cd ansible-include-vs-import
ansible-playbook -vv import.yaml
ansible-playbook -vv include.yaml
```

import
=====
When using vars in `import_role` like below, the vars are applied globally
to the whole play.

```
- name: play1
  hosts: test
  tasks:
    - debug: var=test_role_var1
    - import_role:
        name: test-role
      vars:
        test_role_var1: 'test_var1_local'

- name: play2
  hosts: test
```

Here, in `play1` the variable `test_role_var1` will have the value as
`test_var1_local` for the whole play. Though it will not affect `play2`.

include
=======
In order to apply the var only to a specific role and not to the entier play,
use `include_role`.

```
- name: play1
  hosts: test
  tasks:
    - debug: var=test_role_var1
    - include_role:
        name: test-role
      vars:
        test_role_var1: 'test_var1_local'

- name: play2
  hosts: test
```
Here, the first debug of variable `test_role_var1` with print undefined
variable, as this variable will be applied only to the role.
 
