**Temat:** Warsztat samochodowy  

**Autorzy:**  


---

# 1. Zakres i krótki opis systemu

## Cel projektu

Celem projektu jest zaprojektowanie relacyjnej bazy danych dla warsztatu samochodowego, umożliwiającej przechowywanie, organizację oraz przetwarzanie danych związanych z obsługą klientów, pojazdów oraz realizacją zleceń serwisowych.

Projekt ma na celu stworzenie spójnej struktury danych, która zapewni integralność danych, ograniczy redundancję oraz umożliwi efektywne wykonywanie operacji na danych.

## Słowny opis systemu

Projektowana baza danych wspiera działalność warsztatu samochodowego poprzez gromadzenie informacji o klientach, ich pojazdach oraz wykonywanych naprawach.

W bazie danych przechowywane są informacje dotyczące:
- klientów warsztatu,
- pojazdów należących do klientów,
- zleceń serwisowych,
- pracowników warsztatu,
- części zamiennych wykorzystywanych w naprawach.

Każdy klient może posiadać jeden lub wiele pojazdów. Każdy pojazd może mieć przypisane wiele zleceń serwisowych. Zlecenia mogą być realizowane przez jednego lub wielu pracowników oraz mogą wykorzystywać różne części zamienne.

Baza danych umożliwia odwzorowanie rzeczywistych procesów zachodzących w warsztacie oraz stanowi podstawę do dalszego rozwoju systemu informatycznego.

System przechowuje również katalog usług (robocizny) wraz z ich cenami jednostkowymi. Przy każdym zleceniu rejestrowany jest przebieg pojazdu, a system automatycznie oblicza całkowity koszt naprawy jako sumę wykorzystanych części oraz wykonanych usług.

---

# 2. Wymagania i funkcje systemu

## Lista wymagań

Projektowana baza danych powinna umożliwiać:

- przechowywanie danych klientów,
- przechowywanie danych pojazdów przypisanych do klientów,
- rejestrowanie zleceń serwisowych,
- przypisywanie pracowników do zleceń,
- ewidencję części zamiennych,
- odwzorowanie relacji między poszczególnymi encjami,
- zapewnienie integralności danych poprzez zastosowanie kluczy głównych i obcych,
- ewidencję świadczonych usług (np. wymiana oleju, diagnostyka),
- rejestrowanie przebiegu pojazdu przy każdym zleceniu,
- automatyczne sumowanie kosztów zlecenia (części + robocizna).

---

## Przypadki użycia

1. Dodanie nowego klienta do bazy danych  
2. Dodanie pojazdu przypisanego do klienta  
3. Utworzenie nowego zlecenia serwisowego  
4. Przypisanie pracownika do zlecenia  
5. Dodanie informacji o wykorzystanych częściach  
6. Aktualizacja statusu zlecenia  
7. Dodanie wykonanej usługi (robocizny) do konkretnego zlecenia  
8. Wygenerowanie raportu końcowego (podsumowanie kosztów) dla klienta  

---

## Historyjki użytkownika

### Klient

- Jako klient chcę zarejestrować swój pojazd w warsztacie, aby móc zlecić jego naprawę.  
- Jako klient chcę otrzymać informację o statusie naprawy, aby wiedzieć, kiedy pojazd będzie gotowy.  
- Jako klient chcę otrzymać informację o kosztach naprawy, aby podjąć decyzję o realizacji usługi.  
- Jako klient chcę mieć wgląd w historię napraw mojego auta, aby wiedzieć, jakie części były wymieniane w przeszłości.  

---

### Pracownik biura (recepcjonista)

- Jako pracownik biura chcę dodać nowego klienta do bazy danych, aby móc obsłużyć jego zgłoszenie.  
- Jako pracownik biura chcę zarejestrować pojazd klienta, aby przypisać go do zlecenia.  
- Jako pracownik biura chcę utworzyć zlecenie serwisowe, aby przekazać je do realizacji mechanikowi.  

---

### Mechanik

- Jako mechanik chcę przeglądać przypisane mi zlecenia, aby wiedzieć, jakie prace wykonać.  
- Jako mechanik chcę aktualizować status zlecenia, aby informować o postępie naprawy.  
- Jako mechanik chcę dodawać informacje o wykorzystanych częściach, aby odzwierciedlić przebieg naprawy.  

---

### Kierownik

- Jako kierownik chcę mieć dostęp do wszystkich danych w bazie, aby zarządzać działalnością warsztatu.  
- Jako kierownik chcę analizować zlecenia i ich koszty, aby kontrolować dochody i wydatki.  
- Jako kierownik chcę zarządzać pracownikami, aby efektywnie organizować pracę warsztatu.  
- Jako kierownik chcę widzieć raport zysków z podziałem na sprzedane części i wykonane usługi mechaników.   
