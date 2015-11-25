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

## Konfiguracja serwera

Tworzymy plik konfiguracji serwera:

```
dev tun   # Tradycyjny VPN jako bridge
proto udp # Domyślnie używamy protokołu UDP
port 1194 # Domyślny port usługi OpenVPN
ca ca.crt # Certyfikat CA, zwróć uwagę na uprawnienia, powinno być 644
cert vpn-serwer.crt # Certyfikat serwera vpn
key  vpn-serwer.key # Klucz serwera vpn
dh dh2048.pem # Pilk klucza używany podczas podczas wymiany kluczy prywatnych
tls-auth ta.key 0
server 192.168.2.0 255.255.255.0

```


## Odwoływanie certyfikatów

## Rozwiązywanie problemów

Narzędziem nmap można przeskanować porty w poszukiwani usługi openvpn:
```sh
nmap -sU 192.168.1.1 
```

## Źródła
* [Portal OpenVPN Community](https://openvpn.net/index.php/open-source.html)
* [OpenVPN na Wiki (eng.)](https://en.wikipedia.org/wiki/OpenVPN)
* [Praktyczna implementacja sieci VPN na przykładzie OpenVPN](http://sekurak.pl/praktyczna-implementacja-sieci-vpn-na-przykladzie-openvpn/)
* [OPENVPN BEZ TAJEMNIC](https://badsector.pl/w-praktyce/artykuly/openvpn-bez-tajemnic-cz-i.121.html)
