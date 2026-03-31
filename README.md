# Debatní časovač (v3.1)

Jednosouborový (HTML) nástroj pro řízení debat. Zvládá výběr/losování témat, rozdělení debatérů do dvojic nebo skupin, řízení časů se zvuky a hudbou, hlasování vítěze a naučný režim pro začátečníky. Vše běží lokálně v prohlížeči.

## Přehled obrazovek
- **Nastavení** – volba tématu, seznam debatérů, presety tříd, import ze souboru, režim (dvojice/skupiny), časy, zvuky, hudba, naučný režim, kontrola vstupů.
- **Tutorial** – 6 slidů: co je debata, pravidla, metoda SEXI, jak vyvracet, časté chyby, rychlý recap.
- **Intro** – téma + legendy PRO/PROTI, úvodní odpočet.
- **Vysvětlení tématu** – blurb a tipy PRO/PROTI pro aktuální téma, samostatný odpočet.
- **Běh debaty** – top lišta s časem, fázemi a tlačítky, mřížka párů/skupin, velký countdown v závěru kola, hlasování (skupiny), restart dialog.
- **Výsledky** – souhrn kol, páry/skupiny, zvýraznění vítězů, tabulka a ocenění (skupinový režim).

## Funkce podle panelů
**Téma**
- Knihovna s kategoriemi, vyhledáváním a filtrem obtížnosti (chip výběr 1–5).
- Náhodné téma každé kolo (mód „zcela náhodné“ nebo „vybrané sekce“ + kategorie + filtr obtížnosti).
- Ruční editace textu, rychlá volba „Náhodné“ / „Vymazat“.

**Debatéři**
- Textarea (jméno na řádek), „Odstranit duplicity“, „Vymazat seznam“.
- Presety tříd (výběr 9.A / 9.B + výběr všech/ničeho, nahradit/přidat do seznamu, live badge souhrnu).
- Import Excel/CSV/TSV/TXT/PDF: drag&drop, PDF parser (SO export), náhled tabulky s editací, filtry, „Nahradit“ / „Přidat“ / „Odebrat neúplné“, hromadné checkboxy.
- Kontrola vstupů ukazuje problémy (např. málo debatérů, lichý počet apod.).

**Režim**
- Přepínač „Ve dvojicích“ (1v1) vs. „Ve skupinách“ (losování skupin + hlasování vítězů).
- Skupiny: předvolené velikosti (safe mode, aby vyšly sudé skupiny), volitelně vlastní velikost (checkbox „Vlastní velikost“), počet kol, reshuffle každý round.

**Časy, zvuk, hudba**
- Pauza na začátku, čas na kolo, pauza mezi koly + odhad celkové délky.
- Zvuky: start/stop, upozornění 10/5/3/2/1 s bliknutím overlay; samostatná hlasitost.
- Hudba v pauzách (ambient), samostatná hlasitost; tlačítka ukázek.

**Naučný režim**
- Přepínač „Naučný režim – Prezentace“: před startem spustí 6 slidů (viz výše) a pak přejde do běhu.
- Samostatné modální „Pravidla debaty“ kdykoli ze setupu.

**Vzhled a přístupnost**
- Přepínač motivu (dark/light/kontrastní), responzivní layout, čitelné fonty, velké ovládací prvky.
- Velké odpočty a blikání pro konce kol, ovládání je popsané ARIA atributy.

## Ovládání v běhu
- Tlačítka nahoře: Pauza/Play, Další fáze, Celá obrazovka, Restart (s potvrzením).
- Klávesy: mezerník = pauza/pokračovat, `N` = další fáze, `R` = restart; pro fullscreen použij klávesu pro prohlížeč (např. F11).
- Velký countdown se zobrazí automaticky pod 10 s (hodnota `COUNTDOWN_PANEL_THRESHOLD`).
- Skupinový režim: klikni na vítěznou stranu/kartu → potvrdíš v liště „Klikněte na stranu, která vyhrála“ → tlačítko „Pokračovat“.
- Výsledky: po skončení kol se zobrazí souhrn, zvýraznění vítězů a tabulka (včetně W/L/Buchholz, pokud je skupinový režim a hlasování proběhlo).

## Typický postup
1) Otevři [debatni-casovac-v3.1.html](debatni-casovac-v3.1.html) (stačí dvojklik nebo `Ctrl+O` v prohlížeči). Funguje offline.
2) **Téma**: vyber z knihovny nebo zapni náhodné téma (případně filtrem omez kategorie/obtížnost). Text můžeš upravit ručně.
3) **Debatéři**: vlož jména, odstraň duplicity, případně načti preset nebo importuj soubor (Excel/CSV/TSV/TXT/PDF). Zvol „Nahradit“ nebo „Přidat“.
4) **Režim**: vyber dvojice nebo skupiny. U skupin nastav velikost/počet kol a zda povolit vlastní velikosti.
5) **Časy a audio**: nastav přípravu, kolo, pauzu; případně zapni Naučný režim, zvuky a hudbu; dolaď hlasitosti.
6) Klikni **Start**. Pokud je Naučný režim, projdeš slidy → Intro → Vysvětlení tématu → Běh.
7) Během debaty používej mezerník / N / R nebo tlačítka. Ve skupinách po každém kole vyber vítěze, ve dvojicích se losují páry pro další kolo.
8) Po skončení kol uvidíš výsledky; poté můžeš restartovat a nastavit novou debatu.

## Nasazení na GitHub Pages
Repo je public a připravené. V GitHubu otevři **Settings → Pages**, Branch `main`, Folder `/`, ulož. První build trvá pár minut. Veřejná adresa: `https://esperosa.github.io/debatni-casovac/debatni-casovac-v3.1.html` (zůstává aktuální i pro nové verze).

## Struktura
- [debatni-casovac-v3.1.html](debatni-casovac-v3.1.html) – kompletní aplikace (HTML/CSS/JS + data knihovny témat).
- [LICENSE](LICENSE) – omezená licence (osobní/interní užití, zákaz úprav/šíření bez souhlasu, povinnost ponechat branding).
- [README.md](README.md) – tento popis.
- [.gitignore](.gitignore)

## Branding a licence
- Autor: Jiří Pelikán (© 2024–2026). Podpis je trvale v UI i v meta hlavičce HTML.
- Branding (logo/jméno) se nesmí odstraňovat ani obcházet. Úpravy, šíření a komerční použití jen s písemným souhlasem (viz [LICENSE](LICENSE)).

## Poznámky k příspěvkům
Repo je určeno k distribuci. Pull requesty ani forky s úpravami se bez souhlasu autora nepřijímají. Pro úpravy nebo rozšířené licence kontaktuj autora.
