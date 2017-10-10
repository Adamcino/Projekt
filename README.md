Projekt - ZABBIX
Zabbix slouží k monitorování aktivních síťových prvků, které jsou připojeny do počítačové sítě.
Můžeme sledovat stav a sbírat různé informace o všem, co má IP adresu. 


- seznámení s projektem

  Metody pro sledovaní
- ICMP (https://is.mendelu.cz/eknihovna/opory/zobraz_cast.pl?cast=597)
- SNMP (http://www.samuraj-cz.com/clanek/snmp-simple-network-management-protocol/)
- IPMI (http://www.svetsiti.cz/clanek.asp?cid=IPMI-V20-zjednodusuje-spravu-serveru-28112005)
- JMX
- SSH/Telnet




1)
Instalace Virtual Boxu
Stažení - Ubuntu server
Stažení Putty - klient ssh
Přidání Zabbix do virtual Boxu. ( Pomocí youtube )


Úbuntu server 64
u-adam p-adam
name : AdamU


Instalace zabbix
# wget http://repo.zabbix.com/zabbix/3.4/debian/pool/main/z/zabbix-release/zabbix-release_3.4-1+stretch_all.deb
# dpkg -i zabbix-release_3.4-1+stretch_all.deb
# apt-get update
# apt-get install zabbix-server-mysql zabbix-frontend-php
# apt-get install zabbix-proxy-mysql
# zcat /usr/share/doc/zabbix-server-mysql/create.sql.gz | mysql -uzabbix -p zabbix
# zcat /usr/share/doc/zabbix-server-pgsql/create.sql.gz | psql -U <username> zabbix
# zcat /usr/share/doc/zabbix-proxy-mysql/schema.sql.gz | mysql -uzabbix -p zabbix

# zcat /usr/share/doc/zabbix-proxy-pgsql/schema.sql.gz | psql -U <username> zabbix
# zcat /usr/share/doc/zabbix-proxy-sqlite3/schema.sql.gz | sqlite3 zabbix.db
# service apache2 restart
# apt-get install zabbix-agent
# service zabbix-agent start


