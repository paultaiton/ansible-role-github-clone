Role Name
=========
paultaiton.github_clone

Requirements
------------


Role Variables
--------------

    # How to connect to github.
    github_username: # github.com user name, also used for namespace of origin remote.
    github_token:    # an optional token in github for adding an ssh key. Can be omitted.

    # To pass to git config
    git_name:
    git_email:

    # What defines repo parameters to clone and configure locally.
    github_repositories: # list of dicts defining details of clone activity.
      - repo_name: # This will be in github_username namespace.
        filesystem_location: # where to clone locally
        project_type: python # only python does anything, activates pip activities. optional
        pip_requirements_relative_path: # if project_type == python, will look at this path (default requirements.yml, ) for the pip package requirements to install.
        pip_extra_packages: # if defined, list will be passed to pip module to install the packages.
        pip_virtualenv_path: # place on filesystem to use for pip virtualenv.
          - packagename1
          - packagename2
        upstream_name: # namespace of upstream repository. Omit to only clone repo from github_username namespace.

Dependencies
------------

Example Playbook
----------------

    # Example here shows a single repository clone for my own repo fork,
    # https://github.com/paultaiton/azure
    # Forked from and set as remote upstream https://github.com/ansible-collections/azure
    - name: github_clone ansible-collection azure
      hosts: servers
      vars:
        github_username: paultaiton
        github_token: !vault |
        $ANSIBLE_VAULT;1.1;AES256
        123456789
        123456789
        123456789

        git_name: Paul Aiton
        git_email: paul@example.com

        github_repositories:
          - repo_name: azure
            filesystem_location: "~/.ansible/collections/ansible_collections/azure/azcollection"
            pip_requirements_relative_path: requirements-azure.txt
            pip_extra_packages:
              - ansible
              - azure-cli
            project_type: python
            upstream_name: ansible-collections
            virtualenv: "~/.azcollectiondev_venv"
      roles:
         - paultaiton.github_clone

License
-------
GPL 3.0 or later.

Author Information
------------------
@paultaiton on github.
