# Przepis na Django 1.8 + PostgreSQL 9.4

Przepis jest dla Debian'a 8.x Jessie wraz z python'em w wersji 3.

Wszystkie polecenia wykonywane są z poziomu uprzywilejowanego użytkownika. Kwestia instalacji czy konfiguracji `sudo` lub `su` nie należą do tej dokumentacji.

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

W pakietach Debian'a dostępna jest starsza wersja Django 1.7. Aktualna wersja Django to 1.8.6. Oprócz nowości wprowadzonych w tej wersji znaczącym faktem jest to, że to jest wersja LTS.

Należy zwrócić uwagę, aby użyć programu `pip3`, a nie `pip`.

```sh
pip3 install django
```

### Tworzenie aplikacji.

```sh
django-admin.py startproject projekt .
```


