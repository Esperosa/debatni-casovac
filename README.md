# Debatní časovač v3.1

![Version](https://img.shields.io/badge/version-3.1-0b8f3d)
![Type](https://img.shields.io/badge/app-single--file%20HTML-1f6feb)
![Languages](https://img.shields.io/badge/language-CZ%20%2F%20EN-0a7ea4)
![License](https://img.shields.io/badge/license-Apache--2.0-111111)

Jednosouborová webová aplikace pro řízení školních debat, turnajových kol a tréninku argumentace.

Projekt je navržený tak, aby fungoval:

- offline přímo v prohlížeči,
- bez backendu,
- bez instalace,
- bez závislosti na serveru.

## Obsah

1. [Co aplikace obsahuje](#co-aplikace-obsahuje)
2. [Tok debaty](#tok-debaty)
3. [Obrazovky a funkcionality](#obrazovky-a-funkcionality)
4. [Ovládání a klávesové zkratky](#ovládání-a-klávesové-zkratky)
5. [Režimy debaty a bodování](#režimy-debaty-a-bodování)
6. [Témata, filtry a náhodné losování](#témata-filtry-a-náhodné-losování)
7. [Import debatérů ze souboru](#import-debatérů-ze-souboru)
8. [Jazyková lokalizace CZ/EN](#jazyková-lokalizace-czen)
9. [Časování, zvuky, hudba](#časování-zvuky-hudba)
10. [Ukládání dat](#ukládání-dat)
11. [Interaktivní prvky (ID map)](#interaktivní-prvky-id-map)
12. [Struktura repozitáře](#struktura-repozitáře)
13. [Autorství a licence](#autorství-a-licence)

## Co aplikace obsahuje

| Oblast | Co přesně umí |
|---|---|
| Kompletní běh debaty | Setup → Intro → Vysvětlení tématu → Příprava → Kolo → Pauza → Výsledky |
| Režimy | 1v1 páry i skupinová varianta s hlasováním vítězů |
| Knihovna témat | Sekce, obtížnost (1–5), fulltext, random volba témat po kolech |
| Edukační vrstva | 6slidový naučný režim + samostatný modal „Pravidla akademické debaty“ |
| Import osob | XLSX/XLS/CSV/TSV/TXT/PDF + kontrolní modal s editací |
| Výsledky | Přehled kol, export do schránky, ve skupinách i tiebreak ranking a ocenění |
| UX nástroje | Walkthrough (4 tour), fullscreen, validace vstupů, motivy UI |
| Lokalizace | Přepínač jazyka CZ/EN včetně runtime textů a dynamických částí |

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

## Obrazovky a funkcionality

| Obrazovka | Účel | Klíčové prvky |
|---|---|---|
| Setup | Kompletní příprava debaty | téma, knihovna, debatéři, režim, časy, audio, import, presety |
| Tutorial | Naučit základy argumentace | 6 kroků: pravidla, SEXI, vyvracení, chyby, rekapitulace |
| Intro | Krátké uvedení před debatou | téma, strany, odpočet, struktura kola |
| Topic Explain | Kontext tématu pro obě strany | blurb, argument PRO, argument PROTI |
| Run | Samotná debata | fáze, časovač, páry/skupiny, hlasování, pauza, restart |
| Done | Vyhodnocení | výsledky, přehled kol, export, ranking, ocenění |

## Ovládání a klávesové zkratky

| Kontext | Klávesa | Akce |
|---|---|---|
| Intro / Run | Space | Pauza / pokračování |
| Run | N | Další fáze |
| Intro / Run | R | Otevřít potvrzení restartu |
| Globálně | Escape | Zavřít modal / ukončit průvodce |
| Přepínač motivu | Enter / Space | Přepnout motiv |
| Přepínač motivu | Šipky | Posun mezi motivy |
| Walkthrough | ArrowLeft / ArrowRight | Předchozí / další krok |

## Režimy debaty a bodování

### Režim dvojic (1v1)

- Round-robin generování kol.
- Při lichém počtu debatérů automatický bye.
- Vítěz duelu se volí klikem na stranu PRO/PROTI.

### Režim skupin

- Každé kolo nové rozdělení skupin.
- Podpora automatické i vlastní velikosti skupiny.
- Hlasování vítěze každého skupinového souboje.
- Finální pořadí:
  1. výhry,
  2. Buchholz (síla soupeřů),
  3. progressive score.

### Ocenění (skupiny)

Výsledkový panel umí přidělovat tematická ocenění podle průběhu turnaje (např. neporažený hráč, comeback, série výher, atd.).

## Témata, filtry a náhodné losování

- Knihovna obsahuje tematické sekce s věkovým doporučením a štítky obtížnosti.
- Fulltext vyhledává v názvu, popisu i argumentačních nápovědách.
- Přepínač „Náhodné téma každé kolo“ přidělí každému kolu jiné téma.
- Ruční téma i vybrané téma z knihovny lze kdykoli upravit.

## Import debatérů ze souboru

### Podporované formáty

- Excel: `.xlsx`, `.xls`
- Tabulkový text: `.csv`, `.tsv`
- Text: `.txt`
- PDF: `.pdf`

### Pipeline importu

1. Načtení souboru (drag and drop / výběr souboru).
2. Parsování podle typu (text / SheetJS / PDF.js).
3. Normalizace polí `jméno / příjmení / třída`.
4. Kontrolní modal s tabulkou a inline editací.
5. Aplikace do seznamu (nahradit / přidat / odebrat neúplné).
6. Volitelná synchronizace do presetů tříd.

### Co umí kontrolní modal

- Filtr: vše / neúplné / konkrétní třída.
- Hromadný výběr checkboxem.
- Inline editace jména, příjmení i třídy.
- Stav řádku: `OK`, `chybí`, `bez jména`, `bez příjmení`, `prázdné`.

## Jazyková lokalizace CZ/EN

- Přepínač jazyka je přímo v hlavičce (`CZ` / `EN`).
- Volba se ukládá do `localStorage` (`debateTimerLang`).
- Lokalizace pokrývá:
  - statické UI texty,
  - dynamické texty generované během běhu,
  - výsledkový panel,
  - export textových výsledků.
- Jazyk lze změnit i během běžící debaty bez reloadu stránky.

## Časování, zvuky, hudba

- Odpočty a fáze: příprava, kolo, pauza mezi koly.
- Kritické zvukové upozornění: `10 / 5 / 3 / 2 / 1` sekund.
- Zvuky: start kola, konec kola, skip fáze, vstup do hlasování, finální akord.
- Hudba v pauzách má samostatnou hlasitost oddělenou od signálů.

## Ukládání dat

| Klíč | Co ukládá |
|---|---|
| `debateTimerV2` | setup, časy, režim, audio, filtry, random volby, tutorial, presety |
| `debateTimerTheme` | aktivní motiv |
| `debateTimerLang` | aktivní jazyk (`cs` / `en`) |
| `wt_completed_tours` | dokončené walkthrough průchody |

## Interaktivní prvky (ID map)

<details>
<summary><strong>Rozbalit kompletní seznam</strong></summary>

### Setup

- `btnWalkthrough`
- `themeTrack`
- `langToggle`
- `langCs`
- `langEn`
- `btnRandomTopic`
- `btnClearTopic`
- `swRandomTopic`
- `topicTextarea`
- `playersTextarea`
- `topicCategory`
- `topicSearch`
- `btnDedupe`
- `btnClearPlayers`
- `modePairs`
- `modeGroups`
- `groupSizeInput`
- `groupSafeOff`
- `groupRoundsInput`
- `initTime`
- `roundTimeInput`
- `pauseTimeInput`
- `swTutorial`
- `swSound`
- `swMusic`
- `volSignal`
- `prevSignal`
- `volMusic`
- `prevMusic`
- `btnStart`
- `btnPravidla`
- `btnFullscreenHint`
- `presetSelect`
- `btnPresetAll`
- `btnPresetNone`
- `btnPresetReplace`
- `btnPresetAppend`
- `importDropZone`
- `importFileInput`

### Tutorial / Intro / Explain / Run

- `btnTutPrev`
- `btnTutNext`
- `btnSkipIntro`
- `btnBackToSetup1`
- `btnSkipExplain`
- `btnPause`
- `btnNext`
- `btnFullscreen`
- `btnRestart`
- `voteConfirmBtn`
- `btnConfirmRestart`
- `btnCancelRestart`
- `btnPravidlaClose`

### Import modal

- `importChkAll`
- `importBtnApply`
- `importBtnAppend`
- `importBtnDelInvalid`
- `importBtnCancel`

### Walkthrough

- `wtClose`
- `wtBack`
- `wtNext`
- `wtSkip`
- `wtPickerClose`
- `wtPickerReset`

</details>

## Struktura repozitáře

- `debatni-casovac-v3.1.html` — kompletní aplikace (HTML/CSS/JS + data témat)
- `README.md` — dokumentace projektu
- `LICENSE` — Apache License 2.0
- `NOTICE` — povinné atribuční informace

## Autorství a licence

Autor projektu: **Jiří Pelikán**.

Projekt je licencován pod **Apache License 2.0**. To umožňuje použití, úpravy i redistribuci při dodržení podmínek licence.

Pro zachování původu projektu je součástí repozitáře soubor `NOTICE`, který je nutné při redistribuci zachovat dle podmínek Apache-2.0.
