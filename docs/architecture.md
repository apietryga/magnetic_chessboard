# System Architecture – Smart Chessboard (Offline-first)

## Założenia architektoniczne

- System działa w pełni autonomicznie (offline-first)
- ESP8266 jest:
  - lokalnym serwerem aplikacji
  - silnikiem logiki gry
  - kontrolerem sprzętu
- Połączenie z urządzeniem klienckim (telefon / laptop) jest opcjonalne
- Brak chmury ≠ brak funkcjonalności

---

## Rola ESP8266

ESP8266 pełni jednocześnie funkcje:
- serwera HTTP
- silnika walidacji ruchów
- kontrolera wejść/wyjść
- systemu zapisu danych

Jest jedynym elementem systemu, który posiada pełny stan gry.

---

## Warstwy logiczne systemu

Architektura wewnętrzna ESP8266 oparta jest o wyraźnie rozdzielone warstwy logiczne:

+--------------------------------------------------+
| Web UI |
| (HTML / CSS / JS – klient) |
+--------------------------------------------------+
| HTTP API |
| (/api/state, /api/history, etc.) |
+--------------------------------------------------+
| Chess Engine |
| (reguły gry, legalność ruchów) |
+--------------------------------------------------+
| Move Interpreter |
| (FROM → TO, sekwencje fizycznych zdarzeń) |
+--------------------------------------------------+
| Board Scanner |
| (odczyt pól, debounce, stabilizacja) |
+--------------------------------------------------+
| Hardware Abstraction Layer (HAL) |
| MCP23018-E/SP / SD Card / Buzzer / WiFi |
+--------------------------------------------------+

markdown
Skopiuj kod

### Opis warstw

#### Hardware Abstraction Layer (HAL)
- bezpośrednia obsługa:
  - MCP23018-E/SP
  - brzęczka
  - karty SD
  - WiFi
- brak logiki biznesowej

#### Board Scanner
- cykliczny odczyt stanu pól
- debounce
- wykrywanie zmian (occupied / empty)

#### Move Interpreter
- interpretuje sekwencje zmian jako kandydat ruchu
- wykrywa:
  - podniesienie pionka
  - położenie pionka
- buduje strukturę FROM → TO

#### Chess Engine
- przechowuje stan gry
- waliduje legalność ruchów
- egzekwuje reguły szachowe
- decyduje o skutkach ruchu

#### HTTP API
- udostępnia stan gry
- historię partii
- kontrolę systemu (reset, nowa gra)

#### Web UI
- wyświetla dane
- nie zawiera krytycznej logiki
- może być podłączone lub nie

---
## Dwufazowy model ruchu (LIFT / PLACE)

Obsługa ruchu oparta jest o dwa jawne etapy:

1. LIFT – podniesienie figury z pola
2. PLACE – położenie figury na innym polu

Każdy etap jest walidowany niezależnie.

### Faza LIFT (podniesienie figury)

1. Board Scanner wykrywa zdjęcie figury z pola
2. Move Interpreter identyfikuje:
   - pole
   - figurę
   - kolor
3. Chess Engine sprawdza:
   - czy to jest tura tego koloru
   - czy król jest w szachu
   - czy dana figura posiada **jakikolwiek legalny ruch**
     prowadzący do usunięcia szacha

#### Decyzja

- jeśli figura **może** rozwiązać szacha:
  - LIFT zaakceptowany
  - system przechodzi w stan AWAITING_PLACE
- jeśli figura **nie może** rozwiązać szacha:
  - LIFT odrzucony
  - sygnał dźwiękowy: ILLEGAL_LIFT
  - UI informuje: "odłóż figurę z powrotem"
  - system oczekuje przywrócenia figury

### Faza PLACE (położenie figury)

1. Board Scanner wykrywa zajęcie nowego pola
2. Move Interpreter buduje kandydat ruchu FROM → TO
3. Chess Engine sprawdza:
   - legalność ruchu figury
   - czy ruch usuwa szacha (jeśli był)
   - czy nie wprowadza nowego szacha

#### Decyzja

- legalny ruch:
  - aktualizacja stanu gry
  - zapis na SD
  - sygnał: MOVE_OK
- nielegalny ruch:
  - brak zmiany stanu gry
  - sygnał: ILLEGAL_MOVE
  - UI żąda cofnięcia figury

## Spójność stanu fizycznego i logicznego

System dopuszcza sytuację, w której:
- fizyczna plansza ≠ stan logiczny gry

W takim przypadku:
- Chess Engine pozostaje źródłem prawdy
- UI informuje użytkownika o niespójności
- użytkownik koryguje fizyczne położenie figur

---

## Sygnalizacja dźwiękowa

Brzęczek jest sterowany wyłącznie na podstawie decyzji logiki gry:

- legalny ruch → krótki sygnał
- nielegalny ruch → długi sygnał
- szach → dedykowany wzorzec
- błąd systemowy → sekwencja alarmowa

Brzęczek nie reaguje bezpośrednio na zdarzenia sprzętowe.

---

## Granice odpowiedzialności

- Hardware:
  - wykrywa stan
- Firmware:
  - interpretuje
  - decyduje
  - zapisuje
- UI:
  - prezentuje

Ta separacja jest kluczowa dla dalszej rozbudowy systemu.