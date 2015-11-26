# Przepis na Django 1.8 + PostgreSQL 9.4

Przepis jest dla Debian'a 8.x Jessie wraz z python'em w wersji 3.

Wszystkie polecenia wykonywane są z poziomu uprzywilejowanego użytkownika. Kwestia instalacji czy konfiguracji `sudo` lub `su` nie należą do tej dokumentacji. Do konfiguracji używam edytora vim, którego instalacja i konfiguracja jest pomięta w tym dokumencie.

## Instalacja python.

Instalujemy pakiety `python3` oraz `pip3` do instalacji dodatkowych modułów.

```sh
apt-get install python3 python3-pip
```

## Instalacja postgresql

```sh
apt-get install postgresql postgresql-contrib
```

### Konfiguracja bazy danych

Początkową konfigurację najłatwiej wykonać z poziomu użytkownika postgres.

```sh
su - postgres
```

Teraz można zalogować się do interaktywnej sesji PostgreSQL'a bez dodatkowej autoryzacji:
```sh
psql
```

Tworzymy bazę danych:
```sql
CREATE DATABASE projekt;
```

Następnie tworzymy użytkownika:
```sql
CREATE USER użytkownik WITH PASSWORD 'hasło';
```

Przydzielamy wszystkie prawa utworzonemu użytkownikowi do nowej bazy.
```sql
GRANT ALL PRIVILEGES ON DATABASE projekt TO użytkownik;
```

Z sesji wychodzimy wklepując `\q`.

Sesję shell użytkownika `postgres` zamykamy skrótem `Ctrl + d`.

## Instalacja Django

W pakietach Debian'a dostępna jest starsza wersja Django 1.7. Aktualna wersja Django to 1.8.7. Oprócz nowości wprowadzonych w tej wersji znaczącym faktem jest to, że to jest wersja LTS.

Należy zwrócić uwagę, aby użyć programu `pip3`, a nie `pip`.

```sh
pip3 install django
```
Następnie warto doinstalować moduły
```
# Unitest do testów jednostkowych jest już dostarczany z python3
# Obsługa testów funkcjonalnych
pip3 install --upgrade selenium

# Jeśli domyślny system szablonów jest za wolny, czy zbyt ubogi
# to warto doinstalować system szablonów jinja2
pip3 install Jinja2
```
### Tworzenie aplikacji.

```sh
django-admin.py startproject projekt .
```

### Konfiguracja bazy danych

Konfiguracja bazy danych musi być wykonana w pliku:
```
vim projekt/settings.py
```

Należy skonfigurować odpowiedni sterownik bazy danych, nazwę bazy, użytkownika, hasło oraz host i port. W tym przypadku `host` to localhost, a `port` można pominąć. Jako sterownik bazy użyty zostanie `psycopg2`, który został wcześniej zainstalowany narzędziem `pip3`.
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'projekt',
        'USER': 'użytkownik',
        'PASSWORD': 'hasło',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

## Konfiguracja aplikacji

Poniżej znajduje się skrypt do rozszerzenia projektu o katalogi dla plików statycznych oraz szablonów. Plik można sobie dowolnie modyfikować i rozszerzać według własnych potrzeb.

```sh
#/bin/bash

DIR_CSS='static/css'
DIR_JS='static/js'

mkdir -p {$DIR_CSS,$DIR_JS}

```

Następnie należy zmodyfikować ustawienia aplikacji w pliku `projekt/settings.py`
```python
STATIC_PATH = os.path.join(PROJECT_PATH,'static') STATIC_URL = '/static/'
STATICFILES_DIRS = (
	STATIC_PATH, )
```

## Instalacja nginx

```
apt-get -t jessie-backports install nginx
```

### Włączenie obsługi `SPDY`

Jest to jeden z powodów, dla którego nginx jest instalowany z backports'ów.
Konfiguracja jest banalnie prosta:
```
server {
    listen 443 ssl spdy;
    ...
```
Weryfikację działania `SPDY` można przeprowadzić na stronie (spdycheck.org)


