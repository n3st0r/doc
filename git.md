# Prosta ściąga do git'a

## Tworzenie nowego projektu na github'ie w linii komend.

Mimo linii komend, to początkowo należy na github'ie utworzyć projekt.
Należy jednak pamiętać, aby go nie inicjować. Nawet plikiem Readme.md.

### Inicjowanie repo git z linii poleceń

Po prostu w katalogu, który jest głównym katalogiem projektu wpisujemy polecenie:
```
git init
```

### Ignorowanie plików

Jeśli w projekcie znajdują się pliki, które nie powinny być umieszczone
w repozytorium, to należy je umieścić w pliku `.gitignore`. Na przykład:
```
echo "db.sqlite3" >> .gitignore
echo "__pycache__" >>.gitignore
echo "*.pyc" >>.gitignore
```

## Dodawanie plików do repozytorium

Teraz można dodać bieżący katalog do repozytorium
```
git add .
```

## Status lokalnego repozytorium

```
git status
```

### Usuwanie plików przed aktualizacją zdalnego repozytorium
Usuwanie plików z lokalnego cache, przed aktualizacją zdalnego repozytorium.
```
git rm -r --cached katalog/__pycache__
```
Dlatego po commicie zawsze warto sprawdzić `git status`, aby mieć
pewność, czy coś niepotrzebnego nie zostało dodane do repo.

## Aktualizacja zdalnego repozytorium
```
git push origin master
```

## Pobieranie zmian ze zdalnego repozytorium
```
git pull origin master
```

