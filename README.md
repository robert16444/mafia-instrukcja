# Mafia Web App – Instrukcja dla GMów

Witaj w aplikacji do prowadzenia gry **Mafia** 🎭.  
Ten dokument jest przeznaczony dla Mistrzów Gry (GM), którzy prowadzą rozgrywki za pomocą tej aplikacji.

---

## 🔑 Logowanie i dołączenie do gry

1. Otwórz stronę aplikacji (link dostarczony przez admina).
2. Wpisz swój **nick** oraz wybierz rolę **GM** (Game Master).
3. Pozostali gracze logują się, wpisując swój nick i wybierając **Gracz**.

---

## 🎲 Przygotowanie lobby

- GM tworzy nowe **lobby gry**.
- Gracze dołączają do lobby wpisując ten sam **ID pokoju**.
- GM widzi listę graczy w lobby.
- GM przydziela każdemu **rolę** (np. Mafia, Policjant, Snajper, Grabarz itd.).
- Kliknięciem przycisku **Rozpocznij grę** – gra startuje.

---

## 🌙 Przebieg gry – fazy dnia i nocy

Gra podzielona jest na fazy:

- **Dzień** ☀️ – gracze dyskutują i mogą głosować na osoby do eliminacji.
- **Noc** 🌙 – poszczególne role budzą się według kolejki.

GM steruje fazami, klikając odpowiednie przyciski:
- **Rozpocznij noc / dzień**
- **Obudź rolę (wg kolejki)** – GM budzi kolejne role zgodnie z ustalonym porządkiem.

---

## 🛠️ Funkcje ról specjalnych

### 👮 Policjant
- W nocy wybiera gracza do sprawdzenia – GM widzi, czy jest pozytywny (🟢), neutralny (🟡) czy negatywny (🔴).

### 🪦 Grabarz
- Może raz w grze przejąć rolę zmarłego gracza.
- Po wykorzystaniu umiejętności Grabarz nie budzi się ponownie.
- W panelu GM pojawia się informacja, jaką rolę przejął.

### 🎯 Snajper
- Zaczyna z **1 pociskiem**.
- W nocy GM wybiera, w kogo Snajper strzela.
- Zasady:
  - trafienie w rolę negatywną (🔴) → Snajper dostaje **kolejny pocisk** następnego ranka.
  - trafienie w rolę neutralną (🟡) → Snajper **nie dostaje** kolejnego pocisku i już się nie budzi.
  - trafienie w rolę pozytywną (🟢) → Snajper ginie razem z ofiarą.
- GM w panelu widzi zawsze, w kogo Snajper strzelił i jaka była rola ofiary.

---

## 📋 Panel GM

GM ma dodatkowe widoki i funkcje:
- podgląd wszystkich ról i statusów graczy,
- kontrolę nad kolejką budzenia ról w nocy,
- informacje o akcjach specjalnych (np. Snajper strzelił, Grabarz przejął rolę),
- przyciski do resetowania gry.

---

## 🔄 Reset gry (powrót do lobby)

- GM może w dowolnym momencie kliknąć **Reset gry**.
- Reset powoduje:
  - wyczyszczenie logów (akcje Snajpera, Grabarza, narracji),
  - przywrócenie lobby do stanu początkowego,
  - gracze wracają do widoku poczekalni.

---

## 💡 Dodatkowe funkcjonalności

- **Log narracyjny** – na dole widoczne są podsumowania akcji specjalnych (np. strzał Snajpera, wybór Grabarza).
- **Synchronizacja stanu** – GM i gracze widzą na bieżąco aktualizacje.
- **Blokady ról** – Snajper budzi się tylko, jeśli ma amunicję. Grabarz tylko, jeśli nie użył jeszcze mocy.

---

## 🐛 Zgłaszanie błędów i pomysłów

Chcesz zgłosić błąd lub zaproponować nowy feature?

1. Wejdź na stronę repozytorium (GitHub).
2. Kliknij zakładkę **Issues**.
3. Kliknij **New Issue**.
4. Opisz:
   - co się wydarzyło (lub czego brakuje),
   - kroki do odtworzenia problemu,
   - ewentualne screeny.

➡️ Dzięki temu wszystkie zgłoszenia będą uporządkowane i łatwe do śledzenia.

---

## ✅ Podsumowanie

Ta aplikacja ma na celu uproszczenie prowadzenia gry Mafia przez internet.  
Rolą GM jest:
- przygotować lobby,
- przypisać role,
- zarządzać fazami dnia i nocy,
- dbać o narrację i klimat rozgrywki.

Miłej gry! 🎉
