# Game History Storage – SD Card

## Cel
Zapewnienie trwałego zapisu historii partii niezależnie od:
- restartu systemu
- braku połączenia z klientem

---

## Format zapisu

### Plik
- jeden plik = jedna partia
- format tekstowy (łatwy debug)

### Nazewnictwo
- game_YYYYMMDD_HHMM.txt

## Format linii

<move_number> <color> <from> <to> <timestamp>

### Przykład
```
1 W e2 e4 1730000000
1 B e7 e5 1730000012
2 W g1 f3 1730000030
```

---

## Zasady zapisu

- zapis tylko po legalnym ruchu
- zapis atomowy (append)
- flush po każdej linii

---

## Odtwarzanie gry

Podczas uruchomienia:
- ostatnia partia jest wczytywana
- stan gry odbudowywany sekwencyjnie

W przypadku błędu:
- plik oznaczony jako uszkodzony
- nowa partia