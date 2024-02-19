# SRX configurations
I've made available a collection of Juniper SRX baseline configurations for various uses. 

**SRX100b-12.1-NBN-baseline** - This is a baseline configuration that could be used for a Juniper SRX100 using Junos v12.1 connected to an NBN modem/gateway.

**Parameters:**
1. You can change the hostname to whatever you like.
2. The router is configured to accept a DHCP address from interface fe-0/0/0. You can plug it into an NBN FTTP UNI-D connection or another gateway, but be mindful of the gateway network addresses. If it conflicts with any addresses in this config, you will have issues.
3. The root user password is 'Password123'. Change it from the top of the configuration ( [edit] ) using "set system root-authentication plain-text-password" hit enter, and put a new password in.
4. The admin user password is 'Password123' Change it from the top of the configuration ( [edit] ) using "set system login user admin authentication plain-text-password" hit enter, and put a new password in.
5. The DHCP pool for this configuration is 192.168.0.0/24, if that conflicts with your gateway, then change it here, and under "vlan unit 10".
6. VLAN10 is a user data VLAN which is extended to all interfaces except fe-0/0/0.
7. You'll need to set the static route to something else other than 10.0.0.1 - I used this as a placeholder, but it needs to be set to whatever DHCP address you get on fe-0/0/0.
8. If you are sitting this behind a gateway, for example a Telstra smart modem or something, which assigns a dhcp address in the 10.0.0.0/24 range, you'll need to add it to the private-ipv4 prefix list. e.g., "set policy-options prefix-list private-ipv4 10.0.0.0/24".
9. Again, you'll need to make the "set security nat source pool GATEWAY address 10.0.0.1/32" match your actual gateway address assigned on fe-0/0/0.

**Features:** This configuration is equipped with the following features:
1. As long as you change any variables mentioned above, it should work out of the box.
2. DNS resolution by QUAD9.
3. A reasonably secure SSH configuration.
4. A user network on interfaces fe-0/0/1 through fe-0/0/7.
5. NTP by NIST.
6. A loopback interface with a firewall which will only accept and limit certain traffic to protect itself, and discard everything else.
7. LLDP and RSTP enabled.
8. A basic IDS.
9. A Zone based firewall which blocks all external to internal traffic by default.

You will need to change some details on this, but otherwise this is a solid baseline configuration.


**SRX300-NBN-baseline** - This is a baseline configuration that could be used for a Juniper SRX300 using Junos v20.2 or above connected to an NBN modem/gateway.

**Parameters:**
1. You can change the hostname to whatever you like.
2. The router is configured to accept a DHCP address from interface ge-0/0/6. You can plug it into an NBN FTTP UNI-D connection or another gateway, but be mindful of the gateway network addresses. If it conflicts with any addresses in this config, you will have issues.
3. The root user password is 'Password123'. Change it from the top of the configuration ( [edit] ) using "set system root-authentication plain-text-password" hit enter, and put a new password in.
4. The admin user password is 'Password123' Change it from the top of the configuration ( [edit] ) using "set system login user admin authentication plain-text-password" hit enter, and put a new password in.
5. The DHCP pool for this configuration is 192.168.0.0/24, if that conflicts with your gateway, then change it here, and under "vlan unit 10".
6. VLAN10 is a user data VLAN which is extended to all interfaces except ge-0/0/[6-7].
7. If you are sitting this behind a gateway, for example a Telstra smart modem or something, which assigns a dhcp address in the 10.0.0.0/24 range, you'll need to add it to the private-ipv4 prefix list. e.g., "set policy-options prefix-list private-ipv4 10.0.0.0/24".

**Features:** This configuration is equipped with the following features:
1. As long as you change any variables mentioned above, it should work out of the box.
2. DNS resolution by QUAD9.
3. A reasonably secure SSH configuration.
4. A user network on interfaces ge-0/0/0 through ge-0/0/5.
5. NTP by NIST.
6. A loopback interface with a firewall which will only accept and limit certain traffic to protect itself, and discard everything else.
7. LLDP and RSTP enabled.
8. A basic IDS.
9. A Zone based firewall which blocks all external to internal traffic by default.
