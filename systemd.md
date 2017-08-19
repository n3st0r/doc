# Obsługa systemd

> ## :nut_and_bolt:  Jednostki (`units`) w systemd
> Mianem `jednostek/units` w systemd określane są:
> * usługi (.service)
> * punkty mountowania (.mount)
> * urządzenia (.device)
> * sockety (.socket)

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

### Maskowanie przed automatycznym lub nawet ręczym uruchamianiem usługi:
```
systemctl mask usługa.service
```

### Odmaskowanie usługi:
```
systemctl unmask usługa.service
```
### Sprawdzenie statusu ON/OFF w różnych runlevelach:
```
ls /etc/systemd/system/*.wants/usługa.service	
```

### Weryfikacja czy `usługa` jest automatycznie uruchamiana:
```
systemctl is-enabled usługa.service; echo $?
```

## Poniżej polecenia do weryfikacji jednostek.

### Wyświetlanie plików modułu:
Poniższe polecenie wyświetla wszytskie pliki należące do modułu oraz ich stan w systemie:
```
systemctl list-unit-files
```
### Pokazuje czy moduł załadowany:
```
systemctl list-units
```
### Wyświetlanie zależności dla usługi:
```
systemctl list-dependencies
```
### Lista socketów modułu:
```
systemctl list-sockets
```
### Lista zadań modułu:
```
systemctl list-jobs
```
### Lista domyślnych (np. jak poziom uruchomienia):
```
systemctl get – default
```
### Wyświetlanie wszystkich uruchomionych jednostek:
```
systemctl list-units
```

### Wyświetlanie wszystkich niepoprawnych jednostek:
```
systemctl --failed
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
