# Instalacja i konfiguracja OpenVPN

Notatki dla instalacji i konfiguracji OpenVPN'a. U Ciebie może nie zadziałać.

## Instalacja pakietów

Po prostu:
```sh
apt-get install openvpn easy-rsa
```

## Centrum autoryzacji.

Ja lubię tworzyć centrum certyfikacji w katalogu `/etc/CA`.
Dlatego na początku przygotowuję katalog:
```sh
mkdir /etc/CA
```
Następnie kopiujemy zawartość katalogu easy-rsa:
```sh
cp -a /usr/share/easy-rsa/* /etc/CA
```

### Przygotowanie danych

Często używane dane przy konfiguracji OpenVPN trzymane są w pliku zmiennych.
```
vim /etc/CA/vars
```
a następnie należy ustawić zmienne w systemie
```
cd /etc/CA
source vars
```

## Rozwiązywanie problemów

Narzędziem nmap można przeskanować porty w poszukiwani usługi openvpn:
```
nmap -sU 192.168.1.1 
```

