# Mafia Web App – Instrukcja dla GM-ów

Witaj w aplikacji do prowadzenia gry **Mafia**.  
Ten dokument jest przeznaczony dla Mistrzów Gry (GM), którzy prowadzą rozgrywki przy pomocy tej aplikacji.

> **Hasło GM** znają GM-owie. Jeśli go nie masz – **zapytać Mańka**.  
> Aplikacja zapamiętuje sesję – **odświeżenie karty nie wyrzuca z gry**. W prawym górnym rogu jest przycisk **Wyjdź** (powrót do ekranu logowania i wyczyszczenie sesji).

---

## Logowanie i dołączenie do gry

1. Otwórz stronę aplikacji - obecny link to http://83.168.88.69/.
2. Wpisz **nick**, zaznacz **GM** i podaj **hasło GM**.
3. Gracze logują się, wpisując **nick** i wybierając **Gracz**.
4. Po odświeżeniu karty GM i gracze **automatycznie wracają** do gry.  
   W razie potrzeby użyj **Wyjdź** (prawy górny róg), aby wrócić do ekranu logowania.

---

## Przygotowanie lobby

- GM tworzy **lobby**. Gracze dołączają, używając linku dostarczonego przez GMa.
- Gracze trafiają do **poczekalni**, gdzie są do momentu rozpoczęcia gry. Mogą dołączyć też po starcie gry, ale to GM ich wtedy **akceptuje/odrzuca**.
- GM **przydziela role** oraz — w razie potrzeby — **oznaczenia/statusy** (patrz niżej).
- **Sąsiedzi**: **zawsze wybierz 2 sąsiadów**.
- **Siostry (Kawaii/Kowai)**: po wyborze jednej **druga wybiera się automatycznie**.
- Kliknięcie **Rozpocznij grę** — start rozgrywki.

---

## Przebieg gry – fazy dnia i nocy

- **Dzień** – dyskusja, **nominacje** i **głosowania** (egzekucja).
- **Noc** – role budzą się wg **Kolejności budzenia**.

W panelu **Fazy dnia**:
- przełączasz **Dzień/Noc**; **zmiana fazy resetuje elementy drugiej fazy**, więc **pilnuj kolejności i klikania**,
- w Dniu obsługujesz nominacje → głosowanie → egzekucję,
- w Nocy budzisz role (pojedynczo lub grupowo) i moderujesz ich czaty oraz akcje.

> **Uwaga:** część przycisków jest **aktywna/nieaktywna** zależnie od **fazy** i **warunków** (np. Snajper tylko z amunicją).

---

## Panel GM (omówienie paneli)

### 1) Lobby / Poczekalnia
- Lista oczekujących: **Akceptuj/Odrzuć**.
- Wstępne przydzielanie ról i oznaczeń.
- Podgląd liczby graczy, ról i statusów.

### 2) Fazy dnia
- **Przełączanie Dzień/Noc** (pamiętaj: każda zmiana **czyści** elementy drugiej fazy).
- **Dzień**: nominacje → głosowanie → egzekucja.
- **Noc**: szybkie budzenie ról i podgląd logów nocnych.
- Opisy pod przyciskami podpowiadają, **co można robić w danej fazie**.

### 3) Kolejność budzenia (noc)
- **Przeciągaj i upuszczaj** role, aby ustawić kolejkę budzenia.
- Po edycji **kliknij Zapisz**.
- Możesz **usunąć** rolę z kolejki i później **przywrócić**.
- Dla części ról dostępne jest:
  - **budzenie pojedyncze** (GM klika *Następny gracz*),
  - **budzenie grupowe** (wszyscy członkowie naraz).

### 4) Czaty ról + sterowanie mocami
- Każda rola ma **czat**; pod czatem mogą być **przyciski sterowania mocą** (jeśli dana rola to wspiera).
- GM może **ukryć treść kanału „Zgon”** u siebie.

### 5) Wydarzenia specjalne
- **Idą święta** – aktywacja mocy Mikołajki.
- **Zemsta Yandere** – użyć po śmierci **Senpaia** - Yandere staje się czerwona i zaczyna zabijać co noc.
- **KPN** – rozpoczęcie **kamień–papier–nożyce** między dowolnymi osobami z dowolnego powodu.
- **Błazen - kradzież karty** – **kradzież karty Błazna**.
- **Tworzenie kochanków** – utworzenie pary w dowolnym momencie.

### 6) Narracja i logi
- **Log narracyjny** – podsumowania akcji (strzały, przejęcia ról itp.).
- Dodatkowe logi (np. **Snajper**, **Grabarz**).
- Znajduje się na samym dole strony.

### 7) Prywatny chat z graczem
- GM może **pisać do graczy na priv** w dowolnym momencie (zliczane nieprzeczytane).

### 8) Reset / Narzędzia
- **Reset gry** – czyści logi, zamyka czaty ról i wraca do **poczekalni**.

---

## Reset gry (powrót do lobby)

- Kliknij **Reset gry** (panel GM).
- Skutki:
  - czyszczenie logów (Snajper, Grabarz, narracja),
  - zamknięcie czatów ról,
  - powrót do **poczekalni**.
- **Zgon** można **cofnąć tylko w tej samej fazie** (tej samej nocy/dniu). Po zmianie fazy jest **permanentny**.

---

## Dodatkowe funkcjonalności

- **Auto-powrót po odświeżeniu** (GM i gracze) + **Wyjdź** (prawy górny róg).
- **Synchronizacja stanu** w czasie rzeczywistym.
- **Role z limitami/blokadami** – niektóre przyciski działają tylko przy spełnionych warunkach (np. Snajper z amunicją, Szekspir tylko **Noc 1**).

---

## Oznaczenia i statusy (co kontroluje GM)

> System wspiera automatycznie część efektów, ale **to GM odpowiada za poprawny stan gry** (nadawanie, zdejmowanie, rozstrzyganie sporów).

### Zasady ogólne
- **Ojciec Chrzestny** to **oznaczenie** – aby dodać go **w trakcie gry**, **nadaj oznaczenie** wybranemu graczowi.
- **Zawsze wybierz 2 sąsiadów**.
- **Siostry (Kawaii/Kowai)**: po wyborze jednej **druga wybiera się automatycznie**.

### Kategorie oznaczeń (z przykładami)

- **Jednoosobowe (może je mieć tylko 1 osoba),**  
- **Czasowe (znikają po 1 nocy/dniu),** 
- **Powiązane (znikają po śmierci roli/partnera).**

---

## Role – specjalne mechaniki (wdrożone przykładowo)

- **Snajper** – budzi się tylko z **amunicją**; strzały w logu; po wykorzystaniu zasobów blokuje się.
- **Grabarz** – **jednorazowo** przejmuje rolę zmarłego; po użyciu mocy zablokowany do końca gry.
- **Lunatyk** – wybiera rolę na **jedną noc** i jest traktowany jak obudzony z tą rolą.
- **Szekspir** – budzi się **wyłącznie w Nocy 1**.
- **Hetera / Ojciec Chrzestny** – **Ojciec Chrzestny** to oznaczenie mafijne (nadaj ręcznie); interakcje z czatem mafii.
- **Snajper** – budzenie **grupowe**; w **Kolejności budzenia** można przełączyć na budzenie **pojedyncze**.

---

## Zgłaszanie błędów i pomysłów

1. Wejdź do repozytorium (GitHub) → **Issues** → **New Issue**.
2. Opisz:
   - co się wydarzyło / czego brakuje,
   - kroki do odtworzenia,
   - screeny (jeśli możesz).

---

## Podsumowanie

Aplikacja upraszcza prowadzenie Mafii online. Zadania GM-a:

- przygotować lobby i **przydzielić role**,
- **zarządzać fazami** dnia i nocy,
- dbać o **oznaczenia/statusy** i zależności między rolami,
- korzystać z **Kolejności budzenia**, **Czatów ról** (ze sterowaniem mocą), **Wydarzeń specjalnych**,
- prowadzić narrację i klimat.

**Nie znasz hasła GM? Zapytaj Mańka.**  
**Odświeżenie nie wyrzuca**, a **Wyjdź** (prawy górny róg) wraca do logowania.  
**Niektóre guziki działają tylko w odpowiedniej fazie/sytuacji** — to normalne.

Miłej gry! 🎭
