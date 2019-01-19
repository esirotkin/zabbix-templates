This template is designed to monitor the PostgreSQL database server.
The original source for this template is the [2ndQuadrant repository](https://github.com/2ndQuadrant/zabbix_templates).

For this template to work correctly, you need:
* copy the `zabbix_agentd.d/userparameter_postgresql.conf` config to the corresponding directory of Zabbix Agent on the PostgreSQL server;
* create the extension "pg_buffercache" on the PostgreSQL server;
* place the config with zabbix user credentials (`.pgpass`) in the home directory of Zabbix Agent.

If the home directory of the Zabbix Agent is the `/var/run/zabbix` directory, then since it is cleared upon reboot, you will need to automate the copying of the psql passwords file into it.
For example:
```bash
cat << EOF > /etc/rc.local
#!/bin/sh -e

# Zabbix PostgreSQL Access
/bin/cp /path/to/source/.pgpass /var/run/zabbix/.pgpass
/bin/chown zabbix:zabbix /var/run/zabbix/.pgpass
/bin/chmod 600 /var/run/zabbix/.pgpass
/usr/sbin/service zabbix-agent restart

exit 0
EOF
```