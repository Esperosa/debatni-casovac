<h1 align="center">Debatní časovač v3.1</h1>

<p align="center">
  Jednosouborová webová aplikace pro školní debaty, argumentační trénink a turnajové vedení kol.
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/version-3.1-0b8f3d" />
  <img alt="Type" src="https://img.shields.io/badge/app-single--file%20HTML-1f6feb" />
  <img alt="Languages" src="https://img.shields.io/badge/language-CZ%20%2F%20EN-0a7ea4" />
  <img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-111111" />
</p>

## Proč je tenhle projekt praktický

- Funguje offline přímo v prohlížeči.
- Nepotřebuje backend, databázi ani instalaci.
- Vše je v jednom souboru HTML.
- Přepínání CZ/EN je okamžité a deterministické.
- Obsahuje výuku argumentace, průvodce aplikací i turnajové režimy.

> [!TIP]
> Aplikaci stačí otevřít jako běžný HTML soubor. To je celé.

## Rychlý start

1. Otevři soubor `debatni-casovac-v3.1.html` v prohlížeči.
2. Vyplň téma, debatéry a režim.
3. Klikni na Start debaty.

## Co všechno aplikace obsahuje

| Oblast | Co dostaneš |
|---|---|
| Kompletní flow | Setup → Intro → Vysvětlení tématu → Příprava → Kolo → Pauza → Výsledky |
| Režimy | 1v1 páry i skupinová varianta s hlasováním vítězů |
| Témata | Ruční zadání, knihovna témat, filtry, fulltext, random témata po kolech |
| Výuka | Naučný režim (prezentace) + modal pravidel akademické debaty |
| Průvodci | App guide picker + 4 specializované walkthrough tour |
| Import | XLSX/XLS/CSV/TSV/TXT/PDF + validační modal s editací |
| Zvuk a hudba | Signály, start/end cue, hudba mezi koly, samostatné hlasitosti + preview |
| Výsledky | Přehled kol, export do schránky, ranking, tiebreak a ocenění |
| UX | Fullscreen, klávesové zkratky, motivy, validace vstupů |
| Lokalizace | CZ/EN napříč setupem, během debaty, výsledky, tutoriály i průvodci |

## Tok debaty

```mermaid
flowchart LR
  A[Nastavení] -->|Start| B{Naučný režim?}
  B -->|Ano| C[Tutorial 6 slidů]
  B -->|Ne| D{Téma vyplněno / random mód}
  C --> D
  D -->|Ano| E[Intro]
  D -->|Ne| F[Příprava]
  E --> G[Vysvětlení tématu]
  G --> F
  F --> H[Kolo]
  H --> I{Skupinový režim?}
  I -->|Ano| J[Hlasování vítěze]
  J --> K{Poslední kolo?}
  I -->|Ne| K
  K -->|Ne| L[Pauza]
  L --> H
  K -->|Ano| M[Výsledky + export]
```

## Obrazovky

| Obrazovka | Co řeší |
|---|---|
| Setup | Kompletní příprava debaty (téma, lidi, režim, časování, audio) |
| Tutorial | Naučný režim: argumentace krok za krokem |
| Intro | Úvod před debatou: téma, strany, struktura, odpočet |
| Topic Explain | Kontext tématu + argument PRO/CON |
| Run | Hlavní běh debaty s fázemi, časovačem a hlasováním |
| Done | Finální výsledky, ranking, ocenění, export |

## Ovládání během debaty

| Kontext | Klávesa | Akce |
|---|---|---|
| Intro / Run | Space | Pauza / pokračování |
| Run | N | Další fáze |
| Intro / Run | R | Potvrzení restartu |
| Globálně | Escape | Zavřít modal / ukončit průvodce |
| Walkthrough | ArrowLeft / ArrowRight | Předchozí / další krok |

Runtime hint se překládá jako celá věta:

- CZ: Ovládání během běhu: Mezerník pauza/pokračovat, N další fáze, R restart.
- EN: Controls during runtime: Space pause/resume, N next phase, R restart.

## Naučný režim (prezentace)

Naučný režim je volitelný onboarding před debatou. Má 6 slidů:

1. Co je debata?
2. Pravidla akademické debaty
3. Model argumentace SEXI
4. Jak vyvracet soupeře
5. Nejčastější argumentační chyby
6. Shrnutí a plynulý start debaty

Prezentační obsah má pevné CZ/EN mapy a při přepnutí jazyka se překreslí okamžitě.

## App guide (walkthrough)

Tlačítko Průvodce otevře picker s tour moduly:

- App guide
- Choose the part you want to explore:
- Recommended
- Reset tours

### Dostupné tour

| Tour | Kroky | Co pokrývá |
|---|---:|---|
| Quick start | 5 | téma, debatéři, start, základní flow |
| Topics and library | 6 | ruční téma, filtry, knihovna, random témata |
| Debaters and import | 6 | seznam, presety tříd, import, validace |
| Mode and settings | 8 | motiv, režim, časování, signály, hudba, learning mode |

Každá tour má progress, zvýraznění cílového prvku, klávesové ovládání a možnost resetu.

## Režimy debaty a bodování

### Režim párů (1v1)

- Round-robin párování.
- Automatické BYE při lichém počtu debatérů.
- Ruční volba vítěze každého duelu.

### Režim skupin

- Dynamické skupiny po kolech.
- Auto velikost i vlastní velikost skupiny.
- Hlasování vítěze v každé skupině.
- Ranking: výhry → Buchholz → progressive score.

### Ocenění

Výsledkovka umí tematická ocenění podle průběhu turnaje (streak, comeback, unbeaten a další).

## Témata, knihovna a random režim

- Knihovna je členěná do sekcí.
- Témata mají metadata, obtížnost a argumentační hinty.
- Fulltext hledá v názvu, popisu i argumentech.
- Random režim umí losovat nové téma každé kolo.

## Import debatérů

### Podporované formáty

- `.xlsx`, `.xls`
- `.csv`, `.tsv`
- `.txt`
- `.pdf`

### Co umí validační modal

- Filtry vše / neúplné / třída.
- Hromadný výběr řádků.
- Inline editace jméno / příjmení / třída.
- Stavy řádku: OK, chybí, bez jména, bez příjmení, prázdné.

## Zvuky, signály, hudba

| Funkce | Popis |
|---|---|
| Signály | Upozornění na časové milníky a přechody fází |
| Alert times | 10 / 5 / 3 / 2 / 1 sekund před koncem |
| Start/End cue | Zvuky začátku a konce kola |
| Skip cue | Zvuk při ručním přeskočení fáze |
| Hlasování cue | Zvuk při vstupu do hlasování |
| Finální akord | Závěr debaty |
| Hudba | Běží v přípravě a mezi koly |
| Hlasitosti | Signály a hudba mají oddělené ovládání |
| Preview | Tlačítka testu signálu i hudby přímo v setupu |

## Lokalizace CZ/EN

- Přepínač jazyka je v hlavičce (CZ / EN).
- Volba jazyka se ukládá do localStorage (`debateTimerLang`).
- Lokalizace je lokální, deterministická, bez externího překládacího API.

Pokrytí lokalizace:

- Setup UI
- Runtime fáze a status texty
- Intro a explain obrazovky
- Tutorial prezentace (6 slidů)
- Walkthrough picker + kroky + smart texty
- Výsledkový panel a export
- Texty témat včetně blurb/PRO/CON hintů

## Ukládání dat

| Klíč | Co ukládá |
|---|---|
| `debateTimerV2` | setup, časy, režim, audio, filtry, random volby, tutorial, presety |
| `debateTimerTheme` | aktivní motiv |
| `debateTimerLang` | aktivní jazyk (`cs` / `en`) |
| `wt_completed_tours` | dokončené průvodce |

## One-file architektura

Aplikace je plně v jednom souboru `debatni-casovac-v3.1.html`.

| Modul | Role |
|---|---|
| DATA: PRESETS | výchozí seznamy debatérů |
| DATA: TOPIC_LIBRARY | knihovna témat a metadata |
| I18N | CZ/EN engine a statické mapy textů |
| FILE IMPORT ENGINE | import a validace dat ze souboru |
| AUDIO | signály, hudba, preview, fade |
| MATCHING / SCORING | párování kol, ranking, tiebreak |
| RENDER | intro / explain / run / done |
| WALKTHROUGH | app guide, tour kroky, progress, reset |

## Struktura repozitáře

- `debatni-casovac-v3.1.html` - celá aplikace
- `README.md` - dokumentace
- `LICENSE` - Apache License 2.0
- `NOTICE` - atribuční informace dle licence

## Autor a licence

Autor projektu: Jiří Pelikán.

Projekt je licencovaný pod Apache License 2.0.
