Network-Log-Server

Done with <3 by rachyandco at #33C3 with the help of Porcus

observium and nagios


# install using CS

copy cs-userdata file

# install using docker-compose

git clone https://github.com/rachyandco/networklogserver.git
cd networklogserver
docker-compose up -d
docker exec -it networklogserver_observium_1 bash -c '/opt/observium/discovery.php -u'



default Nagios user/passs
nagiosadmin:nagios


default Observium user/passs
ob_admin:ob_pass