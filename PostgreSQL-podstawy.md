# Notatki - obsługa bazy danych PostgreSQL

## Wyświetlanie dostępnych baz:
```
\l
```
## Wybranie bazy danych
```
\c nazwa_bazy_danych
```

## Wyświetlanie tabel w bazie danych:
W poleceniu `psql` najprościej jest użyć:
```
\dt
```
Jako zapytanie SQL można to zrobić tak:
```
SELECT * FROM pg_catalog.pg_tables
```
lub dodatkowo pozbyć się tabel systemowych:
```
SELECT * FROM pg_catalog.pg_tables WHERE schemaname != 'pg_catalog' AND schemaname != 'information_schema'
```

## Zakładanie bazy danych + kodowanie UTF-8
### Założenie bazy:
```sql
CREATE DATABASE nazwa_bazy_danych WITH ENCODING ‘UTF8’;
```

### Założenie użytkownika bazy + konfiguracja 
```sql 
CREATE USER użytkownik_bazy WITH PASSWORD 'hasło_do_bazy';
ALTER ROLE użytkownik_bazy SET client_encoding TO 'utf8';
```
Prawnienia można nadać wszystkie do bazy:
```sql
GRANT ALL PRIVILEGES ON DATABASE użytkownik_bazy to nazwa_bazy_danych;
```
lub tylko wybrane:
```sql
GRANT CONNECT ON DATABASE użytkownik_bazy TO nazwa_bazy_danych;
GRANT SELECT,INSERT, UPDATE, DELETE TO nazwa_bazy_danych;
```

# "Polonizacja" bazy
Dodajemy w pliku `postgresql.conf`
```
timezone = 'Poland'
# Poniższy komunikat warto zostawić w języku angielskim - łatwiej znaleźć rozwiązanie problemu
lc_messages = 'pl_PL.UTF-8'  # formatowanie komunikatów o błędach
lc_monetary = 'pl_PL.UTF-8'  # formatowanie walut
lc_numeric = 'pl_PL.UTF-8'   # formatowanie liczb
lc_time = 'pl_PL.UTF-8'      # formatowanie daty i czasu
```

# Zakładanie bazy dla rsyslog'a
Historycznie baza sysloga nazywana była Syslog (z wielkiej litery). U mnie baza nazywa się po prostu 'syslog':
```sql
CREATE DATABASE "Syslog" WITH ENCODING 'SQL_ASCII' TEMPLATE template0;
CREATE USER rsyslog WITH PASSWORD '******';
GRANT ALL  PRIVILEGES ON DATABASE syslog TO rsyslog;
```
## Tworzenie tabel dla rsysloga:
```sql
\c syslog;
CREATE TABLE SystemEvents
(
        ID serial not null primary key,
        CustomerID bigint,
        ReceivedAt timestamp without time zone NULL,
        DeviceReportedTime timestamp without time zone NULL,
        Facility smallint NULL,
        Priority smallint NULL,
        FromHost varchar(60) NULL,
        Message text,
        NTSeverity int NULL,
        Importance int NULL,
        EventSource varchar(60),
        EventUser varchar(60) NULL,
        EventCategory int NULL,
        EventID int NULL,
        EventBinaryData text NULL,
        MaxAvailable int NULL,
        CurrUsage int NULL,
        MinUsage int NULL,
        MaxUsage int NULL,
        InfoUnitID int NULL ,
        SysLogTag varchar(60),
        EventLogType varchar(60),
        GenericFileName VarChar(60),
        SystemID int NULL
);

CREATE TABLE SystemEventsProperties
(
        ID serial not null primary key,
        SystemEventID int NULL ,
        ParamName varchar(255) NULL ,
        ParamValue text NULL
);
```
