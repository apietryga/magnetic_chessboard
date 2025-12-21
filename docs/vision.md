# Vision – Smart Chessboard

## Cel produktu
Stworzenie fizycznej, inteligentnej szachownicy, która automatycznie wykrywa ruchy pionków,
rejestruje przebieg partii i synchronizuje dane z aplikacją, działając również w trybie offline.

Produkt ma być:
- autonomiczny
- odporny na brak sieci
- możliwy do dalszej rozbudowy

## Zakres
System obejmuje:
- fizyczną szachownicę z czujnikami (czujniki Hall'a)
- mikrokontroler ESP8266
- ekspandery GPIO MCP23018-E/SP
- zapis danych lokalnie (karta SD)
- komunikację z aplikacją
- sygnalizację dźwiękową (brzęczek)

## Co ten projekt robi
- wykrywa podniesienie i postawienie pionka
- interpretuje to jako ruch
- zapisuje ruchy lokalnie
- synchronizuje je z aplikacją, gdy dostępne jest połączenie
- informuje użytkownika dźwiękiem o stanie systemu (np. błąd, nielegalny ruch)

## Czego ten projekt NIE robi
- nie analizuje strategii gry
- nie liczy rankingu
- nie gra przeciwko użytkownikowi (brak AI)
- nie polega wyłącznie na chmurze

## Filozofia
- hardware jest możliwie prosty
- logika gry znajduje się poza mikrokontrolerem
- system działa offline-first
- każdy element projektu jest modułowy i wymienialny
