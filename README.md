# SzafkaSkyPvP — Paper 1.21.4

Wersja konfiguracji dla trybu **SkyPvP**.

## Budowanie
Wymagania: Java 21, Maven, Paper 1.21.4.
W folderze projektu:
```bash
mvn clean package
```
JAR: `target/SzafkaSkyPvP-1.0.0.jar` — wrzuć do `plugins/` odpowiedniego serwera.

## GUI i komunikaty
- `/szafka`: 54 sloty; kostiumy na dole po lewej, pety po prawej, sklep/przedłużenia pośrodku.
- Po założeniu: zielony tytuł na środku ekranu, np. `Założono kostium Kostium Koksa` lub `Założono peta Pszczółka`.
- Po zdjęciu: czerwony tytuł na środku ekranu, np. `Zdjąłeś kostium Kostium Koksa` lub `Zdjąłeś peta Pszczółka`.

## Komendy
`/kosmetyki give <gracz> <kostium|pet> <id> <dni>`
`/kosmetyki extend <gracz> <kostium|pet> <id> <dni>`
`/kosmetyki coins <gracz> <kwota>`
`/kosmetyki crate <gracz> <kostium|pet>`
`/kosmetyki reload`

Uwaga: to projekt źródłowy, nie skompilowany JAR. Nie uruchamiałem kompilacji w tym środowisku. Wygląd kostiumu/peta jest obecnie prototypowy i używa wyświetlanego przedmiotu; pełne modele wymagają resource packa i dalszej implementacji.

## Ikony kostiumów i petów
- Kostiumy mogą używać `LEATHER_CHESTPLATE` z `color: "#RRGGBB"` albo główki z HeadDatabase.
- Pety mogą używać główek z HeadDatabase.
- `hdb-id` jest opcjonalne. Gdy HeadDatabase jest zainstalowane i wpiszesz prawidłowe ID, plugin spróbuje pobrać główkę przez API; bez HDB użyje zwykłego przedmiotu zastępczego.
- Wpisz prawdziwe ID główek do `hdb-id` w `config.yml`. Puste pole nie pobiera główki.
- Po zmianie konfiguracji wykonaj `/kosmetyki reload`.

## Opisy, efekty i ikony
Każdy kostium i pet ma własną nazwę, opis i efekt konfigurowany w `config.yml`.
- Efekty są włączane, gdy kosmetyk jest założony i odświeżane cyklicznie.
- Kostiumy używają barwionych skórzanych napierśników (kolor `#RRGGBB`).
- Pole `hdb-id` można uzupełnić ID główki z HeadDatabase; jeśli HDB jest dostępne, plugin spróbuje pobrać ikonę. Puste ID oznacza ikonę zastępczą.
- Dla uczciwego PvP bonusy są ograniczone do efektów I poziomu; w razie potrzeby można je wyłączyć, ustawiając `effects: []`.

## Przedłużenia i komendy admina
- W sklepie kliknij kosmetyk, a potem wybierz przedłużenie na 7, 14 lub 30 dni.
- Cena skaluje się proporcjonalnie do ceny bazowej (7 dni = cena bazowa).
- Lore pokazuje pozostały czas oraz dokładną datę wygaśnięcia `dd.MM.yyyy HH:mm`.
- `/kosmetyki give <gracz> <kostium|pet> <id> [dni]` nadaje kosmetyk na podany czas (domyślnie 7 dni).
- `/kosmetyki extend <gracz> <kostium|pet> <id> <dni>` dodaje czas do aktualnej daty wygaśnięcia.
Przykłady:
`/kosmetyki give Steve kostium koks 30`
`/kosmetyki give Steve pet bee 14`
`/kosmetyki extend Steve kostium koks 7`
Dostępne ID są w `config.yml`.

## Wariant z motywami i poprawionym nadawaniem
- `/kosmetyki give <gracz> <kostium|pet> <id> [dni]` zapisuje własność, dodaje ikonę-token do ekwipunku i automatycznie zakłada kosmetyk.
- Kliknięcie prawym przyciskiem trzymanego tokenu ponownie zakłada kosmetyk.
- Motywy SkyPvP: Lotnik, Feniks, Nocny Sokół; pety: Lis Polarny, Mały Feniks, Nietoperz Cienia.
- Motywy LifeSteal: Wampir, Krwawy Baron, Feniks Krwi; pety: Kruk Wampira, Nietoperz, Krwawy Lisek.
- Ikony wykorzystują numery główek HeadDatabase (wymagany zainstalowany plugin HeadDatabase).
- To są ikony główek i efekty cząsteczkowe, nie kompletne modele postaci. Pełne kostiumy jak na serwerach z custom armor wymagają resource packa i kompatybilnego pluginu/modeli.
