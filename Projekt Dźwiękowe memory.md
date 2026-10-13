---
tags: [projekt, raspberry, react]
status: pomysł
start: 2026-10-13
---

# Projekt: Dźwiękowe memory

> [!quote] Pierwotny zamysł
> Mata wielkości planszy do Twistera z czujnikami stanięcia. Kiedy ktoś stanie na polu, w aplikacji odtwarza się dźwięk przypisany do tego pola — i tak rozwiązuje się memory.

Tablica zadań: [[Kanban - Dźwiękowe memory]] · Poradnik: [[Wstęp do obsidian]]

## Opis

Klasyczne memory, ale zamiast odkrywać obrazki, **odkrywa się dźwięki — stopami**. Gracz staje na polu → słyszy dźwięk → staje na drugim polu → jeśli dźwięki są takie same, para jest odkryta. Gra łączy ruch, pamięć słuchową i zabawę w grupie.

**Dla kogo:** dzieci, imprezy, zajęcia ruchowe/terapeutyczne; dzięki temu, że gra opiera się na słuchu, może być dostępna także dla osób niewidomych i słabowidzących.

## Zasady gry

1. Na starcie gra losowo przypisuje dźwięki do pól (każdy dźwięk dwa razy).
2. Gracz staje na pierwszym polu → odtwarza się dźwięk.
3. Gracz staje na drugim polu → odtwarza się dźwięk.
4. Para pasuje → dźwięk sukcesu, pole się podświetla (zielone), punkt dla gracza.
5. Nie pasuje → dźwięk błędu, ruch przechodzi na kolejnego gracza.
6. Koniec, gdy wszystkie pary są odkryte → ekran z wynikami i czasem.

## Architektura

```
 [ Mata z czujnikami ]
          │  (przewody → GPIO)
          ▼
 [ Raspberry Pi ] ── backend w Pythonie: odczyt czujników + logika gry
          │  WebSocket (zdarzenie: "naciśnięto pole 7")
          ▼
 [ Aplikacja React ] ── odtwarza dźwięki, pokazuje planszę, wyniki
   (ekran/telewizor przy Pi albo telefon/tablet w tej samej sieci Wi‑Fi)
```

### Sprzęt — Raspberry Pi

**Rekomendacja: Raspberry Pi 4 (4 GB) lub Pi 5.** Ma GPIO do czujników, Wi‑Fi do komunikacji z telefonem, wyjście HDMI/audio i daje radę uruchomić przeglądarkę z aplikacją React w trybie kiosku — jedno urządzenie robi wszystko.

| Element | Propozycja | Uwagi |
|---|---|---|
| Komputer | Raspberry Pi 4/5 + zasilacz + karta microSD 32 GB | system: Raspberry Pi OS |
| Czujniki pól | **domowe przełączniki foliowe**: dwie warstwy folii aluminiowej/taśmy miedzianej przedzielone dziurkowaną pianką | najtańsze, działają jak przycisk (0/1) |
| Alternatywa | czujniki FSR lub Velostat | mierzą siłę nacisku, ale wymagają przetwornika ADC (np. MCP3008) |
| Rozszerzenie GPIO | ekspander **MCP23017** (I²C, 16 wejść) | przy 16+ polach brakuje wolnych pinów |
| Podświetlenie | taśma LED **WS2812B** pod polami | opcjonalnie, efekt „wow” |
| Dźwięk | głośnik przez HDMI/jack lub głośnik Bluetooth | |
| Mata | gruba mata piankowa / plandeka, pola wycięte i oklejone | wymiar ok. 1,5 × 1,5 m jak Twister |

**Wielkość planszy:** start od **4 × 4 = 16 pól (8 par)**. Kolejne poziomy: 4 × 5 lub 5 × 6.

### Oprogramowanie

**Frontend — React (najlepszy wybór):**
- **Vite + React + TypeScript** — szybki start projektu i wygodny rozwój.
- Dźwięki: **Howler.js** albo Web Audio API (niskie opóźnienie, wiele dźwięków naraz).
- Komponenty: `Plansza`, `Pole`, `PanelGraczy`, `EkranWyników`, `Ustawienia`.
- Stan gry: `useReducer` lub **Zustand**.
- Działa w przeglądarce, więc ta sama aplikacja chodzi na ekranie Pi i na telefonie.
- Tryb **symulacji klawiaturą/myszką** — można rozwijać i testować grę bez gotowej maty!

**Backend — na Raspberry Pi:**
- **Python + gpiozero** (odczyt przycisków, debouncing) + **FastAPI** z WebSocketem.
- Alternatywa: **Node.js** (`onoff` + `ws`) — jeden język z Reactem.
- Pi serwuje też zbudowaną aplikację React; Chromium uruchamiany w trybie `--kiosk` po starcie systemu.

**Przepływ zdarzeń:** czujnik → backend wykrywa naciśnięcie (z filtrem drgań ~50 ms) → wysyła `{ "pole": 7 }` przez WebSocket → React odtwarza dźwięk i aktualizuje stan gry.

## Pomysły na rozszerzenia
- 🎵 **Paczki dźwięków:** zwierzęta, instrumenty, nuty (gama), głosy znajomych, efekty z gier.
- 👥 **Tryb wieloosobowy** z punktacją i turami.
- ⏱️ **Tryb na czas** i ranking najlepszych wyników.
- 🎹 **Tryb „pianino”** — mata jako wielkie klawisze, swobodne granie.
- 🔁 **Tryb Simon** — zapamiętaj i powtórz coraz dłuższą sekwencję dźwięków.
- 📱 Telefon jako pilot: wybór trybu, liczby graczy i paczki dźwięków.
- 💡 Animacje LED po odkryciu pary.

## Szacunkowy budżet

| Pozycja | Koszt (ok.) |
|---|---|
| Raspberry Pi 4/5 + zasilacz + karta SD | 300–450 zł |
| Ekspander MCP23017 + przewody + płytka | 40 zł |
| Folia/taśma miedziana, pianka, mata | 80–150 zł |
| Taśma LED WS2812B (opcjonalnie) | 60 zł |
| Głośnik | 0–100 zł |
| **Razem** | **~500–750 zł** |

## Plan prac (kamienie milowe)

- [ ] **Etap 1 – Prototyp programowy:** aplikacja React z grą sterowaną klawiaturą ⏫ 📅 2026-10-27
- [ ] **Etap 2 – Jeden czujnik:** domowy przełącznik foliowy + Raspberry Pi wykrywa nacisk 📅 2026-11-03
- [ ] **Etap 3 – Komunikacja:** backend na Pi wysyła zdarzenia do Reacta przez WebSocket 📅 2026-11-10
- [ ] **Etap 4 – Mała mata 2 × 2:** test całego łańcucha na 4 polach 📅 2026-11-17
- [ ] **Etap 5 – Pełna mata 4 × 4** z ekspanderem MCP23017 📅 2026-12-01
- [ ] **Etap 6 – Dopracowanie:** tryb kiosku, LED, paczki dźwięków, testy z graczami 📅 2026-12-15

### Wszystkie otwarte zadania projektu
```tasks
not done
path includes Dźwiękowe memory
sort by due
```

## Ryzyka i pytania
- Czy czujniki foliowe przetrwają skakanie? → zrobić test wytrzymałości na prototypie.
- Fałszywe odczyty (ktoś stoi na dwóch polach) → liczy się tylko *nowe* naciśnięcie.
- Opóźnienie dźwięku → testować na docelowym sprzęcie; Howler.js z wcześniej załadowanymi plikami.
- Prowadzenie przewodów w macie → płaskie przewody taśmowe, wspólna masa dla wszystkich pól.
