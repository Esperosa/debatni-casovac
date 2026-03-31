# Debatní časovač (v3.1)

Moderní jednostránkový nástroj pro řízení debat v prohlížeči. Umí nastavit formát debaty, losovat témata a páry, odpočítávat čas s audio signály a přidává naučný režim pro začátečníky. Funguje plně offline – stačí otevřít HTML.

## Co aplikace dělá
- Kompletní web v jediném souboru [debatni-casovac-v3.1.html](debatni-casovac-v3.1.html) (dark/light/kontrastní režim, responzivní layout).
- Témata: knihovna s vyhledáváním a filtrem obtížnosti, náhodné téma pro každé kolo, ruční úprava textu.
- Debatéři: ruční seznam, odstranění duplicit, presety tříd, import z Excel/CSV/TSV/TXT/PDF s náhledem a volbou „nahradit/přidat“.
- Režimy: páry 1v1 nebo skupiny s automatickým rozdělením, bezpečný/vlastní počet členů, přepočet každé kolo, hlasování vítěze ve skupinách.
- Časování: příprava, čas kola, pauza mezi koly, odhad celku, zvukové upozornění 10/5/3/2/1, ambientní hudba v pauzách, samostatné hlasitosti.
- Naučný režim: průvodce debatou (slidy) a modální pravidla; ovládání během běhu: mezerník pauza, N další fáze, R restart, tlačítko fullscreen.
- Branding a metadata: autor zobrazen v UI i v metadatech, licence zakazuje odstranění brandingu bez souhlasu.

## Jak spustit (offline i online)
1. Stáhni nebo naklonuj repozitář: `git clone https://github.com/Esperosa/debatni-casovac.git`.
2. Otevři soubor [debatni-casovac-v3.1.html](debatni-casovac-v3.1.html) dvojklikem nebo přes prohlížeč (`Ctrl+O` → vybrat soubor). Nic se neinstaluje, vše běží v prohlížeči.

## Rychlý návod k použití
1. **Téma**: vyber z knihovny nebo napiš vlastní; můžeš zapnout „náhodné téma každé kolo“ a filtrovat sekce/obtížnost.
2. **Debatéři**: vlož jména (každé na řádek), klikni „Odstranit duplicity“. Můžeš použít presety tříd nebo importovat soubor (Excel/CSV/TSV/TXT/PDF), v náhledu zvol „Nahradit“ nebo „Přidat“.
3. **Režim**: zvol „Ve dvojicích“ nebo „Ve skupinách“. U skupin nastav velikost a počet kol; volitelně povol vlastní velikosti.
4. **Časy a audio**: nastav přípravu, čas kola a pauzu; můžeš zapnout Naučný režim, zvuk signálů, hudbu v pauzách a upravit hlasitosti.
5. **Start**: klikni „Start“. Pokud je zapnutý Naučný režim, projdi slidy a přepni na debatu.

## Ovládání během debaty
- Top lišta: Pauza/Play, Další fáze, Celá obrazovka, Restart (s potvrzením).
- Klávesy: mezerník = pauza/pokračovat, `N` = další fáze, `R` = restart.
- Páry/skupiny: zobrazeny pro aktuální kolo, při skupinovém režimu se po kolech přelosují; hlasování vítěze proběhne přes spodní lištu.
- Velký countdown se automaticky ukáže v závěru kola; zvukové signály upozorňují na 10/5/3/2/1 sekund.

## Nasazení na GitHub Pages
Repo je public a připravené. V GitHubu otevři **Settings → Pages**, vyber Branch `main`, Folder `/` a ulož. Publikovaná adresa bude `https://esperosa.github.io/debatni-casovac/debatni-casovac-v3.1.html` (počítej s několika minutami na první build). Pro offline použití dál slouží lokální HTML.

## Struktura repozitáře
- [debatni-casovac-v3.1.html](debatni-casovac-v3.1.html) – kompletní aplikace (HTML+CSS+JS+ikony, embedded data).
- [LICENSE](LICENSE) – omezená licence (osobní/interní užití, zákaz úprav/šíření bez souhlasu, povinnost ponechat branding).
- [README.md](README.md) – tento popis.
- [.gitignore](.gitignore)

## Branding a licence
- Autor: Jiří Pelikán (© 2024–2026). Podpis je pevně v UI a v metadatech HTML.
- Licence: viz [LICENSE](LICENSE). Nesmíš odstraňovat logo ani jméno autora; šíření, úpravy a komerce jen s písemným souhlasem.

## Příspěvky
Repozitář slouží k distribuci, nikoli k otevřenému vývoji. Pull requesty a forky s úpravami nejsou bez souhlasu autora přijímány. Potřeba úpravy nebo licence? Kontaktuj autora.
