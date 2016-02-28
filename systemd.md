# Obsługa systemd

## Polecenie systemctl

### Listing uruchomionych usług
```
systemctl
```

### Weryfikacja stanu `usługi`:
```
systemctl status usługa.service
```

### Uruchomienie `usługi`:
```
systemctl start usługa.service
```

### Zatrzymanie `usługi`:
```
systemctl stop usługa.service
```

### Restart `usługi`:
```
systemctl restart usługa.service
```

### Przeładowanie ustawień `usługi`:
Jeśli jest obsługiwane, następuje przeładowanie usługi bez jej restartu
```
systemctl reload usługa.service
```

### Warunkowy restart `usługi`:
Przeładowanie usługi tylko w przypadku, gdy jest uruchomiona
```
systemctl condrestart usługa.service
```

### Aktywacja automatycznego uruchamiania `usługi`:
```
systemctl enable usługa.service
```

### Dezaktywacja automatycznego uruchamiania `usługi`:
```
systemctl disable usługa.service
```

### Sprawdzenie statusu ON/OFF w różnych runlevelach:
```
ls /etc/systemd/system/*.wants/foobar.service	
```

### Weryfikacja czy `usługa` jest automatycznie uruchamiana:
```
systemctl is-enabled usługa.service; echo $?
```

## Widok jednostek w `systemctl`

Mianem `jednostek/units` w systemd określane są:
* usługi (.service)
* punkty mountowania (.mount)
* urządzenia (.device)
* sockety (.socket)

Poniżej polecenia do weryfikacji jednostek.

### Wyświetlanie stanu wszystkich jednostek w systemie:
```
systemctl list-unit-files
```

### Wyświetlanie wszystkich uruchomionych jednostek:
```
systemctl list-units
```

### Wyświetlanie wszystkich niepoprawnych jednostek:
```
systemctl –failed
```

## Polecenie systemd-analyze
Dostarcza ogólnych informacji na temat procesu uruchamiania:
```
systemd-analyze
```
Szczegółowe informacje na temat uruchamiania każdej usługi:
```
systemd-analyze blame
```
