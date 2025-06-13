	snmp-server enable
	snmp-server securityip 10.10.11.99
	snmp-server securityip 2001:10:10:11::99
	snmp-server trap-source 10.10.1.2
	snmp-server trap-source 2001:10:10:1::2
	snmp-server engineid 1
	snmp-server user USER2024 GROUP2024 authPriv aes pASS.2024 auth sha pASS.2024
	snmp-server group GROUP2024 authpriv read SKILLS_Ro write SKILLS_Rw
	snmp-server hosT 2001:10:10:11::99 v3 authpriv USER2024
	snmp-server hosT 10.10.11.99 v3 authpriv USER2024
	snmp-server enable traps