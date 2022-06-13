How can I access my VMs using names instead of IP addresses?
=============================================================

The VM-s are seen simultaneously in several networks, at least in your „private” LAN and in public Internet. By default the public addresses (floating-ip, 185.48.x.x) have no associated names. You may assign such names from your DNS domain or you may request a name from us (as an additional service). The names provided by us have the following format: computer_name.users.creodias.eu, where "computer_name" is chosen by you.

If you need the name just to access the machine from your office workstation, the simplest way is to add its address and friendly name to /etc/hosts.

The VM-s in a given project share common „private” network – by default it is 192.168.0.x. You may create additional private networks with any addresses you like. However, they will not be equipped with DNS. If the machines are expected to recognize other by their names, either /etc/hosts need to be created and copied to all machines, or private DNS may be run on one of them. Moreover, although the addresses are dynamically assigned they are constant – they do not change from the moment of creation to deletion of the machine.
