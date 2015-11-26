# Prosta ściąga do git'a

## Tworzenie nowego projektu na github'ie w linii komend.

Mimo linii komend, to początkowo należy na github'ie utworzyć projekt.
Należy jednak pamiętać, aby go nie inicjować. Nawet plikiem Readme.md.

### Inicjowanie repo git z linii poleceń

Po prostu w katalogu, który jest głównym katalogiem projektu wpisujemy polecenie:
```
git init
```
### Dostosowanie git'a
#### Kolorowy diff
Polecenie `git diff` posiada opcję `–color` do wyświetlania zmian w kolorach. Warto skonfigurować nawet globalnie tą opcję na stałe:
```
git config --global diff.color true
```
#### Jeszcze więcej kolorów
Globalna konfiguracja dla wszystkich czynności
```
git config --global color.ui always
```
Lub specyficzna konfiguracja dla poleceń typu status czy branch:
```
git config --global color.branch true
git config --global color.diff true
git config --global color.interactive true
git config --global color.status true
```

#### Warto podpisać kto wykonuje zmiany
```
git config user.name "Twój nick lub imię i nazwisko"
git config user.email "twój@mail.pl"
```
Weryfikacja wprowadzonych zmian:
```
git config --list
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

## Zatwierdzanie zmian - commit

Teoretycznie do zatwierdzania zmian służy polecenie:
```
git commit
```

Znacznie lepiej używać w połączeniu z dwoma opcjami:
```
git commit -a -m'Komentarz do zmian'
```

## Status lokalnego repozytorium
Wyświetla listę wszystkich zmienionych plików w lokalnym repozytorium.
```
git status
```

Szczegółowo wyświetla zmiany w wybranym pliku przed commit'em
```
git diff [plik]
```

Wyświetlanie zmian we wszystkich plikach przed commit'em
```
git diff
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

## Branch, czyli rozgałęzienia projektu

Utworzenie nowej gałęzi projektu, a następnie przełączenie aktualnej pracy
na nowo utworzoną gałąź:
```
git checkout -b [branch]
```

Pobieranie zmian z gałęzi master do aktywnej gałęzi
```
git rebase master
```

Usuwanie gałęzi na zdalnym repozytorium
```
git push origin :[branch]
```

Usuwanie lokalnego rozgałęzienia projektu. Nie można usunąć w ten sposób aktywnego brancha
```
git branch -d [branch]
```

Pobranie najnowszych zmian dla aktywnego rozgałęzienia ze zdalnego repozytorium.
```
git pull --rebase
```

Wyświetlenie listy gałęzi projektu na zdalnym repozytorium
```
git branch -r
```
