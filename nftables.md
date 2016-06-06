
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

## Definicje i sety

```
#!/usr/sbin/nft
 
define google_dns = 8.8.8.8   # Definicja zmiennej
define ntp_servers = { 84.77.40.132, 176.31.53.99, 81.19.96.148, 138.100.62.8 }  # jak IPset

add table filter
add chain filter input { type filter hook input priority 0; }
add rule filter input ip saddr $google_dns counter
add rule filter input ip saddr $ntp_servers counter
```
