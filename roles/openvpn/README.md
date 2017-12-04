OpenVPN
=========

This role installs OpenVPN and configures it as a client.

Tested OS:
* Ubuntu Xenial (16.04)

Requirements
------------

OpenVPN must be available as a package in APT repository.

Role Variables
--------------

| Variable                 | Default           | Comment                                   |
| ------------------------ | ----------------- | ----------------------------------------- |
| openvpn_cache_valid_time | 86300             | APT cache valid time                      |
| openvpn_port             | 2195              | The port OpenVPN client should connect to |
| openvpn_proto            | udp               | OpenVPN client protocol                   |
| openvpn_server_hostname  | 8.8.8.8           | Remote VPN endpoint                       |
| openvpn_version          | 2.3.10-1ubuntu2.1 | OpenVPN package version                   |
| openvpn_ca_cert          |                   | CA certificate                            |
| openvpn_client_cert      |                   | Client certificate                        |
| openvpn_private_key      |                   | Private key                               |
| openvpn_tls_auth         |                   | TLS-auth key                              | 

Dependencies
------------

Doesn't depend on any other roles.

Example Playbook
----------------

	- hosts: all
	  become: true
	  gather_facts: false
	  pre_tasks:
	  - name: Install python2 for Ansible
	    raw: bash -c "test -e /usr/bin/python || (apt -qqy update && apt install -qqy python-minimal)"
	    register: output
	    changed_when: output.stdout != ""

	- hosts: openvpn_target
	  name: OpenVPN playbook
	  roles:
	  - openvpn

License
-------


Author Information
------------------

