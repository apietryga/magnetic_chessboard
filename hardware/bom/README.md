# Bill of Materials (BOM)

Ten katalog zawiera kompletną dokumentację zakupową projektu Smart Chessboard.

Celem BOM nie jest tylko lista części, ale:
- umożliwienie łatwego odtworzenia projektu
- centralizacja informacji o podzespołach
- możliwość szybkiej zmiany dostawcy
- reuse w kolejnych projektach

---

## Struktura
```
hardware/bom/
├── README.md # ten plik
├── components.md # co jest potrzebne i do czego
└── vendors.md # gdzie to kupić + alternatywy
```


---

## Jak z tego korzystać

### 1. `components.md`
Opisuje:
- **jakie** elementy są używane
- **do czego** służą
- **ile** sztuk potrzeba
- ważne uwagi techniczne

Ten plik jest niezależny od dostawców.

---

### 2. `vendors.md`
Opisuje:
- **gdzie** kupić komponenty
- preferowanych dostawców
- alternatywne źródła
- ryzyka zakupowe

Można go aktualizować bez zmiany projektu.

---

## Zasady BOM

- BOM nie zawiera linków do pojedynczych aukcji (chyba że konieczne)
- zawsze planowany jest zapas (+10–20%)
- komponent musi mieć:
  - nazwę
  - funkcję
  - krytyczne parametry
- zmiany w BOM → commit + krótki opis

---

## Status BOM

- [x] wstępny (POC)
- [ ] MVP
- [ ] produkcyjny

Aktualny status: **POC**

---

## Uwagi końcowe

BOM jest częścią dokumentacji technicznej produktu,
a nie jednorazową checklistą zakupową.
