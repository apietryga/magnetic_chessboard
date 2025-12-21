# Requirements – Smart Chessboard

## Wymagania funkcjonalne

### Detekcja ruchów
- Każde pole planszy posiada czujnik obecności pionka
- System wykrywa:
  - zdjęcie pionka z pola
  - położenie pionka na innym polu
- Ruch jest interpretowany jako para: FROM -> TO

### Obsługa gry
- System wykrywa ruchy, ale:
  - nie waliduje ich samodzielnie
  - przekazuje dane do warstwy logiki gry
- W przypadku wykrycia nielegalnego ruchu:
  - użytkownik jest informowany sygnałem dźwiękowym

### Sygnalizacja dźwiękowa (brzęczek)
Brzęczek musi:
- sygnalizować:
  - start systemu
  - poprawnie wykryty ruch
  - nielegalny ruch
  - błąd systemowy
- obsługiwać różne wzorce dźwiękowe (krótkie / długie / sekwencje)

### Zapis danych
- Wszystkie ruchy są zapisywane lokalnie na karcie pamięci
- Dane muszą przetrwać:
  - restart systemu
  - brak połączenia z aplikacją

### Synchronizacja
- Po nawiązaniu połączenia z aplikacją:
  - zapisane lokalnie ruchy są synchronizowane
- System zapobiega duplikacji danych

### Tryb offline
- Pełna funkcjonalność wykrywania i zapisu ruchów działa bez połączenia
- Synchronizacja jest wykonywana asynchronicznie

---

## Wymagania niefunkcjonalne

### Architektura
- firmware działa w oparciu o maszynę stanów
- komunikacja oparta o zdarzenia (event-based)

### Niezawodność
- system odporny na:
  - drgania pionków
  - krótkotrwałe zakłócenia styków
- stosowany debounce logiczny

### Modułowość
- możliwość:
  - zmiany typu czujników
  - wymiany mikrokontrolera
  - rozbudowy o kolejne peryferia

### Utrzymanie
- czytelna struktura repozytorium
- dokumentacja decyzji architektonicznych
- możliwość łatwego debugowania

### Tryb lokalnego serwera
- ESP uruchamia własny Access Point lub działa w LAN
- po połączeniu klient jest automatycznie przekierowany na UI
- UI prezentuje historię partii i aktualny stan