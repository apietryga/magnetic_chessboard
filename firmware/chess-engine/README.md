# Chess Engine – MVP Scope

## Rola silnika
Chess Engine jest jedynym komponentem systemu posiadającym pełny i autorytatywny
stan gry. Wszystkie decyzje dotyczące legalności ruchów zapadają w tej warstwie.

Silnik działa całkowicie offline.

---

## Reprezentacja planszy

- plansza 8x8
- indeksowana logicznie (a1–h8)
- przechowywana jako tablica 64 pól

Każde pole zawiera:
- typ figury
- kolor
- flagi pomocnicze (np. czy figura była ruszana)

---

## Obsługiwane reguły (MVP)

### Ruchy figur
- pion
- wieża
- skoczek
- goniec
- hetman
- król

### Zasady
- naprzemienne tury
- wykrywanie szacha
- zakaz ruchu pozostawiającego króla w szachu
- nie każda figura może być w ogóle podniesiona.

---

## Reguły NIEobsługiwane (MVP)

- roszada
- en passant
- promocja pionka (domyślnie hetman lub brak)
- remis (pat, 50 ruchów, trzykrotne powtórzenie)

> Cel: prostota i stabilność, nie kompletność FIDE.

---

## Interfejs silnika

### Wejście
- validate_move(from, to) -> RESULT

### Wyniki
- MOVE_OK
- ILLEGAL_MOVE
- CHECK
- CHECKMATE

---

## Zarządzanie stanem
- stan gry przechowywany w RAM
- po każdym legalnym ruchu:
  - aktualizacja stanu
  - zapis na SD
