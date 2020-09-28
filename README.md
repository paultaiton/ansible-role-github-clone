Role Name
=========
paultaiton.github_clone

Requirements
------------


Role Variables
--------------

		github_username: # github.com user name
		github_token:    # an optional token in github for adding an ssh key. Can be omitted.

		git_name: Paul Aiton
		git_email: paul@example.com

		github_repositories:
			- repo_name: azure  # This will be in github_username  namespace.
				filesystem_location: # example "~/.ansible/collections/ansible_collections/azure/azcollection"
				project_type: python # only python does anything, and activates pip activities.
				pip_requirements_relative_path: # if project_type == python, will look at this path (default requirements.yml, ) for the pip package requirements to install.
				pip_extra_packages: # if defined, list will be passed to pip module to install the packages.
					- ansible
					- azure-cli
				upstream_name: ansible-collections # namespace of upstream repository. Omit to only clone repo from github_username namespace.
				virtualenv: "~/.azcollectiondev_venv"

Dependencies
------------

Example Playbook
----------------

		- name: github_clone paultaiton.azcollection
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
