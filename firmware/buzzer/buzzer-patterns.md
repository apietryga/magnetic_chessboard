# Buzzer Patterns – Smart Chessboard

Brzęczek jest elementem interfejsu użytkownika.
Każdy sygnał dźwiękowy odpowiada **konkretnej decyzji logiki gry**.

Brzęczek:
- reaguje wyłącznie na decyzje Chess Engine
- nie reaguje bezpośrednio na zdarzenia sprzętowe
- daje szybki, jednoznaczny feedback

---

## BOOT_OK
**Wzorzec:**  
- krótki sygnał (100 ms)

**Znaczenie:**  
System uruchomiony poprawnie.

---

## MOVE_OK
**Wzorzec:**  
- dwa krótkie sygnały (2 × 80 ms)

**Znaczenie:**  
Ruch zaakceptowany, stan gry zaktualizowany.

---

## ILLEGAL_LIFT
**Wzorzec:**  
- natychmiastowy długi sygnał (600–800 ms)

**Znaczenie:**  
„Nie ruszaj tej figury. Odłóż ją z powrotem.”

**Kiedy używany:**  
- król jest w szachu  
- podniesiona figura **nie ma żadnego legalnego ruchu**, który usuwa szacha  
- LIFT zostaje odrzucony

---

## ILLEGAL_MOVE
**Wzorzec:**  
- długi sygnał + krótka przerwa + krótki sygnał

**Znaczenie:**  
„Ten ruch jest nielegalny. Cofnij figurę.”

**Kiedy używany:**  
- PLACE wykonany
- ruch FROM → TO nie spełnia reguł gry

---

## CHECK
**Wzorzec:**  
- krótki + długi sygnał

**Znaczenie:**  
Król jest w szachu.

---

## CHECKMATE
**Wzorzec:**  
- 3 krótkie sygnały + długi sygnał

**Znaczenie:**  
Szach-mat, koniec partii.

---

## SYSTEM_ERROR
**Wzorzec:**  
- 3 długie sygnały

**Znaczenie:**  
Błąd systemowy (SD, I2C, krytyczny błąd logiki).

---

## Zasady projektowe

- brak melodii
- brak sygnałów ciągłych
- każdy wzorzec musi być:
  - krótki
  - jednoznaczny
  - łatwy do rozróżnienia

Brzęczek ma informować i dyscyplinować, nie wkurwiać.
