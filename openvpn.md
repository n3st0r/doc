# Instalacja i konfiguracja OpenVPN

Notatki dla instalacji i konfiguracji OpenVPN'a. U Ciebie może nie zadziałać.

## Instalacja pakietów

Po prostu:
```sh
apt-get install openvpn easy-rsa haveged
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

```sh
vim /etc/CA/vars
```

Żadne z poniższych zmiennych nie powinny zostać puste
```sh
export KEY_COUNTRY=""
export KEY_PROVINCE=""
export KEY_CITY=""
export KEY_ORG=""
export KEY_EMAIL=""
export KEY_OU=""
```

a następnie należy ustawić zmienne w systemie
```sh
cd /etc/CA
source vars
```
za pierwszym razem należy przygotować katalogi
```
./clean-all
```
### Tworzymy CA

```
./build-ca
```

## Tworzenie certyfikatów i kluczy dla serwera

Tworzymy certyfikat i klucz serwera
```
./build-key-server vpn-serwer
```
W wyniku tego polecenia w katalogu kluczy powinny powstać trzy pliki
```
vpn-serwer.crt
vpn-serwer.csr
vpn-serwer.key
```

Tworzymy klucz Diffie-Hellman'a
```
./build-dh
```

Tworzymy plik ta.key, który będzie dodatkowo zabezpieczał naszego VPN'a 
```
openvpn --genkey --secret ta.key
```




## Rozwiązywanie problemów

Narzędziem nmap można przeskanować porty w poszukiwani usługi openvpn:
```sh
nmap -sU 192.168.1.1 
```

