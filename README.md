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

# 3. Opis tabel
<img width="1213" height="854" alt="image" src="https://github.com/user-attachments/assets/7d44ae2d-7242-4d1e-8e6f-c92818678db2" />


---

## Nazwa tabeli: Klienci

**Opis:**  
Tabela przechowuje dane klientów korzystających z usług warsztatu samochodowego. Dane te umożliwiają identyfikację właściciela pojazdu oraz kontakt z klientem.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_klienta | INT | Klucz główny, unikalny identyfikator klienta |
| imie | VARCHAR(50) | Imię klienta |
| nazwisko | VARCHAR(50) | Nazwisko klienta |
| telefon | VARCHAR(15) | Numer telefonu klienta |

---

## Nazwa tabeli: Klasy_Pojazdow

**Opis:**  
Tabela przechowuje klasy pojazdów oraz odpowiadające im mnożniki kosztów usług. Pozwala to uwzględnić różnice w kosztach napraw pomiędzy pojazdami różnych klas.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_klasy | INT | Klucz główny |
| nazwa | VARCHAR(20) | Nazwa klasy pojazdu |
| mnoznik | DECIMAL(3,2) | Współczynnik wpływający na koszt usług |

---

## Nazwa tabeli: Marki

**Opis:**  
Tabela przechowuje listę marek pojazdów dostępnych w systemie. Rozdzielenie marek i modeli pozwala uniknąć powielania danych.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_marki | INT | Klucz główny |
| nazwa | VARCHAR(50) | Nazwa marki pojazdu |

---

## Nazwa tabeli: Modele

**Opis:**  
Tabela przechowuje modele pojazdów przypisane do konkretnych marek.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_modelu | INT | Klucz główny |
| id_marki | INT | Klucz obcy → Marki |
| nazwa | VARCHAR(50) | Nazwa modelu pojazdu |

---

## Nazwa tabeli: Pojazdy

**Opis:**  
Tabela przechowuje dane pojazdów należących do klientów warsztatu. Każdy pojazd jest przypisany do modelu oraz klasy pojazdu.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_pojazdu | INT | Klucz główny |
| id_klienta | INT | Klucz obcy → Klienci |
| id_modelu | INT | Klucz obcy → Modele |
| id_klasy | INT | Klucz obcy → Klasy_Pojazdow |
| nr_rejestracyjny | VARCHAR(20) | Unikalny numer rejestracyjny |
| vin | VARCHAR(50) | Unikalny numer VIN |

---

## Nazwa tabeli: Pracownicy

**Opis:**  
Tabela przechowuje dane pracowników warsztatu, takich jak mechanicy oraz kierownicy.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_pracownika | INT | Klucz główny |
| imie | VARCHAR(50) | Imię pracownika |
| nazwisko | VARCHAR(50) | Nazwisko pracownika |
| stanowisko | VARCHAR(50) | Stanowisko pracownika |

---

## Nazwa tabeli: Zlecenia

**Opis:**  
Tabela przechowuje informacje o zleceniach naprawczych realizowanych w warsztacie samochodowym.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_zlecenia | INT | Klucz główny |
| id_pojazdu | INT | Klucz obcy → Pojazdy |
| data_przyjecia | DATE | Data przyjęcia pojazdu |
| data_zakonczenia | DATE | Data zakończenia naprawy |
| status | VARCHAR(30) | Status zlecenia |
| przebieg | INT | Aktualny przebieg pojazdu |
| opis | VARCHAR(255) | Opis usterki lub naprawy |

---

## Nazwa tabeli: Czesci

**Opis:**  
Tabela przechowuje dane części zamiennych wykorzystywanych podczas napraw.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_czesci | INT | Klucz główny |
| nazwa | VARCHAR(100) | Nazwa części |
| cena | DECIMAL(10,2) | Aktualna cena części |

---

## Nazwa tabeli: Czesci_Modele

**Opis:**  
Tabela pośrednia realizująca relację wiele-do-wielu pomiędzy częściami a modelami pojazdów. Pozwala określić, które części są kompatybilne z konkretnymi modelami samochodów.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_czesci | INT | Klucz obcy → Czesci |
| id_modelu | INT | Klucz obcy → Modele |

---

## Nazwa tabeli: Uslugi

**Opis:**  
Tabela przechowuje listę usług wykonywanych w warsztacie samochodowym.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_uslugi | INT | Klucz główny |
| nazwa | VARCHAR(100) | Nazwa usługi |
| cena_jednostkowa | DECIMAL(10,2) | Bazowa cena usługi |

---

## Nazwa tabeli: Zlecenia_Pracownicy

**Opis:**  
Tabela pośrednia realizująca relację wiele-do-wielu pomiędzy zleceniami a pracownikami.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_zlecenia_pracownika | INT | Klucz główny |
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_pracownika | INT | Klucz obcy → Pracownicy |

---

## Nazwa tabeli: Zlecenia_Czesci

**Opis:**  
Tabela przechowuje informacje o częściach wykorzystanych podczas realizacji konkretnego zlecenia wraz z ilością oraz ceną obowiązującą w momencie naprawy.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_zlecenia_czesci | INT | Klucz główny |
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_czesci | INT | Klucz obcy → Czesci |
| ilosc | INT | Ilość użytych części |
| cena_w_momencie | DECIMAL(10,2) | Cena części w momencie naprawy |

---

## Nazwa tabeli: Zlecenia_Uslugi

**Opis:**  
Tabela przechowuje informacje o usługach wykonanych w ramach zlecenia wraz z ilością oraz ceną obowiązującą w momencie realizacji usługi.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---|---|---|
| id_zlecenia_uslugi | INT | Klucz główny |
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_uslugi | INT | Klucz obcy → Uslugi |
| ilosc | INT | Ilość wykonanych usług |
| cena_w_momencie | DECIMAL(10,2) | Cena usługi w momencie realizacji |


# 4. Implementacja

## Kod poleceń DDL

```sql
--------------------------------------------------
-- KLIENCI
--------------------------------------------------

CREATE TABLE Klienci (
    id_klienta INT PRIMARY KEY IDENTITY(1,1),
    imie VARCHAR(50) NOT NULL,
    nazwisko VARCHAR(50) NOT NULL,
    telefon VARCHAR(15)
);

--------------------------------------------------
-- KLASY POJAZDOW
--------------------------------------------------

CREATE TABLE Klasy_Pojazdow (
    id_klasy INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(20) NOT NULL UNIQUE,
    mnoznik DECIMAL(3,2) NOT NULL
);

--------------------------------------------------
-- MARKI
--------------------------------------------------

CREATE TABLE Marki (
    id_marki INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(50) NOT NULL UNIQUE
);

--------------------------------------------------
-- MODELE
--------------------------------------------------

CREATE TABLE Modele (
    id_modelu INT PRIMARY KEY IDENTITY(1,1),

    id_marki INT NOT NULL,

    nazwa VARCHAR(50) NOT NULL,

    FOREIGN KEY (id_marki)
        REFERENCES Marki(id_marki)
);

--------------------------------------------------
-- POJAZDY
--------------------------------------------------

CREATE TABLE Pojazdy (
    id_pojazdu INT PRIMARY KEY IDENTITY(1,1),

    id_klienta INT NOT NULL,
    id_modelu INT NOT NULL,
    id_klasy INT NOT NULL,

    nr_rejestracyjny VARCHAR(20) UNIQUE NOT NULL,
    vin VARCHAR(50) UNIQUE,

    FOREIGN KEY (id_klienta)
        REFERENCES Klienci(id_klienta),

    FOREIGN KEY (id_modelu)
        REFERENCES Modele(id_modelu),

    FOREIGN KEY (id_klasy)
        REFERENCES Klasy_Pojazdow(id_klasy)
);

--------------------------------------------------
-- PRACOWNICY
--------------------------------------------------

CREATE TABLE Pracownicy (
    id_pracownika INT PRIMARY KEY IDENTITY(1,1),
    imie VARCHAR(50) NOT NULL,
    nazwisko VARCHAR(50) NOT NULL,
    stanowisko VARCHAR(50) NOT NULL
);

--------------------------------------------------
-- ZLECENIA
--------------------------------------------------

CREATE TABLE Zlecenia (
    id_zlecenia INT PRIMARY KEY IDENTITY(1,1),

    id_pojazdu INT NOT NULL,

    data_przyjecia DATE NOT NULL,
    data_zakonczenia DATE,

    status VARCHAR(30)
        CHECK (
            status IN (
                'Oczekujace',
                'W trakcie',
                'Zakonczone'
            )
        )
        DEFAULT 'Oczekujace',

    przebieg INT NOT NULL,

    opis VARCHAR(255),

    FOREIGN KEY (id_pojazdu)
        REFERENCES Pojazdy(id_pojazdu),

    CHECK (
        data_zakonczenia IS NULL
        OR data_zakonczenia >= data_przyjecia
    )
);

--------------------------------------------------
-- CZESCI
--------------------------------------------------

CREATE TABLE Czesci (
    id_czesci INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(100) NOT NULL,
    cena DECIMAL(10,2) NOT NULL
);

--------------------------------------------------
-- CZESCI ↔ MODELE
--------------------------------------------------

CREATE TABLE Czesci_Modele (
    id_czesci INT NOT NULL,
    id_modelu INT NOT NULL,

    PRIMARY KEY (
        id_czesci,
        id_modelu
    ),

    FOREIGN KEY (id_czesci)
        REFERENCES Czesci(id_czesci),

    FOREIGN KEY (id_modelu)
        REFERENCES Modele(id_modelu)
);

--------------------------------------------------
-- USLUGI
--------------------------------------------------

CREATE TABLE Uslugi (
    id_uslugi INT PRIMARY KEY IDENTITY(1,1),
    nazwa VARCHAR(100) NOT NULL,
    cena_jednostkowa DECIMAL(10,2) NOT NULL
);

--------------------------------------------------
-- ZLECENIA ↔ PRACOWNICY
--------------------------------------------------

CREATE TABLE Zlecenia_Pracownicy (

    id_zlecenia_pracownika INT
        PRIMARY KEY IDENTITY(1,1),

    id_zlecenia INT NOT NULL,

    id_pracownika INT NOT NULL,

    FOREIGN KEY (id_zlecenia)
        REFERENCES Zlecenia(id_zlecenia),

    FOREIGN KEY (id_pracownika)
        REFERENCES Pracownicy(id_pracownika)
);

--------------------------------------------------
-- ZLECENIA ↔ CZESCI
--------------------------------------------------

CREATE TABLE Zlecenia_Czesci (

    id_zlecenia_czesci INT
        PRIMARY KEY IDENTITY(1,1),

    id_zlecenia INT NOT NULL,

    id_czesci INT NOT NULL,

    ilosc INT NOT NULL DEFAULT 1,

    cena_w_momencie DECIMAL(10,2) NOT NULL,

    FOREIGN KEY (id_zlecenia)
        REFERENCES Zlecenia(id_zlecenia),

    FOREIGN KEY (id_czesci)
        REFERENCES Czesci(id_czesci)
);

--------------------------------------------------
-- ZLECENIA ↔ USLUGI
--------------------------------------------------

CREATE TABLE Zlecenia_Uslugi (

    id_zlecenia_uslugi INT
        PRIMARY KEY IDENTITY(1,1),

    id_zlecenia INT NOT NULL,

    id_uslugi INT NOT NULL,

    ilosc INT NOT NULL DEFAULT 1,

    cena_w_momencie DECIMAL(10,2) NOT NULL,

    FOREIGN KEY (id_zlecenia)
        REFERENCES Zlecenia(id_zlecenia),

    FOREIGN KEY (id_uslugi)
        REFERENCES Uslugi(id_uslugi)
);
```

## Widoki

```sql
CREATE VIEW v_Koszty_Uslug_Z_Mnoznikiem AS
SELECT 
    z.id_zlecenia,

    ma.nazwa AS marka,
    mo.nazwa AS model,

    p.nr_rejestracyjny,

    kp.nazwa AS klasa_pojazdu,
    kp.mnoznik,

    u.nazwa AS nazwa_uslugi,

    zu.cena_w_momencie AS cena_bazowa,

    zu.ilosc,

    CAST(
        (
            zu.cena_w_momencie
            * zu.ilosc
            * kp.mnoznik
        ) AS DECIMAL(10,2)
    ) AS koszt_rzeczywisty

FROM Zlecenia_Uslugi zu

JOIN Uslugi u
    ON zu.id_uslugi = u.id_uslugi

JOIN Zlecenia z
    ON zu.id_zlecenia = z.id_zlecenia

JOIN Pojazdy p
    ON z.id_pojazdu = p.id_pojazdu

JOIN Modele mo
    ON p.id_modelu = mo.id_modelu

JOIN Marki ma
    ON mo.id_marki = ma.id_marki

JOIN Klasy_Pojazdow kp
    ON p.id_klasy = kp.id_klasy;
```

## Funkcje

```sql
CREATE FUNCTION dbo.fn_ObliczKosztCalkowity (
    @id_zlecenia INT
)
RETURNS DECIMAL(10,2)
AS
BEGIN

    DECLARE @koszt_czesci DECIMAL(10,2) = 0;
    DECLARE @koszt_uslug DECIMAL(10,2) = 0;
    DECLARE @mnoznik DECIMAL(3,2) = 1.0;

    SELECT @mnoznik = kp.mnoznik
    FROM Zlecenia z

    JOIN Pojazdy p
        ON z.id_pojazdu = p.id_pojazdu

    JOIN Klasy_Pojazdow kp
        ON p.id_klasy = kp.id_klasy

    WHERE z.id_zlecenia = @id_zlecenia;

    SELECT @koszt_czesci =
        ISNULL(
            SUM(
                zc.cena_w_momencie
                * zc.ilosc
            ),
            0
        )
    FROM Zlecenia_Czesci zc

    WHERE zc.id_zlecenia = @id_zlecenia;

    SELECT @koszt_uslug =
        ISNULL(
            SUM(
                zu.cena_w_momencie
                * zu.ilosc
                * @mnoznik
            ),
            0
        )
    FROM Zlecenia_Uslugi zu

    WHERE zu.id_zlecenia = @id_zlecenia;

    RETURN @koszt_czesci + @koszt_uslug;

END;
```

## Triggery

```sql
CREATE TRIGGER trg_Log_Uslugi
ON Zlecenia_Uslugi
AFTER INSERT
AS
BEGIN

    PRINT 'Dodano nowa usluge do zlecenia';

END;
```

```sql
CREATE TRIGGER trg_Log_Czesci
ON Zlecenia_Czesci
AFTER INSERT
AS
BEGIN

    PRINT 'Dodano nowa czesc do zlecenia';

END;
```


