
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
nft list table inet filter > filter-table
```
Monitorowanie aktualizacji reguł nftables:
```
nft monitor
nft monitor rules
nft monitor new rules
```

## Includowanie plików
```
#!/usr/sbin/nft
 
include "inet-filter-sets.nft"
include "inet-filter-chain-input.nft"
```

## Sety
Jeśli nie ma takiej potrzeby, to nie używaj Set'a zamiast zmiennej.
```
set ssh {
  type ipv4_addr
  elements = { 192.168.0.1, 192.168.0.2 }
}
...
    tcp saddr @ssh tcp dport ssh ct state new accept
...
```

## Reguły

```
nft add rule inet filter input tcp saddr @ssh dport 22 ct state new tcp flags \& \(syn \| ack\) == syn log prefix \"inet/input/accept: \" counter accept

```

```
nft add rule inet filter input tcp dport 0-65535 reject
nft add rule inet filter input udp dport 0-65535 counter drop
nft add rule inet filter input counter drop
```
