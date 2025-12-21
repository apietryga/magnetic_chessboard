# Edge Case – Physical / Logical Desynchronization

## Opis problemu

System dopuszcza sytuację, w której fizyczne położenie figur
nie odpowiada logicznemu stanowi gry.

Przykłady:
- cofnięcie nielegalnego ruchu
- przypadkowe przesunięcie figury
- dotknięcie pionka bez wykonania ruchu

---

## Zachowanie systemu

### Wykrycie
- Board Scanner wykrywa zmianę
- Move Interpreter nie potrafi zbudować poprawnego ruchu

### Reakcja
- brak zmiany stanu gry
- sygnał dźwiękowy: ERROR / WARNING
- UI informuje o niespójności

---

## Rola użytkownika

- użytkownik przywraca poprawne położenie figur
- system nie „naprawia” planszy automatycznie

---

## Uzasadnienie
Automatyczna korekta:
- zwiększa złożoność
- zwiększa ryzyko błędów
- utrudnia debugowanie

Decyzja:
**stan logiczny jest nadrzędny nad fizycznym.**
