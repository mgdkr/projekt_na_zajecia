Diagram przypadków użycia: Aplikacja do zarządzania budżetem studenckim
(odbiorcy: osoby 18–25 lat)
DIAGRAM FLOWCHART - PRZEPŁYW GŁÓWNYCH OPERACJI

                              * START *
                                  |
                                  v
                      +---------------------------+
                      |  STUDENT 18-25            |
                      |  (Nowy/Istniejący)        |
                      +---------------------------+
                                  |
                    +--------------+---------------+
                    |                              |
                    v                              v
          +--------------------+      +--------------------+
          | REJESTRACJA        |      | LOGOWANIE          |
          | Nowy uzytkownik    |      | Istniejacy uzyt.   |
          +----------+---------+      +----------+---------+
                     |                           |
                     +----------+-----------+----+
                                |
                                v
                    +========================+
                    | STRONA GLOWNA          |
                    | - MENU GLOWNE -        |
                    +========================+
                                |
           +--------------------+--------------------+
           |                    |                    |
           v                    v                    v
    +------------------+ +------------------+ +------------------+
    | WYDATKI          | | BUDZET           | | STATYSTYKI       |
    |                  | |                  | |                  |
    | Dodaj            | | Ustaw            | | Wykresy          |
    | Kategoria        | | Limit            | | Trendy           |
    | Kwota            | |                  | |                  |
    | Data             | |                  | |                  |
    +--------+---------+ +-------+----------+ +--------+---------+
             |                   |                    |
             v                   v                    v
        +--------+          +--------+            +--------+
        | ZAPIS  |          | LIMIT? |            | RAPORT |
        | W BD   |          +---+----+            | EKSPORT|
        +---+----+              |                 +---+----+
            |               TAK | NIE                 |
            |                   v                     |
            |            +----------+                |
            |            | ALERT    |                |
            |            | POWIADOM.|                |
            |            +----+-----+                |
            |                 |                      |
            +-----------------+----------------------+
                              |
                              v
                       +------------------+
                       | KONIEC SESJI?    |
                       +-------+----------+
                               |
                            TAK|
                               v
                       +------------------+
                       | WYLOGUJ          |
                       | (Do widzenia!)    |
                       +--------+---------+
                                |
                                v
                           * KONIEC *

    Psy strzegace wydatkow:
    
         ^__^                ^__^                ^__^
         (oo)\_______        (oo)\_______        (oo)\_______
         (__)\       )\/\    (__)\       )\/\    (__)\       )\/\
             ||----w |          ||----w |          ||----w |
             ||     ||          ||     ||          ||     ||


Relacje istotne (przykładowe):
 - Powiadomienia o przekroczeniu limitu -> wykorzystuje -> Ustawianie budżetów miesięcznych
 - Wykresy wydatków -> korzysta z -> Śledzenie wydatków
 - Kategorie kosztów -> powiązane ze Śledzeniem wydatków

Uwagi:
 - Cechy kluczowe: śledzenie wydatków, kategorie, budżety miesięczne, wykresy, powiadomienia.
 - Odbiorcy: młodzi użytkownicy 18–25 lat chcący oszczędzać i planować wydatki.


```mermaid
flowchart TD
    START([START]) --> STUDENT["👤 STUDENT 18-25<br/>(Nowy/Istniejący)"]
    
    STUDENT --> CHOICE{Typ użytkownika}
    CHOICE -->|Nowy| REJESTRACJA["📝 REJESTRACJA<br/>Nowy użytkownik"]
    CHOICE -->|Istniejący| LOGOWANIE["🔐 LOGOWANIE<br/>Istniejący użytkownik"]
    
    REJESTRACJA --> GLOWNA["📊 STRONA GŁÓWNA<br/>MENU GŁÓWNE"]
    LOGOWANIE --> GLOWNA
    
    GLOWNA --> MENU{Wybór funkcji}
    
    MENU -->|1| WYDATKI["💰 WYDATKI<br/>• Dodaj<br/>• Kategoria<br/>• Kwota<br/>• Data"]
    MENU -->|2| BUDZET["📈 BUDŻET<br/>• Ustaw<br/>• Limit"]
    MENU -->|3| STATYSTYKI["📊 STATYSTYKI<br/>• Wykresy<br/>• Trendy"]
    
    WYDATKI --> ZAPIS["💾 ZAPIS W BD"]
    BUDZET --> LIMIT{Limit<br/>przekroczony?}
    STATYSTYKI --> RAPORT["📋 RAPORT<br/>EKSPORT"]
    
    LIMIT -->|TAK| ALERT["🔔 ALERT<br/>POWIADOMIENIE"]
    LIMIT -->|NIE| KONTYNUACJA["Kontynuacja"]
    ALERT --> KONTYNUACJA
    
    ZAPIS --> KONTYNUACJA
    RAPORT --> KONTYNUACJA
    
    KONTYNUACJA --> SESJA{Koniec sesji?}
    SESJA -->|TAK| WYLOGUJ["🚪 WYLOGUJ<br/>Do widzenia!"]
    SESJA -->|NIE| GLOWNA
    
    WYLOGUJ --> END([KONIEC])
    
    style START fill:#90EE90
    style END fill:#FFB6C6
    style GLOWNA fill:#87CEEB
    style WYDATKI fill:#FFD700
    style BUDZET fill:#FFA500
    style STATYSTYKI fill:#87CEEB
    style ALERT fill:#FF6B6B
```

```mermaid
graph LR
    UZYTKOWNIK["👤 STUDENT 18-25"]
    
    UZYTKOWNIK -->|1| SLEDZ["Śledzenie wydatków"]
    UZYTKOWNIK -->|2| KATEG["Kategorie kosztów"]
    UZYTKOWNIK -->|3| BUDZ["Ustawianie budżetów<br/>miesięcznych"]
    UZYTKOWNIK -->|4| WYKRESY["Wykresy wydatków"]
    UZYTKOWNIK -->|5| POWIAD["Powiadomienia<br/>o przekroczeniu limitu"]
    
    POWIAD -.->|wykorzystuje| BUDZ
    WYKRESY -.->|korzysta z| SLEDZ
    KATEG -.->|powiązane| SLEDZ
    
    style UZYTKOWNIK fill:#FFD700
    style SLEDZ fill:#87CEEB
    style KATEG fill:#87CEEB
    style BUDZ fill:#87CEEB
    style WYKRESY fill:#87CEEB
    style POWIAD fill:#FF6B6B
```
