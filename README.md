[![Latest Release](https://img.shields.io/github/release/andock/environment.svg?style=flat-square)](https://github.com/andock/andock/releases/latest) [![Build Status](https://img.shields.io/travis/andock/andock.svg?style=flat-square)](https://travis-ci.org/andock/environment)

andock.environment
=========

**andock.environment** is a Ansible role which:
* Checks out or pull a repository (e.g. from github) based on project and branch
* Configure docsal based on branch.domain (e.g. master-build.myproject.mydomain.de)
* Runs "fin up" 
* Runs init hook (configurable through hooks/init_tasks.yml)
* Runs update hook (configurable through hooks/update_tasks.yml)
* Runs test hook (configurable through hooks/test_tasks.yml)
* Runs "fin stop"
* Runs "fin rm"
* Clears the instance
  
**The livecycle can be controlled with tags**
* Clears the instance
Requirements
------------

In order to build your apps with Andock, you will need:

* Ansible
* Docksal
* git on both machines


Role Variables
--------------

```yaml
vars:
  git_artifact_repository_path: https://github.com/andock/demo-project.git
  project_name: demo-project-name
  project_id: demo-project
  branch: "master"
  mounts:
    files:
      path: docroot/files

  virtual_hosts:
    default:
      virtual_host: "{{ branch }}.demo-project-fin.docksal"
      container: web
    sub:
      virtual_host: "{{ branch }}.demo2-project-fin.docksal"
      container: web
  hook_init_tasks: "hooks/init_tasks.yml"
  docksal_env:
    XDEBUG_ENABLED: "0"
  hook_init_tasks: "hooks/init_tasks.yml" #Task file for the project init. Run site-install here.  
  hook_update_tasks: "hooks/update_tasks.yml" #Task file for the project init. Run site-install here.
  hook_deploy_done: "hooks/deploy_done_tasks.yml" #Task file after deployment was done.
  hook_deploy_failure: "hooks/hook_deploy_failure.yml" #Task file after deployment failed.

```

Installation
------------

Andock is an Ansible role distributed globally using [Ansible Galaxy](https://galaxy.ansible.com/). In order to install Andock role you can use the following command.

```
$ ansible-galaxy install andock.environment
```

Update
------

If you want to update the role, you need to pass **--force** parameter when installing. Please, check the following command:

```
$ ansible-galaxy install --force andock.environment
```

Dependencies
------------

@TODO

Example Playbook
----------------

@TODO

License
-------

BSD

Author Information
------------------

Christian Wiedemann (christian.wiedemann@key-tec.de)
