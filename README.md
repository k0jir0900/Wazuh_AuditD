# Wazuh_AuditD
 AuditD monitoring with Wazuh

The following setup is for using AuditD with Wazuh. The base configuration of the audit rules (audit.rules) is based on the file published by Florian Roth at https://github.com/Neo23x0/auditd/blob/master/audit.rules. 

The file was modified to include the audit-keys needed by Wazuh for reading logs and a rule for Webshell detection was added.

## Installation

### Ubuntu/Debian


Install AuditD

    sudo apt-get install -y auditd

Edit the AuditD base configuration file in the following path

    vi /etc/audit/rules.d/audit.rules

Paste the contents of the audit.rules file and then restart the service.

    systemctl auditd restart

### Wazuh Agent

Edit the configuration file ossec.conf. For this, edit the file of the following path. and 

    vi /var/ossec/etc/ossec.conf

In the "localfile" section add the lines that appear in ossec.conf and then restart the service.

    systemctl wazuh-agent restart

### Wazuh Manager

In order for Wazuh to properly recognize the audit logs, audit-keys must be added. For this, edit the file of the following path.

    vi /var/ossec/etc/lists/audit-keys

Paste the contents of the audit-keys file and then restart the service.

    systemctl wazuh-manager restart


### Important

If you cannot see all the auditd events, you should modify the configuration of /var/ossec/ruleset/rules/0365-auditd_rules.xml so that the rules have at least alert level 3
