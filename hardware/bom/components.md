# Bill of Materials – Components

Lista wszystkich kluczowych podzespołów użytych w projekcie.
Pozycje mogą mieć alternatywy – szczegóły w vendors.md.

---

## Czujniki pól

### Czujniki Halla
- Typ: czyujnik halla
- Ilość: 64
- Zastosowanie: detekcja obecności pionka
- Uwagi:
  - montowane pod każdym polem
  - wymagany debounce programowy

---

### Magnesy do pionków
- Typ: neodymowy
- Ilość: 32
- Zastosowanie: aktywacja czujników halla
- Uwagi:
  - jeden magnes na pionek
  - biegunowość bez znaczenia

---

## Ekspandery GPIO

### MCP23018-E/SP
- Typ: I2C GPIO expander
- Ilość: TBD (w zależności od topologii)
- Zastosowanie: odczyt stanu pól
- Uwagi:
  - adresy I2C konfigurowalne
  - preferowane krótkie linie

---

## Kontroler

### ESP8266
- Typ: NodeMCU / bare ESP
- Zastosowanie:
  - logika gry
  - serwer HTTP
  - zapis danych
- Uwagi:
  - działa jako single source of truth

---

## Sygnalizacja

### Brzęczek
- Typ: aktywny / pasywny (do ustalenia)
- Zastosowanie: feedback użytkownika
- Uwagi:
  - sterowany z logiki gry
  - przez tranzystor

---

## Pamięć

### Karta SD + moduł
- Zastosowanie: zapis historii partii
- Uwagi:
  - zapis atomowy
  - odporność na reset
