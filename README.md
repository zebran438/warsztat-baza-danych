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

# 3. Projekt bazy danych

<img width="748" height="782" alt="image" src="https://github.com/user-attachments/assets/56968c47-a29c-4c94-9f4a-68db729044ab" />

# Opis poszczególnych tabel

---

## Nazwa tabeli: Klienci

- **Opis:** Tabela przechowuje podstawowe dane klientów korzystających z usług warsztatu samochodowego. Dane te są wykorzystywane do kontaktu z klientem oraz powiązania właściciela z jego pojazdami i historią napraw.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_klienta | INT | Klucz główny, unikalny identyfikator klienta |
| imie | VARCHAR(50) | Imię klienta |
| nazwisko | VARCHAR(50) | Nazwisko klienta |
| telefon | VARCHAR(15) | Numer telefonu kontaktowego |

---

## Nazwa tabeli: Klasy_Pojazdow

- **Opis:** Tabela przechowuje klasy pojazdów oraz przypisane do nich mnożniki kosztów usług. Pozwala to uwzględnić różnice w kosztach napraw pomiędzy pojazdami ekonomicznymi, średnimi i premium.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| nazwa | VARCHAR(20) | Klucz główny, nazwa klasy pojazdu |
| mnoznik | DECIMAL(3,2) | Współczynnik wpływający na końcowy koszt usług |

---

## Nazwa tabeli: Pojazdy

- **Opis:** Tabela przechowuje dane pojazdów należących do klientów warsztatu. Każdy pojazd jest przypisany do konkretnego klienta oraz klasy pojazdu wpływającej na koszt napraw.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_pojazdu | INT | Klucz główny |
| id_klienta | INT | Klucz obcy → Klienci |
| marka | VARCHAR(50) | Marka pojazdu |
| model | VARCHAR(50) | Model pojazdu |
| nr_rejestracyjny | VARCHAR(20) | Unikalny numer rejestracyjny pojazdu |
| vin | VARCHAR(50) | Unikalny numer VIN pojazdu |
| klasa_pojazdu | VARCHAR(20) | Klucz obcy → Klasy_Pojazdow |

---

## Nazwa tabeli: Pracownicy

- **Opis:** Tabela zawiera dane pracowników warsztatu, takich jak mechanicy oraz kierownicy. Informacje te pozwalają przypisywać pracowników do konkretnych zleceń naprawczych.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_pracownika | INT | Klucz główny |
| imie | VARCHAR(50) | Imię pracownika |
| nazwisko | VARCHAR(50) | Nazwisko pracownika |
| stanowisko | VARCHAR(50) | Stanowisko pracownika w warsztacie |

---

## Nazwa tabeli: Zlecenia

- **Opis:** Tabela przechowuje informacje o zleceniach naprawczych realizowanych przez warsztat. Każde zlecenie jest przypisane do konkretnego pojazdu i zawiera informacje o statusie naprawy, przebiegu pojazdu oraz całkowitym koszcie wykonanych prac.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_zlecenia | INT | Klucz główny |
| id_pojazdu | INT | Klucz obcy → Pojazdy |
| data_przyjecia | DATE | Data przyjęcia pojazdu do warsztatu |
| data_zakonczenia | DATE | Data zakończenia naprawy |
| status | VARCHAR(30) | Status zlecenia (Oczekujace, W trakcie, Zakonczone), domyślnie: Oczekujace |
| przebieg | INT | Aktualny przebieg pojazdu |
| koszt_calkowity | DECIMAL(10,2) | Łączny koszt części i usług |
| opis | VARCHAR(255) | Opis usterki lub wykonanej naprawy |

---

## Nazwa tabeli: Czesci

- **Opis:** Tabela zawiera informacje o częściach zamiennych dostępnych i wykorzystywanych podczas realizacji napraw. Dane te są używane do obliczania kosztów zleceń.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_czesci | INT | Klucz główny |
| nazwa | VARCHAR(100) | Nazwa części zamiennej |
| cena | DECIMAL(10,2) | Cena jednostkowa części |

---

## Nazwa tabeli: Uslugi

- **Opis:** Tabela przechowuje listę usług wykonywanych w warsztacie, takich jak wymiana oleju, diagnostyka czy naprawa hamulców. Koszt usług może być modyfikowany przez mnożnik klasy pojazdu.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_uslugi | INT | Klucz główny |
| nazwa | VARCHAR(100) | Nazwa usługi |
| cena_jednostkowa | DECIMAL(10,2) | Bazowa cena wykonania usługi |

---

## Nazwa tabeli: Zlecenia_Pracownicy

- **Opis:** Tabela pośrednia realizująca relację wiele-do-wielu pomiędzy zleceniami a pracownikami. Pozwala określić, którzy pracownicy uczestniczyli w realizacji konkretnego zlecenia.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_pracownika | INT | Klucz obcy → Pracownicy |

---

## Nazwa tabeli: Zlecenia_Czesci

- **Opis:** Tabela przechowuje informacje o częściach wykorzystanych podczas realizacji konkretnego zlecenia naprawczego wraz z ich ilością.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_czesci | INT | Klucz obcy → Czesci |
| ilosc | INT | Ilość wykorzystanych części |

---

## Nazwa tabeli: Zlecenia_Uslugi

- **Opis:** Tabela przechowuje informacje o usługach wykonanych w ramach konkretnego zlecenia oraz ich ilości. Dane te są wykorzystywane do obliczania kosztu całkowitego naprawy.

| Nazwa atrybutu | Typ | Opis/Uwagi |
|---------------|-----|------------|
| id_zlecenia | INT | Klucz obcy → Zlecenia |
| id_uslugi | INT | Klucz obcy → Uslugi |
| ilosc | INT | Ilość wykonanych usług |


# 4. Implementacja


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
    status VARCHAR(30) 
        CONSTRAINT chk_status 
        CHECK (status IN ('Oczekujace', 'W trakcie', 'Zakonczone'))
        DEFAULT 'Oczekujace',
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
# Widoki

```sql
CREATE VIEW v_Koszty_Uslug_Z_Mnoznikiem AS
SELECT 
    z.id_zlecenia,
    p.marka,
    p.model,
    p.nr_rejestracyjny,
    kp.nazwa AS klasa_pojazdu,
    kp.mnoznik,
    u.nazwa AS nazwa_uslugi,
    u.cena_jednostkowa AS cena_bazowa,
    zu.ilosc,
    CAST(
        (u.cena_jednostkowa * zu.ilosc * kp.mnoznik)
        AS DECIMAL(10,2)
    ) AS koszt_rzeczywisty
FROM Zlecenia_Uslugi zu
JOIN Uslugi u 
    ON zu.id_uslugi = u.id_uslugi
JOIN Zlecenia z 
    ON zu.id_zlecenia = z.id_zlecenia
JOIN Pojazdy p 
    ON z.id_pojazdu = p.id_pojazdu
JOIN Klasy_Pojazdow kp 
    ON p.klasa_pojazdu = kp.nazwa;

--------------------------------------------------

CREATE VIEW v_Pelny_Raport_Zlecenia AS
SELECT 
    z.id_zlecenia,
    p.marka,
    p.model,
    p.nr_rejestracyjny,
    z.data_przyjecia,
    z.data_zakonczenia,
    z.status,
    z.przebieg,
    z.koszt_calkowity
FROM Zlecenia z
JOIN Pojazdy p ON z.id_pojazdu = p.id_pojazdu;
```
# Funkcja

```sql
CREATE FUNCTION dbo.fn_ObliczKosztCalkowity (@id_zlecenia INT)
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @koszt_czesci DECIMAL(10,2) = 0;
    DECLARE @koszt_uslug DECIMAL(10,2) = 0;
    DECLARE @mnoznik DECIMAL(3,2) = 1.0;

    SELECT @mnoznik = kp.mnoznik
    FROM Zlecenia z
    JOIN Pojazdy p ON z.id_pojazdu = p.id_pojazdu
    JOIN Klasy_Pojazdow kp ON p.klasa_pojazdu = kp.nazwa
    WHERE z.id_zlecenia = @id_zlecenia;

    SELECT @koszt_czesci = ISNULL(SUM(c.cena * zc.ilosc), 0)
    FROM Zlecenia_Czesci zc
    JOIN Czesci c ON zc.id_czesci = c.id_czesci
    WHERE zc.id_zlecenia = @id_zlecenia;

    SELECT @koszt_uslug = ISNULL(SUM(u.cena_jednostkowa * zu.ilosc * @mnoznik), 0)
    FROM Zlecenia_Uslugi zu
    JOIN Uslugi u ON zu.id_uslugi = u.id_uslugi
    WHERE zu.id_zlecenia = @id_zlecenia;

    RETURN @koszt_czesci + @koszt_uslug;
END;
```
# Tiggery

```sql
CREATE TRIGGER trg_AktualizujKosztZlecenia_Uslugi
ON Zlecenia_Uslugi
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
    SET NOCOUNT ON;

    UPDATE z
    SET koszt_calkowity = dbo.fn_ObliczKosztCalkowity(z.id_zlecenia)
    FROM Zlecenia z
    WHERE z.id_zlecenia IN (
        SELECT id_zlecenia FROM inserted
        UNION
        SELECT id_zlecenia FROM deleted
    );
END;

--------------------------------------------------

CREATE TRIGGER trg_AktualizujKosztZlecenia_Czesci
ON Zlecenia_Czesci
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
    SET NOCOUNT ON;

    UPDATE z
    SET koszt_calkowity = dbo.fn_ObliczKosztCalkowity(z.id_zlecenia)
    FROM Zlecenia z
    WHERE z.id_zlecenia IN (
        SELECT id_zlecenia FROM inserted
        UNION
        SELECT id_zlecenia FROM deleted
    );
END;
```


