
# nftables
Oficjalny następca aplikacji: {ip,ip6,arp,eb}tables

# Obsługa nftables z 

## Instalacja
W Jessie warto zainstalować kernal 4.x z backportów w Stretch bez problemów:
```
apt install nftables
```

## Zarządzanie z poziomu systemd
```
systemctl status|start|stop|restart|enable|disable nftables
```
