# Sprawdzanie poziomu entropii w systemie:
```sh
cat /proc/sys/kernel/random/entropy_avail
```
Jeśli w wyniku powyższego polecenia otrzymujemy liczbę mniejszą niż 1000, konieczne jest zainstalowanie daemon'a `haveged`.

## Instalacja haveged:
Wykonaj poniższe polecenie w konsoli z uprawnieniami root'a
```sh
apt-get install haveged
```

Ponowna weryfikacja entropii w systemie pokazuje, iż problem został rozwiązany:
```
cat /proc/sys/kernel/random/entropy_avail
3581
```
