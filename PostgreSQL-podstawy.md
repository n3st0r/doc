#Obsługa bazy danych

## Wyświetlanie dostępnych baz:
\l

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
