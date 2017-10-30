Projekt - ZABBIX 3.4
Zabbix slouží k monitorování aktivních síťových prvků, které jsou připojeny do počítačové sítě.
Můžeme sledovat stav a sbírat různé informace o všem, co má IP adresu. 


- seznámení s projektem

  Metody pro sledovaní
- ICMP (https://is.mendelu.cz/eknihovna/opory/zobraz_cast.pl?cast=597)
- SNMP (http://www.samuraj-cz.com/clanek/snmp-simple-network-management-protocol/)
- IPMI (http://www.svetsiti.cz/clanek.asp?cid=IPMI-V20-zjednodusuje-spravu-serveru-28112005)
- JMX
- SSH/Telnet
- XML XPath – extrahuje hodnotu nebo fragment z dat XML pomocí XPath


Proč používat Zabbix? 

Dohledových systému je celá řada. Uvedu zde nejpodstatnější body proč používat dohledový systém Zabbix především z technického hlediska.

- rychlost
- otevřenost (licence GPL)
- přehledné prostředí
- intuitivní ovládání
- živý a rychlý vývoj
- mnohostrannost (možné sledovat prakticky cokoliv)

Agent

Je klientský proces běžící na hostech. Sbírá informace a průběžně je předává serveru.

Zabbix agent

Active checks : agent požádá server o to, co má monitorovat a průběžně serveru odesílá hodnoty všech požadovaných testů
Passive checks : server pošle agentu žádost o data (např. velikost volné paměti). Agent provede požadovaný test a odešle serveru hodnotu
monitoring logů
použití vlastních testů



Zabbix 3.4 Novinky oproti starším modelům

- Přepracovaný dashboard
- Nové možnosti předběžného zpracování dat
- Podpora vzdálených příkazů prostřednictvím Zabbix proxy
- Snadnější správa časových období – pomocí maker
- Vylepšení na straně serveru


1)
Instalace Virtual Boxu
Stažení - Ubuntu server
Stažení Putty - klient ssh
Přidání Zabbix do virtual Boxu.


Úbuntu server 64
u-adam p-adam
name : AdamU





Instalace zabbix
 wget http://repo.zabbix.com/zabbix/3.4/debian/pool/main/z/zabbix-release/zabbix-release_3.4-1+stretch_all.deb
 dpkg -i zabbix-release_3.4-1+stretch_all.deb
 apt-get update
 apt-get install zabbix-server-mysql zabbix-frontend-php
 apt-get install zabbix-proxy-mysql
 zcat /usr/share/doc/zabbix-server-mysql/create.sql.gz | mysql -uzabbix -p zabbix
 zcat /usr/share/doc/zabbix-server-pgsql/create.sql.gz | psql -U <username> zabbix
 zcat /usr/share/doc/zabbix-proxy-mysql/schema.sql.gz | mysql -uzabbix -p zabbix

 zcat /usr/share/doc/zabbix-proxy-pgsql/schema.sql.gz | psql -U <username> zabbix
 zcat /usr/share/doc/zabbix-proxy-sqlite3/schema.sql.gz | sqlite3 zabbix.db
 service apache2 restart
 apt-get install zabbix-agent
 service zabbix-agent start
  
hostname: ZabbixSrv
Name: AdamU
Username: adam
Password: adam
system mail name - Zabbix.adam
ip 192.168.1.212
  
Stáhl jsem si do windows Virtual box , kde jsem si vytvořil nový projekt(Zabbix). Kde jsem nastavil 
Linux , ubuntu 64b , 2048 MB ram a velikost 20 Gb. Nastavil jsem síťový most a změnil adresu.
Pak jsem si stáhl (ubuntu-16.04.3-server-amd64),které jsem vložil do VB, ale jelikož mam 32 b tak to nefungovalo , proto jsem si musel  v BIOSU povolit i 64 b.
Poté jsem ubuntu nakonfiguroval a nainstaloval SSH. Z internetu jsem stahl PUTTTY , abych mohl příkazy kopírovat a nemusel je opisovat.
Putty jsem spustil a nastavil stejnou ip jak na VB, čímž jsem to propojil. Pak jsem pomoci příkazu nainstaloval Zabbix 3.4 a Mysql.
Všechno dělano v rootu. 
 
SNMP

SNMP je jednoduchý, široce rozšířený a užitečný standardizovaný protokol, který slouží k získávání nebo nastavování hodnot na určitém zařízení. Obdobou je například WMI od firmy Microsoft. Podporu SNMP má velká řada zařízení, například aktivní síťové prvky, počítačová čidla, tiskárny, přístupové body nebo pomocí softwaru a ovladačů ji mohou získat osobní počítače a servery. Hodnoty můžeme získávat v pravidelném intervalu a ty pak jednoduše ukládat do databáze spolu s časem a následně vykreslit do grafu. Přehledně tak můžeme zobrazit třeba vytížení procesoru, průběh teploty nebo datový tok na portu přepínače.

Jak SNMP funguje
Protokol SNMP vyžaduje pro komunikaci dvě strany. Jednou entitou je správce (manager) a druhou agent. SNMP pracuje ve dvou režimech činnosti:

Správce posílá dotazy agentovi a přijímá odpovědi. Hodnoty tedy může získávat i více správců a mohou se ptát kdykoliv.
Agent zasílá oznámení (trapy) na adresu správce. V nějakých definovaných situacích (překročení nějaké hodnoty nebo i v pravidelném intervalu) odesílá agent jednomu správci hodnoty.
Protokol SNMP nyní existuje ve třech verzích. SNMPv1 a SNMPv2c používají pro autentizaci community string, v podstatě textové heslo. V SNMPv3 je možno využít autentizaci pomocí jména a hesla a šifrování.

SNMP používá pro komunikaci UDP protokol, díky čemuž je velmi rychlé, ale může dojít ke ztrátě (nedoručení) zasílané informace (paketu). Od verze 2 je implementována kontrola doručení, takže ke ztrátě by nemělo dojít. Standardně se používá port 161 (SNMP) na straně agenta (pro dotazy) a port 162 (SNMPTRAP) na straně serveru (pro trapy). Klient, který posílá dotaz, zvolí dynamický port, z kterého posílá dotaz na port 161. Agent odpovídá z portu 161 na dynamický port klienta. V praxi je pro každý dotaz použit jiný dynamický port.


Nainstalovat a nakonfigurovat Zabbix (klient Zabbix server) do virtual boxu. 
Prozkoumat vazbu Zabbix SNMP a dohlížet os linux - pomoci SNMP.
Prozkoumat JMX modul pro Zabbix a nakonfigurovat vazbu java server Zabbix.
Napsat první skript pro trigger alarm . 
 
