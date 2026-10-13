---
tags: [obsidian, poradnik]
---

# Wstęp do Obsidiana

## Czym jest Obsidian?

Obsidian to edytor notatek oparty na zwykłych plikach **Markdown** (`.md`), które leżą w folderze na Twoim dysku — ten folder to **sejf** (*vault*). Nic nie jest zamknięte w chmurze ani w bazie danych: notatki możesz otworzyć dowolnym edytorem, wersjonować Gitem albo skopiować na pendrive.

Największa siła Obsidiana to **linkowanie notatek** — z pojedynczych plików robi się sieć wiedzy, którą widać na grafie.

## Podstawy, które warto znać

| Funkcja | Jak użyć |
|---|---|
| Link do notatki | `[[Projekt Dźwiękowe memory]]` → [[Projekt Dźwiękowe memory]] |
| Link do nagłówka | `[[Projekt Dźwiękowe memory#Sprzęt]]` |
| Link z inną nazwą | `[[Projekt Dźwiękowe memory\|mój projekt]]` |
| Osadzenie notatki | `![[nazwa notatki]]` (wstawia jej treść) |
| Tag | `#pomysł`, `#raspberry` — lista w panelu tagów |
| Właściwości | blok `---` na samej górze pliku (tak jak w tej notatce) |
| Paleta poleceń | `Ctrl + P` — tu znajdziesz **każdą** funkcję, także z wtyczek |
| Szybkie otwieranie | `Ctrl + O` — wyszukaj notatkę po nazwie |
| Szukanie w treści | `Ctrl + Shift + F` |
| Podgląd / edycja | `Ctrl + E` |
| Graf | `Ctrl + G` lub ikona w lewym pasku |

### Włączone wtyczki wbudowane (core)
- **Graf** i **Linki zwrotne** (*backlinks*) — kto linkuje do bieżącej notatki.
- **Canvas** — tablica do rysowania map myśli z notatek, obrazków i kart.
- **Notatki dzienne** (*daily notes*) — jeden plik na dzień, np. dziennik postępów projektu.
- **Szablony** — wstawianie gotowych struktur notatek.
- **Bases** — widoki tabelaryczne notatek na podstawie ich właściwości.
- **Konspekt**, **Zakładki**, **Licznik słów**, **Odzyskiwanie plików** (lokalne kopie zmian).

---

## Zainstalowane wtyczki społecznościowe

W tym sejfie są trzy wtyczki: **Git**, **Tasks** i **Kanban**.

### 1. Git (`obsidian-git`)

Synchronizuje sejf z repozytorium Git (np. GitHub) — masz pełną historię zmian i kopię zapasową.

**Pierwsza konfiguracja** (sejf jeszcze *nie jest* repozytorium):
1. Zainstaluj Gita na komputerze: https://git-scm.com.
2. W Obsidianie: `Ctrl + P` → **Git: Initialize a new repo**.
3. Utwórz puste repozytorium na GitHubie (najlepiej **prywatne**).
4. `Ctrl + P` → **Git: Edit remotes** → nazwa `origin`, adres repozytorium.
5. Pierwsze wysłanie: `Ctrl + P` → **Git: Commit-and-sync**.

Alternatywnie z terminala w folderze sejfu:
```bash
git init
git remote add origin https://github.com/TWOJ_LOGIN/memory-vault.git
git add .
git commit -m "Pierwszy commit"
git push -u origin main
```

**Codzienne użycie** (wszystko przez `Ctrl + P` → wpisz „Git”):
- **Commit-and-sync** — zapisuje zmiany, pobiera cudze i wysyła swoje (najczęściej używane).
- **Pull** — pobierz zmiany z innego urządzenia.
- **Open source control view** — panel ze zmienionymi plikami (jak w VS Code).
- **Open history view** — historia commitów.

**Automatyzacja** — Ustawienia → Git:
- *Auto commit-and-sync interval* — np. `10` minut, sejf sam się zapisuje.
- *Pull on startup* — pobiera zmiany przy uruchomieniu Obsidiana.

> [!tip] Dobra praktyka
> Dodaj plik `.gitignore` z linią `.obsidian/workspace.json` — ten plik zmienia się przy każdym kliknięciu i robi niepotrzebne konflikty.

### 2. Tasks (`obsidian-tasks-plugin`)

Zamienia zwykłe checkboxy w zadania z terminami, priorytetami i powtarzaniem — a potem pozwala je **zbierać z całego sejfu** w jednym miejscu.

**Zadanie** to linia zaczynająca się od `- [ ]`. Najwygodniej tworzyć je przez `Ctrl + P` → **Tasks: Create or edit task** (okienko z polami do wypełnienia).

| Znacznik | Znaczenie | Przykład |
|---|---|---|
| `📅` | termin (*due*) | `📅 2026-10-20` |
| `⏳` | zaplanowane na (*scheduled*) | `⏳ 2026-10-18` |
| `🛫` | data startu | `🛫 2026-10-15` |
| `✅` | data wykonania (dodaje się sama) | `✅ 2026-10-14` |
| `🔺 ⏫ 🔼 🔽 ⏬` | priorytet: najwyższy → najniższy | `⏫` |
| `🔁` | powtarzanie | `🔁 every week` |

Przykład:
- [ ] Zamówić czujniki nacisku ⏫ 📅 2026-10-20
- [ ] Przejrzeć postępy projektu 🔁 every week on Sunday 📅 2026-10-18
- [x] Opisać pomysł na projekt ✅ 2026-10-13

**Zapytania** — blok kodu `tasks` wyświetla zadania z wielu notatek. Np. wszystkie niezrobione zadania z sejfu, pogrupowane po pliku:

```tasks
not done
sort by priority
sort by due
group by filename
```

Inne przydatne filtry: `due before tomorrow`, `due this week`, `path includes Projekt`, `priority is high`, `tags include #raspberry`.

### 3. Kanban (`obsidian-kanban`)

Tablica kanban (jak Trello), która jest zwykłym plikiem Markdown. Każda **kolumna** to nagłówek `##`, każda **karta** to zadanie `- [ ]`.

**Jak działa kanban:** praca płynie od lewej do prawej — *Pomysły → Do zrobienia → W trakcie → Testy → Zrobione*. Zasada: **ogranicz liczbę rzeczy „W trakcie”** (np. max 3) — lepiej kończyć niż zaczynać.

**Obsługa:**
- Nowa tablica: `Ctrl + P` → **Kanban: Create new board** (albo prawy klik na folder → *New kanban board*).
- Karty przeciągasz myszką między kolumnami.
- W karcie możesz pisać linki `[[notatka]]`, tagi `#tag` i daty `@{2026-10-20}`.
- Przełączenie na surowy Markdown: menu `⋯` w prawym górnym rogu → **Open as markdown** (i z powrotem: **Open as kanban board**).
- Ustawienia tablicy (ikona koła zębatego): np. automatyczne odhaczanie kart w kolumnie „Zrobione”, limit kart w kolumnie.

> [!example] Przykład
> Gotowa tablica dla projektu: [[Kanban - Dźwiękowe memory]]

**Tasks + Kanban razem:** karty kanbana to też zadania `- [ ]`, więc jeśli dopiszesz w nich `📅 data`, pojawią się w zapytaniach Tasks z innych notatek.

---

## Proponowana struktura sejfu

```
Memory/
├── Wstęp do obsidian.md          ← ta notatka
├── Projekt Dźwiękowe memory.md   ← opis projektu
├── Kanban - Dźwiękowe memory.md  ← tablica zadań
├── Dziennik/                     ← notatki dzienne (postępy, problemy)
└── Szablony/                     ← szablony notatek
```

## Moje notatki
- [[Projekt Dźwiękowe memory]]
- [[Kanban - Dźwiękowe memory]]
