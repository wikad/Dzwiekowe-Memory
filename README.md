# D-wi-kowe-Memory

Projekt grupowy **Dźwiękowe memory** dla dzieci w wieku przedszkolnym: duża mata (jak do Twistera) z czujnikami w polach. Dziecko staje na polu, słyszy dźwięk i szuka drugiego pola z takim samym dźwiękiem. Sprzęt to Raspberry Pi, a aplikacja jest napisana w React.

To repozytorium jest **sejfem Obsidiana**, w którym zarządzamy projektem: notatki, zadania i tablica kanban.

| Plik | Co zawiera |
|---|---|
| `Wstęp do obsidian.md` | poradnik: podstawy Obsidiana, Git, Tasks i Kanban |
| `Projekt Dźwiękowe memory.md` | opis projektu, sprzęt, architektura, plan prac |
| `Kanban - Dźwiękowe memory.md` | tablica zadań zespołu |

---

## Instalacja

### 1. Zainstaluj Git

- **Windows:** pobierz z https://git-scm.com/download/win i zainstaluj z domyślnymi ustawieniami.
- **macOS:** w terminalu wpisz `git --version`. Jeśli Gita nie ma, system zaproponuje instalację.
- **Linux:** `sudo apt install git` (Debian/Ubuntu).

Przy pierwszym użyciu ustaw swoje dane (w terminalu):

```bash
git config --global user.name "Imię Nazwisko"
git config --global user.email "twoj@email.com"
```

### 2. Zainstaluj Obsidiana

Pobierz instalator ze strony https://obsidian.md/download (Windows, macOS, Linux, Android, iOS) i zainstaluj. Obsidian jest darmowy.

### 3. Sklonuj repozytorium

W terminalu, w folderze, w którym chcesz trzymać projekt (np. na Pulpicie):

```bash
git clone https://github.com/wikad/D-wi-kowe-Memory.git
```

Jeśli nie masz uprawnień do repozytorium, poproś właściciela o dodanie Cię jako *collaborator* (GitHub → Settings → Collaborators).

### 4. Otwórz folder jako sejf

1. Uruchom Obsidiana.
2. Wybierz **Open folder as vault** („Otwórz folder jako sejf”).
3. Wskaż sklonowany folder `D-wi-kowe-Memory`.
4. Obsidian zapyta, czy ufasz autorowi sejfu. Kliknij **Trust author and enable plugins**.

### 5. Wtyczki

Wtyczki są już w repozytorium (folder `.obsidian/plugins`), więc **nie trzeba ich instalować ręcznie**. Po zaufaniu sejfowi włączą się same:

| Wtyczka | Do czego |
|---|---|
| **Git** (`obsidian-git`) | synchronizacja notatek z GitHubem |
| **Tasks** (`obsidian-tasks-plugin`) | zadania z terminami, priorytetami i zapytaniami |
| **Kanban** (`obsidian-kanban`) | tablica kanban w pliku Markdown |

Jeśli wtyczki nie działają:

1. Otwórz **Ustawienia** (ikona koła zębatego, lewy dolny róg) → **Community plugins**.
2. Kliknij **Turn on community plugins**, jeśli tryb ograniczony (*Restricted mode*) jest włączony.
3. Upewnij się, że przełączniki przy **Git**, **Tasks** i **Kanban** są włączone.
4. Jeśli którejś wtyczki brakuje, kliknij **Browse**, wyszukaj ją po nazwie, a potem kliknij **Install** i **Enable**.

### 6. Logowanie do GitHuba

Przy pierwszej synchronizacji (`Ctrl + P` → **Git: Commit-and-sync**) na Windowsie otworzy się okno logowania do GitHuba (Git Credential Manager). Zaloguj się przez przeglądarkę.

---

## Praca na co dzień

1. **Przed pracą:** `Ctrl + P` → **Git: Pull**, żeby pobrać zmiany reszty zespołu.
2. Edytuj notatki i przesuwaj karty na tablicy kanban.
3. **Po pracy:** `Ctrl + P` → **Git: Commit-and-sync**, żeby wysłać swoje zmiany.

Wskazówki:
- Możesz włączyć automatyczną synchronizację: **Ustawienia → Git → Auto commit-and-sync interval** (np. `10` minut) oraz **Pull on startup**.
- Synchronizuj często, wtedy rzadziej powstają konflikty.
- Więcej o Obsidianie i wtyczkach znajdziesz w notatce **Wstęp do obsidian**.
