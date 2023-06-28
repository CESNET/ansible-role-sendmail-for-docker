# cesnet.sendmail_for_docker
Ansible role cesnet.sendmail_for_docker configuring Sendmail usable from Docker containers.

It installs sendmail MTA and configures it to listen on all IP addresses and to accept SMTP messages
coming from a specified Docker subnet.

Role Variables
--------------

- **sendmail_for_docker_hostname** - the hostname to be set for the machine, it appears in the MIME headers in outgoing emails
- **sendmail_for_docker_bridge_network_name** - the name of Docker bridge network that should be able to send emails, it is added to /etc/hosts, default is perun_net 
- **sendmail_for_docker_config** - arbitrary lines to be added to /etc/mail/sendmail.mc, default is empty

Example Playbook
----------------
```yaml
- hosts: all
  roles:
    - role: cesnet.sendmail_for_docker
      vars:
        sendmail_for_docker_hostname: my-server.example.org
        sendmail_for_docker_bridge_network_name: perun_net
        sendmail_for_docker_bridge_network_gateway: 192.168.0.1
        sendmail_for_docker_config: |
          dnl # define relay.muni.cz as relay receiving ESMTP protocol on TCP port 25 
          define(`SMART_HOST', relay.muni.cz)dnl
          define(`RELAY_MAILER',`esmtp')dnl
          define(`ESMTP_MAILER_ARGS', `TCP $h 25')dnl
```
