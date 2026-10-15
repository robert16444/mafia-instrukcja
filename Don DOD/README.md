# Don DOD - Discord Bot dla Mafii DOD

Bot Discordowy obsługujący system aktywności i rang XP, rozgrywki Mafii, zapisy na gry online, wydarzenia Discorda oraz organizację konwentów.

Projekt został przygotowany z myślą o jednym głównym serwerze Discord i przechowuje dane lokalnie w bazie SQLite.

## Spis treści

- [Najważniejsze funkcje](#najważniejsze-funkcje)
- [System XP](#system-xp)
  - [Total XP](#total-xp)
  - [Chat XP](#chat-xp)
  - [VC XP](#vc-xp)
  - [Mafia XP](#mafia-xp)
  - [Manual XP](#manual-xp)
  - [Migracja starego systemu](#migracja-starego-systemu)
  - [Rangi](#rangi)
  - [Poziomy](#poziomy)
- [Profile i rankingi](#profile-i-rankingi)
- [Konwenty](#konwenty)
  - [Tworzenie konwentu](#tworzenie-konwentu)
  - [Samodzielne dołączanie](#samodzielne-dołączanie)
  - [Nowa osoba podczas trwania konwentu](#nowa-osoba-podczas-trwania-konwentu)
  - [Kilka konwentów jednocześnie](#kilka-konwentów-jednocześnie)
  - [Archiwizacja](#archiwizacja)
- [Zapisy na rozgrywki online](#zapisy-na-rozgrywki-online)
- [Zaplanowane wydarzenia Discorda](#zaplanowane-wydarzenia-discorda)
- [Komendy](#komendy)
- [Hierarchia ról](#hierarchia-ról)

---

## Najważniejsze funkcje

Bot obsługuje:

- automatyczny system XP za wiadomości,
- automatyczny system XP za aktywność na kanałach głosowych,
- Mafia XP przyznawane za rozgrywki,
- ręczne korekty XP wykonywane przez Game Masterów,
- 100 poziomów progresji,
- automatyczne role zależne od Total XP,
- jednorazową migrację starych ról do nowego systemu,
- profile użytkowników,
- rankingi Total XP, Mafia XP, VC XP i Chat XP,
- tworzenie i archiwizację konwentów,
- role i prywatne kanały konwentowe,
- samodzielne zapisywanie się na konwenty przez przycisk,
- automatyczne przypisywanie nowej osoby do trwającego konwentu,
- obsługę kilku jednocześnie trwających konwentów,
- zapisy na rozgrywki online,
- deklarowanie najwcześniejszej godziny dostępności,
- automatyczne liczenie dostępnych graczy w kolejnych godzinach,
- tworzenie natywnych Zaplanowanych Wydarzeń Discorda,
- pingowanie osób, które według deklaracji powinny być już dostępne,
- trwałe przyciski działające również po restarcie bota,
- trwałe przechowywanie danych w SQLite.

---

# System XP

## Total XP

Każdy użytkownik posiada kilka niezależnych liczników:

```text
Total XP = Chat XP + VC XP + Mafia XP + Manual XP + Migration XP
```

`Total XP` jest używane do:

- wyliczania poziomu,
- ustalania aktualnej rangi,
- automatycznego nadawania i odbierania ról rangowych,
- rankingu Total XP.

---

## Chat XP

Za poprawną wiadomość użytkownik otrzymuje:

```text
+2 XP
```

Bot posiada zabezpieczenia przed prostym farmieniem punktów.

Wiadomość zapunktuje tylko wtedy, gdy:

- została wysłana przez prawdziwego użytkownika,
- została wysłana na kanale tekstowym,
- kanał nie ma wyłączonego Chat XP,
- zawiera minimum 8 znaków po normalizacji,
- zawiera rzeczywistą treść, a nie wyłącznie emoji,
- od poprzedniej punktowanej wiadomości użytkownika minęło minimum 20 sekund,
- nie jest w co najmniej 90% podobna do poprzedniej punktowanej wiadomości.

Linki są normalizowane przy porównywaniu wiadomości, a custom emoji są pomijane.

Administrator może wyłączyć naliczanie punktów na konkretnym kanale:

```text
/xp-kanal-wylacz
```

oraz ponownie je włączyć:

```text
/xp-kanal-wlacz
```

---

## VC XP

Na kanałach głosowych bot nalicza:

```text
1 XP za każde 120 sekund
```

czyli maksymalnie około:

```text
30 XP / godzinę
```

### Warunki naliczania VC XP

- na kanale muszą znajdować się minimum 2 osoby niebędące botami,
- kanał AFK serwera nie daje XP,
- bot nie musi wchodzić na kanał głosowy,
- pozostałe sekundy są zapisywane w bazie i przenoszone na kolejne naliczenie.

Przykład:

```text
90 sekund przed restartem + 30 sekund po restarcie = 1 VC XP
```

### Self-deaf

Po włączeniu `self-deaf` użytkownik ma 10 minut okresu tolerancji.

Po przekroczeniu tego czasu VC XP przestaje być naliczane aż do wyłączenia self-deaf.

Zmiana kanału, opuszczenie VC lub zmiana stanu self-deaf resetuje licznik ciągłego self-deaf.

Bot nie nalicza sztucznego czasu po restarcie lub utracie połączenia z Discordem.

---

## Mafia XP

Mafia XP jest przyznawane ręcznie przez GM-a lub administratora za konkretną rozgrywkę.

| Aktywność | XP |
|---|---:|
| Udział w pełnej rozgrywce | 150 |
| Wygrana | 50 |
| Prowadzenie jako GM | 250 |
| Pomocniczy GM / co-GM | 100 |

Komenda:

```text
/mafia-xp
```

Każda nagroda zawiera `ID gry`.

Bot blokuje ponowne przyznanie tej samej osobie tego samego typu nagrody dla tego samego ID gry.

Przykładowo użytkownik może dostać za tę samą grę:

- udział,
- wygraną,

ale nie może dostać dwa razy nagrody `udział` dla tego samego `ID gry`.

### Event specjalny

Parametr `event_specjalny` uruchamia mnożnik:

```text
x1.5
```

Przykłady:

| Aktywność | Normalnie | Event specjalny |
|---|---:|---:|
| Udział | 150 XP | 225 XP |
| Wygrana | 50 XP | 75 XP |
| GM | 250 XP | 375 XP |
| co-GM | 100 XP | 150 XP |

---

## Manual XP

Osoba posiadająca rolę Game Mastera może ręcznie skorygować punkty użytkownika:

```text
/dodaj-punkty
```

Przykłady:

```text
/dodaj-punkty osoba:@User punkty:500
```

Dodaje:

```text
+500 Manual XP
```

Natomiast:

```text
/dodaj-punkty osoba:@User punkty:-500
```

odejmuje:

```text
-500 Manual XP
```

Zakres pojedynczej operacji:

```text
-1 000 000 do +1 000 000 XP
```

Wartość `0` jest odrzucana.

### Zabezpieczenie przed ujemnym Total XP

Bot nigdy nie pozwala, aby `Total XP` spadło poniżej zera.

Jeżeli użytkownik ma 300 Total XP, a GM spróbuje odjąć 500 XP:

```text
żądana korekta: -500 XP
faktyczna korekta: -300 XP
nowy wynik: 0 Total XP
```

### Audyt ręcznych korekt

Każda wykonana korekta jest zapisywana w tabeli:

```text
manual_xp_awards
```

Zapisywane są m.in.:

- ID użytkownika,
- faktycznie zastosowana zmiana XP,
- ID Game Mastera,
- data i godzina operacji,
- status wysłania powiadomienia.

---

## Migracja starego systemu

Komenda:

```text
/migracja-xp
```

jest jednorazową komendą administratora przenoszącą stare role aktywności do nowego systemu XP.

| Stara rola | Migration XP |
|---|---:|
| Jak ch*j Mafia | 100 |
| Cichy/a, ale podejrzany/a | 2 500 |
| Tymczasowo zaufany/a | 10 000 |
| Za długo jest w grze | 50 000 |
| Pierwszy/a do zabicia | 250 000 |

Jeżeli użytkownik posiada kilka starych ról, wybierana jest najwyższa wartość.

Migracja zapisuje również `migration floor`, czyli minimalną rangę zachowaną dla użytkownika.

Dzięki temu osoba, która przed migracją posiadała wyższą rolę, nie zostanie zdegradowana tylko dlatego, że nowe progi są inne niż stare wartości migracyjne.

Flaga zakończenia migracji jest zapisywana dopiero po prawidłowym zakończeniu całej operacji.

Po zakończeniu migracji ponowne wykonanie komendy na tym samym serwerze jest blokowane.

---

## Rangi

Bot automatycznie zarządza pięcioma rangami.

| Próg Total XP | Rola |
|---:|---|
| 500 | Jak ch*j Mafia |
| 5 000 | Cichy/a, ale podejrzany/a |
| 20 000 | Tymczasowo zaufany/a |
| 75 000 | Za długo jest w grze |
| 250 000 | Pierwszy/a do zabicia |

Użytkownik posiada tylko jedną aktualną rolę rangową.

Po zmianie XP bot:

1. oblicza należną rangę,
2. respektuje `migration floor`,
3. usuwa nieaktualne role rangowe,
4. nadaje właściwą rolę.

---

## Poziomy

Bot posiada 100 poziomów.

Poziom jest wyliczany na podstawie Total XP z nieliniową krzywą progresji.

```text
Level 100 = 250 000 XP
```

Poziomy są informacyjne i nie tworzą osobnych ról Discorda.

---

# Profile i rankingi

## Profil

Komenda:

```text
/profil
```

pokazuje profil własny lub wybranego użytkownika.

Profil zawiera:

- Total XP,
- poziom,
- aktualną rangę,
- progres do następnego poziomu,
- Chat XP,
- VC XP,
- Mafia XP,
- Manual XP, jeśli występuje,
- Migration XP, jeśli występuje,
- liczbę rozegranych gier,
- liczbę wygranych,
- liczbę gier prowadzonych jako GM,
- liczbę gier jako co-GM,
- następną rangę.

## Rankingi

Dostępne komendy:

```text
/ranking
/punkty
```

Obsługiwane typy:

- Total XP,
- Mafia XP,
- VC XP,
- Chat XP.

Ranking wyświetla 15 osób na stronę i posiada przyciski do przechodzenia pomiędzy stronami.

Manual XP jest uwzględniane w rankingu `Total XP`, ale nie jest doliczane do rankingów Mafia, VC ani Chat.

---

# Konwenty

## Tworzenie konwentu

Komenda administratora:

```text
/konwent
```

otwiera formularz zawierający:

1. nazwę konwentu,
2. nazwę roli,
3. kolor roli w formacie HEX,
4. zakres dat,
5. treść ogłoszenia dla graczy.

Przykładowe daty:

```text
2026-09-04 -> 2026-09-06
```

Dla zgodności ze starszą wersją można również podać pojedynczą datę:

```text
2026-09-06
```

W takim przypadku jest ona traktowana jako data końca, a data początku jako dzień utworzenia konwentu.

Bot automatycznie tworzy:

- rolę `Będę na <nazwa roli>`,
- prywatny kanał tekstowy,
- ogłoszenie dla graczy z przyciskiem do otrzymania roli.

Kanał jest tworzony w kategorii aktywnych konwentów.

Dostęp otrzymują:

- użytkownicy posiadający rolę danego konwentu,
- sam bot.

`@everyone` nie widzi prywatnego kanału.

Jeżeli którykolwiek z etapów tworzenia konwentu nie powiedzie się, bot próbuje wycofać wcześniej utworzone elementy, aby nie pozostawić niekompletnego konwentu.

---

## Samodzielne dołączanie

Na kanale ogłoszeń konwentowych pojawia się treść wpisana przez administratora oraz przycisk:

```text
Będę na <nazwa konwentu>
```

Kliknięcie przycisku nadaje użytkownikowi odpowiednią rolę.

Jeżeli użytkownik już posiada rolę, bot nie nadaje jej drugi raz.

Przycisk jest trwały i działa również po restarcie procesu bota.

---

## Nowa osoba podczas trwania konwentu

Jeżeli nowa osoba dołączy na serwer podczas trwania aktywnego konwentu, bot automatycznie nada jej rolę tego wydarzenia.

Przykład:

```text
Konwent: 2026-09-04 -> 2026-09-06
```

Automatyczne przypisanie działa:

```text
2026-09-04  TAK
2026-09-05  TAK
2026-09-06  TAK
2026-09-07  NIE
```

Jeżeli trwa dokładnie jeden konwent, dodatkowe potwierdzenie nie jest wymagane.

---

## Kilka konwentów jednocześnie

Jeżeli w dniu dołączenia użytkownika trwa kilka konwentów jednocześnie:

1. bot nada mu role wszystkich aktywnych konwentów,
2. na prywatnym kanale każdego konwentu oznaczy użytkownika,
3. wyświetli pytanie z dwoma przyciskami:
   - `Tak, zostaję`,
   - `Nie, usuń rolę`.

Przycisk może obsłużyć wyłącznie użytkownik, którego dotyczy pytanie.

Wybranie `Nie, usuń rolę` usuwa tylko rolę konkretnego konwentu.

Pytania są zapisywane w bazie i ich przyciski są ponownie rejestrowane po restarcie bota.

---

## Archiwizacja

Co 5 minut bot sprawdza aktywne konwenty.

Konwent zostaje zarchiwizowany dopiero następnego dnia po `end_date`.

Podczas archiwizacji bot:

1. zmienia nazwę roli z `Będę na <konwent>` na samą nazwę konwentu,
2. przenosi kanał do kategorii archiwum,
3. zachowuje dotychczasowe prywatne permission overwrites kanału,
4. wyłącza przycisk w ogłoszeniu,
5. zmienia jego etykietę na `Zapisy zakończone`,
6. zamyka nierozstrzygnięte pytania nowych użytkowników.

---

# Zapisy na rozgrywki online

Komenda:

```text
/zapisy
```

jest dostępna wyłącznie dla osób posiadających faktyczną rolę Game Mastera.

Administrator bez roli GM nie przechodzi tego ograniczenia.

Formularz zawiera:

- nazwę wydarzenia,
- listę dni,
- listę najwcześniejszych godzin startu,
- listę godzin końca.

Przykład:

```text
Nazwa wydarzenia:
Mafia Online

Dni:
2026-09-05, 2026-09-06

Najwcześniejsze starty:
18:00, 17:00

Końce:
02:00, 23:00
```

Liczba dni, startów i końców musi być taka sama.

Jedne zapisy mogą obejmować maksymalnie 7 dni.

Najwcześniejszy start musi znajdować się w przyszłości.

## Przejście przez północ

Jeżeli godzina końca jest wcześniejsza lub równa godzinie początku, bot przyjmuje, że koniec przypada następnego dnia.

Przykład:

```text
18:00 -> 02:00
```

oznacza:

```text
18:00 danego dnia -> 02:00 następnego dnia
```

Jedno okno nie może trwać dłużej niż 24 godziny.

## Zapisy graczy

Bot publikuje panel zapisów na skonfigurowanym kanale i oznacza rolę osób zainteresowanych grami online.

Gracz klika:

```text
Zapisz / zmień dostępność
```

następnie:

1. wybiera dzień,
2. wybiera najwcześniejszą godzinę, od której może grać.

Godziny są generowane w odstępach jednej godziny.

Deklaracja oznacza dostępność od wybranej godziny do końca danego okna.

Przykład:

```text
okno: 17:00 -> 23:00
wybrana dostępność: 19:00
```

Użytkownik jest liczony jako dostępny o:

```text
19:00
20:00
21:00
22:00
23:00
```

ale nie o:

```text
17:00
18:00
```

Ponowne wybranie godziny aktualizuje wcześniejszą deklarację zamiast tworzyć duplikat.

W głównym embedzie bot pokazuje:

- liczbę dostępnych osób dla każdej godziny,
- deklaracje konkretnych użytkowników,
- maksymalnie 20 deklaracji tekstowo dla jednego okna oraz informację o pozostałych.

Zapisy zamykają się o najwcześniejszej godzinie rozpoczęcia ze wszystkich podanych okien.

Po zamknięciu panel pozostaje widoczny historycznie, ale nie przyjmuje nowych zmian.

---

# Zaplanowane wydarzenia Discorda

Podczas tworzenia `/zapisy` bot próbuje utworzyć natywne Zaplanowane Wydarzenie Discorda dla każdego okna czasowego.

Jedno okno oznacza jedno wydarzenie.

Przy kilku dniach powstają osobne wydarzenia, np.:

```text
Mafia Online — 2026-09-05
Mafia Online — 2026-09-06
```

W opisie wydarzenia znajduje się:

- informacja o rozgrywce,
- link do wiadomości z zapisami,
- nazwa Game Mastera, który utworzył zapisy.

Wydarzenie jest przypięte do skonfigurowanego kanału Voice lub Stage.

Jeżeli tworzenie wydarzenia nie powiedzie się, same zapisy pozostają utworzone.

---

# Komendy

| Komenda | Dostęp | Opis |
|---|---|---|
| `/profil [osoba]` | wszyscy | Pokazuje profil XP własny lub innego użytkownika |
| `/ranking [typ]` | wszyscy | Ranking Total, Mafia, VC lub Chat XP |
| `/punkty [typ]` | wszyscy | Alternatywna komenda rankingu z paginacją |
| `/zapisy` | tylko rola GM | Tworzy zapisy na grę online i wydarzenia Discorda |
| `/ping` | GM lub administrator | Pinguje osoby, które według deklaracji powinny być już dostępne |
| `/mafia-xp` | GM lub administrator | Przyznaje XP za konkretną rozgrywkę Mafii |
| `/dodaj-punkty` | tylko rola GM | Dodaje lub odejmuje Manual XP |
| `/konwent` | administrator | Tworzy konwent, rolę, prywatny kanał i ogłoszenie |
| `/migracja-xp` | administrator | Jednorazowo migruje stare role do XP |
| `/xp-kanal-wylacz [kanał]` | administrator | Wyłącza Chat XP na kanale |
| `/xp-kanal-wlacz [kanał]` | administrator | Ponownie włącza Chat XP na kanale |
| `/xp-kanaly-lista` | administrator | Wyświetla listę kanałów, na których wyłączono zdobywanie Chat XP |

> [!NOTE]
> `/zapisy` oraz `/dodaj-punkty` sprawdzają faktyczną rolę GM. Samo posiadanie uprawnienia Administrator nie wystarcza do użycia tych dwóch komend.

---

# Stałe serwera

Aktualna wersja kodu zawiera skonfigurowane na stałe ID elementów serwera.

| Element | ID |
|---|---:|
| Kategoria aktywnych konwentów | `1127965938520686745` |
| Kategoria archiwum konwentów | `1137336493417955449` |
| Kanał ogłoszeń konwentowych | `1127967837340848168` |
| Kanał zapisów online | `1505517553982636112` |
| Rola pingowana przy zapisach online | `1122879832775209092` |
| Kanał Voice/Stage wydarzeń online | `1123845826888876103` |
| Rola Game Master | `1122879978023960618` |
| Odbiorca DM z audytem Manual XP | `399169695846236160` |

### Role rangowe

| Rola | ID | Próg |
|---|---:|---:|
| Jak ch*j Mafia | `1122922705130365061` | 500 XP |
| Cichy/a, ale podejrzany/a | `1122922598393729065` | 5 000 XP |
| Tymczasowo zaufany/a | `1122922468483539045` | 20 000 XP |
| Za długo jest w grze | `1122922327596875856` | 75 000 XP |
| Pierwszy/a do zabicia | `1122914363158827048` | 250 000 XP |

Jeżeli bot ma zostać przeniesiony na inny serwer, wartości te trzeba zmienić w `bot.py`.

---