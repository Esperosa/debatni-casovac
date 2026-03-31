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
5. [Naučný režim (prezentace)](#naučný-režim-prezentace)
6. [App guide (walkthrough)](#app-guide-walkthrough)
7. [Režimy debaty a bodování](#režimy-debaty-a-bodování)
8. [Témata, filtry a náhodné losování](#témata-filtry-a-náhodné-losování)
9. [Import debatérů ze souboru](#import-debatérů-ze-souboru)
10. [Jazyková lokalizace CZ/EN](#jazyková-lokalizace-czen)
11. [Verifikace lokalizace](#verifikace-lokalizace)
12. [Časování, zvuky, hudba](#časování-zvuky-hudba)
13. [Ukládání dat](#ukládání-dat)
14. [Interní architektura (one-file)](#interní-architektura-one-file)
15. [Interaktivní prvky (ID map)](#interaktivní-prvky-id-map)
16. [Struktura repozitáře](#struktura-repozitáře)
17. [Autorství a licence](#autorství-a-licence)

## Co aplikace obsahuje

| Oblast | Co přesně umí |
|---|---|
| Kompletní běh debaty | Setup → Intro → Vysvětlení tématu → Příprava → Kolo → Pauza → Výsledky |
| Režimy | 1v1 páry i skupinová varianta s hlasováním vítězů |
| Knihovna témat | Sekce, obtížnost (1–5), fulltext, random volba témat po kolech |
| Edukační vrstva | 6slidový naučný režim + samostatný modal „Pravidla akademické debaty“ |
| Průvodci | App guide picker + 4 specializované walkthrough tour s progress a resetem |
| Import osob | XLSX/XLS/CSV/TSV/TXT/PDF + kontrolní modal s editací |
| Výsledky | Přehled kol, export do schránky, ve skupinách i tiebreak ranking a ocenění |
| Audio | Signalizační pípnutí, start/end zvuky, hudba v pauzách, oddělené hlasitosti + preview |
| UX nástroje | Fullscreen, validace vstupů, motivy UI, klávesové ovládání |
| Lokalizace | Přepínač jazyka CZ/EN s okamžitým, deterministickým přepnutím (exact/regex/fragment + statické EN packy témat i tutorial slidů) |

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

Runtime nápověda v aplikaci se lokalizuje jako celá věta:

- CZ: Ovládání během běhu: Mezerník pauza/pokračovat, N další fáze, R restart.
- EN: Controls during runtime: Space pause/resume, N next phase, R restart.

## Naučný režim (prezentace)

Naučný režim je volitelný 6slidový pre-debate onboarding určený pro začátečníky. Zapíná se přepínačem `swTutorial`.

| Slide | Obsah |
|---|---|
| 1. Co je debata? | role PRO/PROTI, jak funguje přesvědčování, co je debata vs. hádka |
| 2. Pravidla | slušnost, nepřerušování, držení tématu, argument podložený důvodem/příkladem |
| 3. Argumentace SEXI | Statement, Explanation, eXample, Impact + praktický příklad |
| 4. Vyvracení soupeře | postup „Soupeř říká... / Ale... protože... / Lepší je...“ |
| 5. Čemu se vyhnout | osobní útok, strawman, falešné dilema |
| 6. Shrnutí a start | rychlá rekapitulace a přechod do debaty |

Implementace lokalizace prezentace:

- český originál je v HTML slidech,
- anglická verze je staticky definovaná v `TUTORIAL_EN_SLIDES`,
- při přepnutí jazyka se obsah slide okamžitě překreslí bez reloadu.

## App guide (walkthrough)

Tlačítko Průvodce (`btnWalkthrough`) otevírá picker, kde si uživatel vybere část aplikace k procvičení.

### Picker texty a stavy

- App guide
- Choose the part you want to explore:
- Recommended
- Reset tours
- Done / Hotovo badge
- steps / kroků badge

### 4 dostupné tour

| Tour | Kroky | Co pokrývá |
|---|---:|---|
| Quick start | 5 | téma, debatéři, start, základní flow |
| Topics and library | 6 | ruční téma, random, kategorie, fulltext, výběr z knihovny |
| Debaters and import | 6 | seznam, dedupe, presety tříd, import souboru, validační panel |
| Mode and settings | 8 | motiv, režim, časy, signály, hudba, learning mode |

Každá tour má:

- krokový progress,
- `Esc` pro ukončení,
- zvýraznění cílového prvku,
- kontextové try-it kroky,
- ukládání dokončení do `wt_completed_tours`.

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
- Překlad je plně lokální a statický: bez runtime volání externích překladových API.
- Lokalizace pokrývá:
  - statické UI texty,
  - dynamické texty generované během běhu,
  - výsledkový panel,
  - export textových výsledků,
  - tutorial prezentaci (6 slidů),
  - walkthrough průvodce (picker + kroky + smart texty),
  - fixní runtime texty (např. hint ovládání během běhu, validační řádky, intro struktura kol).
- Překlad je navržený nad celými významovými bloky (exact/regex/fragment), ne jako word-by-word převod.
- Nad základní mapou běží i statické EN packy:
  - `I18N_TOPIC_STATIC_EN` pro témata (názvy, blurby, argumenty, tagy),
  - `TUTORIAL_EN_SLIDES` pro celý obsah 6 slidů.
- Přepnutí jazyka okamžitě přerenderuje aktivní obrazovky (topic list, tutorial, run phase, done, otevřený walkthrough picker/krok), takže texty „nedoskakují“ později.
- Jazyk lze změnit i během běžící debaty bez reloadu stránky.

## Verifikace lokalizace

Lokalizace je kontrolovaná dvěma auditními průchody nad zdrojovým kódem:

- **Static text audit**: textové uzly v HTML (bez `script/style`) se porovnají proti překladové vrstvě.
- **Runtime text audit**: řetězce používané v `textContent`, `innerHTML`, `alert`, `toast` a import workflow se porovnají proti překladové vrstvě.

Aktuální stav:

- Statické texty: pokryté přes exact/regex/fragment překladovou vrstvu.
- Témata: pokrytá přes statický EN topic pack přímo v aplikaci.
- Tutorial prezentace: pokrytá přes dedikovaný EN slide pack (`TUTORIAL_EN_SLIDES`).
- Runtime texty: pokryté synchronně při renderu + i18n observer pro nově vložené uzly.

Poznámka: témata, tutorial i průvodce se překládají deterministicky ze statických map v aplikaci, takže přepnutí jazyka je okamžité a bez doskakování textu.

## Časování, zvuky, hudba

- Odpočty a fáze: příprava, kolo, pauza mezi koly.
- Kritické zvukové upozornění: `10 / 5 / 3 / 2 / 1` sekund.
- Signalizační audio události:
  - odpočet (`ALERT_TIMES`),
  - start kola,
  - konec kola,
  - skip fáze,
  - vstup do hlasování,
  - finální akord.
- Hudba v pauzách:
  - běží v přípravě a mezi koly,
  - má vlastní gain a fade-in/fade-out,
  - hlasitost je oddělená od signálů.
- Setup obsahuje náhledová tlačítka:
  - `prevSignal` pro ukázku signálu,
  - `prevMusic` pro ukázku hudby.
- Přepínače:
  - `swSound` pro signály,
  - `swMusic` pro hudbu,
  - posuvníky `volSignal` a `volMusic` pro jemné doladění.

## Ukládání dat

| Klíč | Co ukládá |
|---|---|
| `debateTimerV2` | setup, časy, režim, audio, filtry, random volby, tutorial, presety |
| `debateTimerTheme` | aktivní motiv |
| `debateTimerLang` | aktivní jazyk (`cs` / `en`) |
| `wt_completed_tours` | dokončené walkthrough průchody |

## Interní architektura (one-file)

Vše je v jednom souboru `debatni-casovac-v3.1.html`, ale kód je modulárně rozdělený komentářovými bloky.

| Modul | Role |
|---|---|
| `DATA: PRESETS` | výchozí seznamy debatérů (9.A/9.B) |
| `DATA: TOPIC_LIBRARY` | knihovna témat včetně metadata sekcí, obtížnosti, tagů a argumentačních nápověd |
| `I18N (CZ / EN)` | jazykový engine (exact/regex/fragment), statický EN topic pack, statický EN tutorial pack, fixní lokalizované runtime texty, observer pro dynamický obsah |
| `FILE IMPORT ENGINE` | import z XLSX/XLS/CSV/TSV/TXT/PDF + normalizace + kontrolní modal |
| `UTIL` | parse/normalizace času, sanitizace vstupů, pomocné funkce |
| `AUDIO` | signalizační zvuky, preview, hudba v pauzách, fade-in/fade-out |
| `TOPIC UI` | sekce témat, filtry, fulltext, random režim po kolech |
| `MATCHING / SCORING` | párování kol, skupinové souboje, winners, tiebreak (Buchholz/progressive) |
| `RENDER` | vykreslení Intro/Explain/Run/Done, hlasování, export výsledků |
| `WALKTHROUGH` | 4 průvodce aplikací, progress, reset dokončených kroků |

### Algoritmy a logika turnaje

- **Pairs mode**: round-robin + automatický `bye` při lichém počtu debatérů.
- **Groups mode**: validace vyvážené velikosti skupiny, možnost custom size, přepočet pro každé kolo.
- **Ranking**: výhry → Buchholz (síla soupeřů) → progressive score.
- **Awards**: tematická ocenění podle průběhu turnaje (streak, comeback, unbeaten, atd.).

## Interaktivní prvky (ID map)

<details>
<summary><strong>Rozbalit kompletní inventory ID (v3.1)</strong></summary>

### SVG tutorial icon sprite

- `ico-target`
- `ico-rules`
- `ico-blocks`
- `ico-shield`
- `ico-alert`
- `ico-rocket`
- `ico-silence`
- `ico-pause`
- `ico-proof`
- `ico-bulb`
- `ico-clock`
- `ico-key`
- `ico-search`
- `ico-ban`
- `ico-question`
- `ico-trophy`
- `ico-zap`
- `ico-x`
- `ico-check`

### Screen roots a setup shell

- `screen-setup`
- `screen-tutorial`
- `screen-intro`
- `screen-topicExplain`
- `screen-run`
- `appTitleText`
- `badgePlayers`
- `langToggle`
- `langCs`
- `langEn`
- `themeTrack`
- `btnWalkthrough`

### Téma, knihovna, debatéři, režim, časy

- `btnRandomTopic`
- `btnClearTopic`
- `swRandomTopic`
- `randomTopicSettings`
- `rndTopicMode`
- `rndCatPicker`
- `rndDiffPicker`
- `topicTextarea`
- `topicCategory`
- `topicSearch`
- `diffFilter`
- `topicList`
- `playerCountPill`
- `playersTextarea`
- `btnDedupe`
- `btnClearPlayers`
- `modePairs`
- `modeGroups`
- `groupSettings`
- `groupSizeAutoWrap`
- `groupSizeButtons`
- `groupSizeManualWrap`
- `groupSizeInput`
- `groupSizeManualHint`
- `groupSafeOff`
- `groupRoundsInput`
- `totalTimePill`
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
- `runtimeControlsHint`

### Presety, import panel a validace

- `presetBadge`
- `presetSelect`
- `btnPresetAll`
- `btnPresetNone`
- `presetList`
- `btnPresetReplace`
- `btnPresetAppend`
- `importDropZone`
- `importFileInput`
- `validationHint`

### Tutorial / intro / explain / run

- `tutProgressBar`
- `tutSlideCounter`
- `btnTutPrev`
- `tutAsk`
- `tutAskText`
- `btnTutNext`
- `introTopic`
- `introProLabel`
- `introConLabel`
- `introTimer`
- `introStructure`
- `btnSkipIntro`
- `btnBackToSetup1`
- `explainBlurb`
- `explainProLabel`
- `explainProHint`
- `explainConLabel`
- `explainConHint`
- `explainTimer`
- `btnSkipExplain`
- `phaseTitle`
- `phaseSub`
- `runTimerTop`
- `btnPause`
- `btnNext`
- `btnFullscreen`
- `btnRestart`
- `countdownPanel`
- `mainTimer`
- `pairsHeadLabel`
- `roundPill`
- `pairsGrid`
- `doneWrap`

### Hlasování, overlaye a modaly

- `voteBar`
- `voteConfirmBtn`
- `beepFlash`
- `overlay`
- `overlayTimer`
- `modal`
- `btnConfirmRestart`
- `btnCancelRestart`
- `pravidlaModal`
- `btnPravidlaClose`
- `importModal`
- `importModalTitle`
- `importSummary`
- `importTabs`
- `importChkAll`
- `importTbody`
- `importBtnApply`
- `importBtnAppend`
- `importBtnDelInvalid`
- `importBtnCancel`

### Walkthrough overlay + picker

- `wtOverlay`
- `wtSpotlight`
- `wtTooltip`
- `wtArrow`
- `wtClose`
- `wtStep`
- `wtTitle`
- `wtBody`
- `wtBack`
- `wtNext`
- `wtSkip`
- `wtProgress`
- `wtPickerOverlay`
- `wtPickerClose`
- `wtPickerGrid`
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
