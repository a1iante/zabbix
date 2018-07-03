Installation on MaxScale server:

# vim /etc/zabbix/zabbix_agent.d/userparameter_maxscale.conf

	UserParameter=maxscale.syncstate[*],maxadmin show server $	1 | grep "Status" | awk '{print $$2}' | tr -d ','
	UserParameter=maxscale.qmaster,maxadmin show service "Galera Service" | grep "Number of queries forwarded to master" | awk '{print $7}'
	UserParameter=maxscale.qslave,maxadmin show service "Galera Service" | grep "Number of queries forwarded to slave" | awk '{print $7}'
	UserParameter=maxscale.conntime,maxadmin show monitor Galera-Monitor | grep "Connect Timeout" | awk '{print $$3}'
	UserParameter=maxscale.readtime,maxadmin show monitor Galera-Monitor | grep "Read Timeout" | awk '{print $$3}'
	UserParameter=maxscale.writetime,maxadmin show monitor Galera-Monitor | grep "Write Timeout" | awk '{print $$3}'
	UserParameter=maxscale.version[*],maxadmin show server $1 | grep "Server Version" | awk '{print $$3}'
	UserParameter=maxscale.connnum[*],maxadmin show server $1 | grep "Number of connections" | awk '{print $$4}'
	UserParameter=maxscale.packnum[*],maxadmin show server $1 | grep "Number of routed packets" | awk '{print $$5}'
	UserParameter=maxscale.currconn[*],maxadmin show server $1 | grep "Current no. of conns:" | awk '{print $$5}'
	UserParameter=maxscale.corroper[*],maxadmin show server $1 | grep "Current no. of operations:" | awk '{print $$5}'

# systemctl restart zabbix-agent
# maxadmin enable account zabbix

Add a template MaxScale Template.xml to Zabbix 

