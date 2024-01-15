Install and configure WireGuard
=========

This role installs and configures WireGuard and wg-dashboard for my server.

Role Variables
--------------

The ```wireguard_dashboard_password``` variable is the password for the wg-dashboard web interface user.

The ```wireguard_host_address``` variable is the internal IP address of the wireguard server within the wireguard network.

The ```wireguard_peers``` variable is a list of dictionaries containing the public key and allowed IPs for each peer.

The ```wireguard_private_key``` variable can be set to the private key for the wireguard server. If this variable is not set, a private key will be generated if nessesary.

The ```wireguard_dashboard_user``` variable is the username for the wg-dashboard web interface admin user.

```wireguard_dashboard_port``` can be set to change the port that wg-dashboard.

```wireguard_port``` can be set to change the port that wireguard listens on.

The ```wireguard_interface_name``` variable can be set to change the name of the wireguard interface to create multiple wireguard interfaces.

```wireguard_global_dns``` can be set to change the default DNS server filled in by wireguard dashboard.

Requirements
----------------

Needs Python3 and git to be installed.

Example Playbook
----------------

```yaml
    - hosts: servers
      vars:
        wireguard_dashboard_password: password123
        wireguard_host_address: 10.6.0.1/32
        wireguard_peers:
          - public_key: 1234567890
            allowed_ips: 10.6.0.2/32
          - public_key: 1234567890
            allowed_ips: 10.6.0.3/32

      roles:
         - { role: tychobrouwer.wireguard }
         - { role: tychobrouwer.wireguard, wireguard_dashboard_user: "admin", wireguard_private_key: {{ wireguard_private_key }},
             wireguard_dashboard_port: 10086, wireguard_port: 51820, wireguard_interface_name: wg0, wireguard_global_dns: 1.1.1.1 }
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
