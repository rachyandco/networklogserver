Network-Log-Server

Done with <3 by rachyandco at #33C3 with the help of Porcus.

Quick install of observium and nagios instances on the same VM. Tested on https://exoscale.ch.


# install using CloudStack

	copy cs-userdata file in the exoscale interface.

# install using docker-compose

	git clone https://github.com/rachyandco/networklogserver.git

	cd networklogserver

	docker-compose up -d

	docker exec -it networklogserver_observium_1 bash -c '/opt/observium/discovery.php -u'

# access to the web interfaces

	Nagios: http://IP_OF_SERVER:8001

	default Nagios credentials: nagiosadmin:nagios

	Observium: http://IP_OF_SERVER:8000

	default Observium credentials: ob_admin:ob_pass


# add VM to Observium

## on the distant VM

This is for reference only. On each VM to be monitored, install snmpd.

	sudo apt-get install snmpd

Replace the config file with the one suggested here. You need to edit the IP_OF_OBSERVIUM and the SECRET.

	sudo mv /etc/snmp/snmpd.conf /etc/snmp/snmpd.conf.orig
	sudo nano /etc/snmp/snmpd.conf
	(paste your config)
	sudo service snmpd restart

## on the Networklogserver VM

Add the distant VM in the host file. Edit /etc/hosts and add:

	DISTANT_VM DISTANT_VM_IP

Add the distant VM to observium:

	docker exec -it networklogserver_observium_1 bash -c '/opt/observium/add_device.php -p DISTANT_VM SECRET v2c'


# Links

	- http://www.observium.org - Observium project
	- https://www.nagios.org - Nagios project
	- https://github.com/henningkessler/observium - Observium Docker image by henningkessler
	- https://github.com/JasonRivers/Docker-Nagios - Nagios Docker image by JasonRivers