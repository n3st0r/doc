# Przepis na Django 1.8 + PostgreSQL 9.4

Przepis jest dla Debian'a 8.x Jessie wraz z python'em w wersji 3.

Wszystkie polecenia wykonywane są z poziomu uprzywilejowanego użytkownika. Kwestia instalacji czy konfiguracji `sudo` lub `su` nie należą do tej dokumentacji.

## Instalacja python.

Instalujemy pakiety `python3` oraz `pip3` do instalacji dodatkowych modułów.

```
apt-get install python3 python3-pip
```

## Instalacja postgresql

```
apt-get install postgresql postgresql-contrib
```

### Konfiguracja bazy danych

Początkową konfigurację najłatwiej wykonać z poziomu użytkownika postgres.

```
su - postgres
```

Teraz można zalogować się do interaktywnej sesji PostgreSQL'a bez dodatkowej autoryzacji:
```
psql
```

Tworzymy bazę danych:
```
CREATE DATABASE projekt;
```

Następnie tworzymy użytkownika:
```
CREATE USER użytkownik WITH PASSWORD 'hasło';
```

Przydzielamy wszystkie prawa utworzonemu użytkownikowi do nowej bazy.
```
GRANT ALL PRIVILEGES ON DATABASE projekt TO użytkownik;
```

Z sesji wychodzimy wklepując:
```
\q
```

Sesję shell użytkownika `postgres` zamykamy skrótem `Ctrl + d`.

## Instalacja Django

W pakietach Debian'a dostępna jest starsza wersja Django 1.7. Aktualna wersja Django to 1.8.6. Oprócz nowości wprowadzonych w tej wersji znaczącym faktem jest to, że to jest wersja LTS.

Należy zwrócić uwagę, aby użyć programu `pip3`, a nie `pip`.

```
pip3 install django
```

### Tworzenie aplikacji.

```
django-admin.py startproject projekt .
```


