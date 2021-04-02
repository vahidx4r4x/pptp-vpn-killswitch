#!/bin/bash
clear
echo 'Welcome to the pptp VPN Kill Switch!'
echo 
echo 'Please Select your Option:'
echo 
echo "	1) Current iptables Status"
echo "	2) Turn ON VPN Kill Switch"
echo "	3) Turn OFF VPN Kill Switch"
echo 
read -p "Option Number[1]: " option
until [[ -z "$option" || "$option" =~ ^[123]$ ]]; do
		echo "$option: invalid selection."
		read -p "Option Number[1]: " option
done
	case "$option" in
		1|"") 
		sudo iptables -S
		;;
		2) 
			read -p "Enter VPN Address: " vpn_addr
			until [[ -z "$vpn_addr" || "$vpn_addr" =~ [0-9]{1,3}(\.[0-9]{1,3}){3}$ ]]; do
				echo "$vpn_addr: invalid IP address."
				read -p "Enter VPN Address: " vpn_addr
			done
		sudo iptables -Z
		sudo iptables -F
		sudo iptables -X
		sudo iptables -A INPUT -i lo -j ACCEPT
		sudo iptables -A OUTPUT -o lo -j ACCEPT
		sudo iptables -A INPUT -s $vpn_addr -j ACCEPT
		sudo iptables -A OUTPUT -d $vpn_addr -j ACCEPT
		sudo iptables -A INPUT -i ppp0 -j ACCEPT
		sudo iptables -A OUTPUT -o ppp0 -j ACCEPT
		sudo iptables -A INPUT -j DROP
		sudo iptables -A OUTPUT -j DROP
		sudo iptables -P INPUT DROP
		sudo iptables -P OUTPUT DROP
		echo -e "VPN Kill Switch is now \e[32mON\e[0m"
		;;
		3)
		sudo iptables -Z
		sudo iptables -F
		sudo iptables -X
		echo -e "VPN Kill Switch is now \e[31mOFF\e[0m"
	esac
