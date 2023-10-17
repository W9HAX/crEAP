# Description

The tool `crEAP.py` is used to try harvesting Radius usernames and handshakes.

Thanks to the usernames found by `crEAP.py`, they can be used as identities for the tool [EAP_buster](https://github.com/blackarrowsec/EAP_buster) in order to list what EAP methods are supported by the RADIUS server behind a WPA-Enterprise access point.



# Requirements

It requires to install [Scapy-com](https://github.com/Tylous/Scapy-com).



# Usage

Execute `creaAP.py`.

```bash
sudo python2.7 crEAP.py -i <MANAGED_WIFI_IF> -c <VICTIMS_AP_CHANNEL> 
```

Then, you need to wait for a **NEW** user to log in to the network.

**Warning**: The script stores a lot of data on RAM, so monitor the RAM usage and interrupt the process once it has consumed a certain amount of resources. Nonetheless, a simple alternative will be this one.

```bash
while true; do sudo python2.7 crEAP.py -i wlan0 -c 1 2>&1 1>>/tmp/crEAP_output.txt ; done
while true; do sudo kill -SIGINT $(ps aux | grep crEAP | awk '{print $2}'); sleep 10 ; done

# Obtain all the harvested users
grep "Unique Harvested Users" -A 1 /tmp/crEAP_output.txt
```

