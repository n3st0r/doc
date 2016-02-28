# Obsługa systemd

## Listing uruchomionych usług
```
systemctl
```
## Polecenie

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

### Aktywacja automatycznego uruchamiania `usługi`:
```
systemctl enable usługa.service
```

### Dezaktywacja automatycznego uruchamiania `usługi`:
```
systemctl disable usługa.service
```

### Weryfikacja czy `usługa` jest automatycznie uruchamiana:
```
systemctl is-enabled usługa.service; echo $?
```
