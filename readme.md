+-----------------+       +------------------+        +-----------------+
|   urzadzenie 1  | <---> |  Raspberry Pi 4B | <----> |  urzadzenie 2   |
+-----------------+       +------------------+        +-----------------+
       ^                         ^
       |                         |
monitor zmian         przechowuje master kopię
i synchronizacja       i rozsyła zmiany



### Podzial na komponenty 

1. Modul monitorujacy folder
 - wykrywa zmiany plikow (dodanie, usuniecie, modyfikacja)

2. Modul klienta siceiowego
 - po wykreciu zmiany - polacz sie z serwerem i wyslij dane 
 -> prosty komunikaty 

3. Modul serwera
 - nasluguje polaczen od klientow i odbiera zmiany, zapisuje pliki

4. Modul porownywania wersji
 - ustala czy dana wersja pliku jest ta nowsza
 -> rozwazenie nadpisywania

5. Modul synchornizujacy lokalnie
 - odbiera zmiany of serwera i zapisuje je u siebie
 





Szkielet klienta;
Loop:
    Sprawdź zmiany plików
    Jeśli zmiana:
        Dodaj do kolejki wysyłki

Co kilka sekund:
    Jeśli kolejka niepusta:
        Nawiąż połączenie TCP z serwerem
        Wyślij dane zmodyfikowanego pliku


Szkielet RP;
Loop:
    Czekaj na połączenia TCP
    Jeśli połączenie:
        Odbierz zmianę
        Zapisz plik
        Zaktualizuj stan wersji
        Oznacz plik jako zmieniony dla innych klientów




### Minimalna wersja 
 - synchornizacja jednego folderu
 - tylko detekcja modyfikacji (bez usuwania/dodawania)
 - prosty schematy komunikacji (np. tekstowy)
 - obsluga dwoch komputerow (klient <-> serwer))
