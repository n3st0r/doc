# Instalacja i konfiguracja OpenVPN

Notatki dla instalacji i konfiguracji OpenVPN'a. U Ciebie może nie zadziałać.

## Instalacja pakietów

Po prostu:
```sh
apt-get install openvpn
```

## Tworzenie centrum certyfikacji.

Ja lubię tworzyć centrum certyfikacji w katalogu `/etc/CA`.
Dlatego na początku przygotowuję katalog:
```sh
mkdir /etc/CA
```

## Rozwiązywanie problemów

Narzędziem nmap można przeskanować porty w poszukiwani usługi openvpn:
```
nmap -sU 192.168.1.1 
```

