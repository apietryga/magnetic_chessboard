# Risks – Smart Chessboard

## Ryzyka sprzętowe

### Czujniki Halla (Hall Effect)
- błędna orientacja magnesu (polaryzacja)
- zbyt duża odległość magnes–czujnik
- tolerancje progów przełączania (+/− mT)

Mitigacja:
- jednolity standard montażu magnesów w pionkach
- testowy jig do weryfikacji zasięgu przed zalaniem epoksydem
- kalibracja logiczna (wymaganie stabilnego stanu przez X ms)

### Magistrala I2C (MCP23018-E/SP)
- zakłócenia przy długich ścieżkach
- ograniczenia prędkości

Mitigacja:
- niskie taktowanie I2C
- krótkie linie
- testy POC na docelowych długościach

### Brzęczek
- zakłócenia EMI
- pobór prądu w momencie aktywacji

Mitigacja:
- sterowanie przez tranzystor
- izolacja od linii logicznych

---

## Ryzyka materiałowe

### Żywica epoksydowa
- przegrzewanie podczas wiązania
- zmiana właściwości czujników
- trwałe uszkodzenie elektroniki

Mitigacja:
- testy zalewania na prototypach
- dokumentowanie proporcji i czasu wiązania
- separacja elektroniki od głównej masy żywicy

---

## Ryzyka systemowe

### Ghost moves
- częściowe zdjęcie pionka
- przypadkowe dotknięcia

Mitigacja:
- interpretacja ruchu jako pełnej sekwencji
- timeouty i walidacja po stronie aplikacji

### Utrata danych
- błąd zapisu na kartę SD
- brak synchronizacji

Mitigacja:
- buforowanie
- walidacja zapisów
- retry sync

---

## Ryzyka projektowe

### Scope creep
- dokładanie funkcji „bo się da”

Mitigacja:
- sztywny backlog MVP
- dokumentowanie pomysłów poza MVP
