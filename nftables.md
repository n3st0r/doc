
# nftables
Oficjalny następca aplikacji: {ip,ip6,arp,eb}tables

## Instalacja
W Jessie warto zainstalować kernal 4.x z backportów w Stretch bez problemów:
```
apt install nftables
```
# Obsługa nftables

## Zarządzanie z poziomu systemd
```
systemctl status|start|stop|restart|enable|disable nftables
```

# Polecenie nft
Ładowanie regułek z pliku:
```
nft -f file
```
Zapisywanie aktualnych reguł do pliku
```
nft list table filter > filter-table
```

## Includowanie plików
```
#!/usr/sbin/nft
 
include "inet-filter-sets.nft"
include "inet-filter-chain-input.nft"
```
