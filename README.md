**Temat:** Warsztat samochodowy  

**Autorzy:**  Raman Dzerban, Mykyta Petrov


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

#3. Projekt bazy danych

<img width="748" height="782" alt="image" src="https://github.com/user-attachments/assets/56968c47-a29c-4c94-9f4a-68db729044ab" />



#4. Implementacja


```sql

--------------------------------------------------

CREATE TABLE Klienci (
    id_klienta INT PRIMARY KEY IDENTITY(1,1),
    imie VARCHAR(50) NOT NULL,
    nazwisko VARCHAR(50) NOT NULL,
    telefon VARCHAR(15)
);

--------------------------------------------------

CREATE TABLE Klasy_Pojazdow (
    nazwa VARCHAR(20) PRIMARY KEY,
    mnoznik DECIMAL(3,2) NOT NULL
);

--------------------------------------------------

CREATE TABLE Pojazdy (
    id_pojazdu INT PRIMARY KEY IDENTITY(1,1),
    id_klienta INT NOT NULL,
    marka VARCHAR(50) NOT NULL,
    model VARCHAR(50) NOT NULL,
    nr_rejestracyjny VARCHAR(20) UNIQUE NOT NULL,
    vin VARCHAR(50) UNIQUE,
    klasa_pojazdu VARCHAR(20) NOT NULL,
    FOREIGN KEY (id_klienta) REFERENCES Klienci(id_klienta),
    FOREIGN KEY (klasa_pojazdu) REFERENCES Klasy_Pojazdow(nazwa)
);

--------------------------------------------------

CREATE TABLE Pracownicy (
    id_pracownika INT PRIMARY KEY IDENTITY(1,1),
    imie VARCHAR(50) NOT NULL,
    nazwisko VARCHAR(50) NOT NULL,
    stanowisko VARCHAR(50) NOT NULL
);

--------------------------------------------------

CREATE TABLE Zlecenia (
    id_zlecenia INT PRIMARY KEY IDENTITY(1,1),
    id_pojazdu INT NOT NULL,
    data_przyjecia DATE NOT NULL,
    data_zakonczenia DATE,
    status VARCHAR(30) DEFAULT 'Oczekujace',
    przebieg INT NOT NULL,
    koszt_calkowity DECIMAL(10,2),
    opis VARCHAR(255),
    FOREIGN KEY (id_pojazdu) REFERENCES Pojazdy(id_pojazdu)
);

--------------------------------------------------

CREATE TABLE Czesci (
    id_czesci INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(100) NOT NULL,
    cena DECIMAL(10,2) NOT NULL
);

--------------------------------------------------

CREATE TABLE Uslugi (
    id_uslugi INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(100) NOT NULL,
    cena_jednostkowa DECIMAL(10,2) NOT NULL
);

--------------------------------------------------

CREATE TABLE Zlecenia_Pracownicy (
    id_zlecenia INT NOT NULL,
    id_pracownika INT NOT NULL,
    PRIMARY KEY (id_zlecenia, id_pracownika),
    FOREIGN KEY (id_zlecenia) REFERENCES Zlecenia(id_zlecenia),
    FOREIGN KEY (id_pracownika) REFERENCES Pracownicy(id_pracownika)
);

--------------------------------------------------

CREATE TABLE Zlecenia_Czesci (
    id_zlecenia INT NOT NULL,
    id_czesci INT NOT NULL,
    ilosc INT NOT NULL DEFAULT 1,
    PRIMARY KEY (id_zlecenia, id_czesci),
    FOREIGN KEY (id_zlecenia) REFERENCES Zlecenia(id_zlecenia),
    FOREIGN KEY (id_czesci) REFERENCES Czesci(id_czesci)
);

--------------------------------------------------

CREATE TABLE Zlecenia_Uslugi (
    id_zlecenia INT NOT NULL,
    id_uslugi INT NOT NULL,
    ilosc INT NOT NULL DEFAULT 1,
    PRIMARY KEY (id_zlecenia, id_uslugi),
    FOREIGN KEY (id_zlecenia) REFERENCES Zlecenia(id_zlecenia),
    FOREIGN KEY (id_uslugi) REFERENCES Uslugi(id_uslugi)
);
```
