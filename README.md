# OFSEC-NOTES

OSCP Preparation notes

# SMB Enumeration

SMB - Server Message Block 

1. nmap -v -p 139,445 -oG smb.txt X.X.X.1-254
2. nbtscan -r NETWORK/XX
3. nmap -v -p 139, 445 --script=smb-os-discovery IP_ADDR
4. nmap -v -p 139,445 --script=smb-vuln-ms08-067 --script-args=unsafe=1 IP_ADDR
5. nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse IP_ADDR
6. smbclient -L //IP_ADDR/
7. smbget -R smb://APP_DR/SHARED_FOLDER


# NFS Enumeration

RPCBind 111/TCP

1. nmap -v -p 111 X.X.X.1-254
2. nmap -sV -p 111 --script=rpcinfo X.X.X.1-254
3. nmap -p 111 --script nfs* IP_ADDR
4. Mounting NFS : sudo mount -o nolock IP_ADDR:/home /home/mtn
5. nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount IP_ADDR


# 7.5 SMTP Enumeration

Mail transport protocol - Port 25

1. nc -nv IP_ADDR PORT_N
2

# SNMP Enumeration

161 / UDP

 - Simple network manager protocol
 - Management Information Base (MIB)

 ## Common MIB

	 - 1.3.6.1.2.1.25.1.6.0 System Processes
	 - 1.3.6.1.2.1.25.4.2.1.2 Running Programs
	 - 1.3.6.1.2.1.25.4.2.1.4 Processes Path
	 - 1.3.6.1.2.1.25.2.3.1.4 Storage Units
	 - 1.3.6.1.2.1.25.6.3.1.2 Software Name
	 - 1.3.6.1.4.1.77.1.2.25 User Accounts
	 - 1.3.6.1.2.1.6.13.1.3 TCP Local Ports

1. sudo nmap -sU --open -p 161 X.X.X.1-254 -oG open-snmp.txt
2. snmpwalk -c public -v1 -t 10 IP_ADDR                 #All elements public comunity string
3. snmpwalk -c public -v1 10.11.1.14 1.3.6.1.4.1.77.1.2.25  #Windows users
4. snmpwalk -c public -v1 10.11.1.73 1.3.6.1.2.1.25.4.2.1.2 #Running processes
5. snmpwalk -c public -v1 10.11.1.14 1.3.6.1.2.1.6.13.1.3   #Open TCP Ports
6. snmpwalk -c public -v1 10.11.1.50 1.3.6.1.2.1.25.6.3.1.2 #Installed software
