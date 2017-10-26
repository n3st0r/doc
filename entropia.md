# Sprawdzanie poziomu entropii w systemie:
> ## :nut_and_bolt:  Entropia
>
> Sprawdzanie w systemia
> ```sh
> cat /proc/sys/kernel/random/entropy_avail
> ```

## Sprawdzanie w systemia
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

## Poziom entropii
W pliku konfiguracji `/etc/default/haveged` można dodatkowo określić poziom entropii, np. na poziomie 2048:
```
DAEMON_ARGS="-w 2048"
```

Sprawdzanie jakości danych losowych:
```
apt-get install rng-tools
cat /dev/random | rngtest -c 1000
```
na wyjściu otrzymujemy:
```
cat /dev/random | rngtest -c 1000
rngtest 2-unofficial-mt.14
Copyright (c) 2004 by Henrique de Moraes Holschuh
This is free software; see the source for copying conditions.  There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

rngtest: starting FIPS tests...
rngtest: bits received from input: 20000032
rngtest: FIPS 140-2 successes: 1000
rngtest: FIPS 140-2 failures: 0
rngtest: FIPS 140-2(2001-10-10) Monobit: 0
rngtest: FIPS 140-2(2001-10-10) Poker: 0
rngtest: FIPS 140-2(2001-10-10) Runs: 0
rngtest: FIPS 140-2(2001-10-10) Long run: 0
rngtest: FIPS 140-2(2001-10-10) Continuous run: 0
rngtest: input channel speed: (min=2.342; avg=15.121; max=19073.486)Mibits/s
rngtest: FIPS tests speed: (min=69.611; avg=91.987; max=93.958)Mibits/s
rngtest: Program run time: 1471983 microseconds
```
