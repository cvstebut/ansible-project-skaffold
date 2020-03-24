-- Work in progress - experimental -- 

# Ansible project skaffold for using molecule during playbook development and testing

This repo is my current attempt for my "standard" project structure developing playbooks. The aim is to use molecule while developing and testing the playbook.

It should also allow me to use travis-ci to run tests, but as of now I have not tested whether this actually works.

## Notes

### No roles are stored in "./roles", only a requirements.yml

This mirrors the way I use it in awx/Tower. The roles are dynamically imported using galaxy. 

Molecule also takes care of importing the role to the "correct" path while testing, so I do not have to manually bother settings the search path for roles.

Snippet from ./molecule/default/molecule.yml
```yaml
dependency:
  name: galaxy
  options:
    role-file: roles/requirements.yml
```


## Point molecule converge at playbook under test

During dev cycle I like to use the standard molecule verbs to exercise and test my playbook. My current way of doing this is pointing ```molecule converge``` at my playbook-under-test by modifying molecule.yml:

```yaml
provisioner:
  name: ansible
  playbooks:
    converge: ../../playbooks/init_dev_environment.yml
```

## License

Apache 2