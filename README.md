# PAIASA PM Team

Tim agenata za Claude Code u ulozi **Product Ownera i Project Managera**. Daš mu jednu rečenicu, link ili folder. On istraži tržište i konkurenciju, napiše definiciju proizvoda i plan realizacije i provede ih kroz nezavisne krugove revizije sa sudijom. Na kraju provjeri usklađenost dokumenata i napravi **promptove za DEV tim**, plus preporuku kakav tim projekat treba.

Par plugin: [PAIASA DEV Team](https://github.com/harymedire/paiasa-dev), koji te promptove implementira.

## Instalacija

Potreban je [Claude Code](https://claude.com/claude-code). U terminalu:

```bash
claude plugin marketplace add harymedire/paiasa-pm
```

```bash
claude plugin install paiasa-pm@paiasa-pm
```

Ili unutar Claude Codea: `/plugin marketplace add harymedire/paiasa-pm`, pa `/plugin install paiasa-pm@paiasa-pm`.

**Ažuriranje:**

```bash
claude plugin marketplace update paiasa-pm
```

```bash
claude plugin update paiasa-pm@paiasa-pm
```

U otvorenoj sesiji nakon ažuriranja pokreni `/reload-plugins`.

## Korištenje

Otvori Claude Code u **folderu projekta** (novi prazan folder za novi projekat) i pokreni:

```
/paiasa-pm:pm-team Aplikacija za online rezervaciju termina u frizerskim salonima u BiH
/paiasa-pm:pm-team https://link-na-sličan-proizvod.com
/paiasa-pm:pm-team resume
/paiasa-pm:pm-team accept .dev/evidence/P-03-booking-calendar.md
```

- **Novi projekat:** postavi najviše 5 pitanja koja mijenjaju smjer, pa radi. Ako ne odgovoriš, nastavlja s jasno označenim pretpostavkama.
- **Nastavak:** ako u folderu postoji `.product/STATE.md`, nastavlja tačno gdje je stao.
- **Tuđi započeti projekat:** prvo uradi pregled postojećeg materijala i analizu praznina, pa nastavlja.
- **Prihvatanje:** kad DEV tim vrati paket dokaza, PO agent provjerava svaki kriterij prihvatanja na osnovu samih dokaza. Gdje nešto fali, piše ciljani prompt za ispravku.

## Tok rada

```
0. Intake        → do 5 pitanja tebi ili označene pretpostavke
1. Istraživanje  → paralelni istraživači: tržište, konkurencija, korisnici, rješenja (s izvorima i datumima)
2. Nacrt         → Product Owner: product.md  |  Project Manager: delivery-plan.md
                   Tech Skeptic: tech-assessment.md (kad projekat to traži)
3. Revizija      → Head of Product + Delivery Lead (+ Tech Skeptic), svaki svježe, po rubrici
   Gate          → svi obavezni kriteriji zadovoljeni i 0 otvorenih kritičnih/značajnih nalaza
   Dorada        → ispravka ili obrazloženje (dnevnik odluka); najviše 3 kruga
4. Sudija        → samo kod zastoja, ponavljanja bez novih dokaza ili poslije 3. kruga
5. Usklađenost   → unakrsna provjera svih dokumenata
6. Predaja       → promptovi za DEV, redoslijed i paralelizam, team.md (ljudi + agenti + modeli)
7. Tebi          → sažetak + odluke koje su TVOJE (novac, rokovi, smjer), s preporukom
```

**Agenti predlažu, ti odlučuješ.** Sve što mijenja novac, obaveze, rokove ili osnovni smjer stiže u `decisions-for-you.md` s opcijama, posljedicama i preporukom. Šutnja nikad nije odobrenje.

## Šta dobiješ (u folderu projekta)

```
.product/
├── STATE.md               ← gdje smo, šta je sljedeće, šta čeka tebe
├── research/              ← istraživanje; svaka tvrdnja: [FACT] (izvor + datum) / [INFERENCE] / [ASSUMPTION] / [PROPOSAL]
├── product.md             ← problem, korisnici, MVP, backlog s user stories i kriterijima prihvatanja, metrike
├── delivery-plan.md       ← faze, zadaci, zavisnosti, procjene s osnovom, rizici, budžet (raspon), QA/UAT/release
├── tech-assessment.md     ← tehničke pretpostavke, arhitektura, sigurnost, troškovi
├── decisions.md           ← dnevnik odluka (sprječava vrtenje u krug)
├── decisions-for-you.md   ← tvoje odluke
├── reviews/               ← nalazi po krugovima, odgovori autora, presuda sudije
└── handoff/
    ├── README.md          ← redoslijed promptova i pravila projekta
    ├── team.md            ← preporuka tima: ljudi, dodatni agenti, modeli, obavezne kapije
    └── prompts/           ← 01-....md, 02-....md: daješ ih DEV timu
```

## Agenti i modeli

| Agent | Model | Zašto |
|---|---|---|
| Product Owner | Fable | najteže produktne odluke i MVP |
| Head of Product (recenzent) | Fable | strogi produktni pregled |
| Tech Skeptic | Fable | tehničke pretpostavke i sigurnost |
| Judge (sudija) | Fable | presude u zastoju |
| Project Manager | Opus | plan, zavisnosti, rizici |
| Delivery Lead (recenzent) | Opus | realnost plana |
| Researcher | Opus | istraživanje s izvorima |
| Consistency Checker | Opus | unakrsna provjera |

Fable 5.1 je prema Anthropicovoj dokumentaciji model za najzahtjevnije zaključivanje, ali je i najskuplji i najsporiji. Opus 5.5 je preporučeni model za većinu posla. Model se mijenja u polju `model:` u `agents/<agent>.md`.

## Predaja DEV timu

1. Instaliraj [PAIASA DEV Team](https://github.com/harymedire/paiasa-dev).
2. U repozitoriju koda: `/paiasa-dev:dev-team <putanja do .product/handoff>`. Prvi put daj cijeli `handoff` folder, da DEV tim pročita i `team.md`.
3. Kad DEV vrati dokaze, ovdje pokreni `/paiasa-pm:pm-team accept <putanja do evidence fajla>`.

## Struktura plugina

```
.claude-plugin/plugin.json, marketplace.json
skills/pm-team/SKILL.md          ← orkestracija cijelog procesa
skills/pm-team/reference/        ← rubrika, format nalaza, standardi istraživanja, šabloni,
                                   stanje i odluke, format dev prompta, preporuka tima
agents/                          ← 8 agenata
```

## Napomene

- Jedan potpuni prolaz koristi desetine agentskih poziva. Istraživanje se radi jednom, a u revizijama samo ciljano.
- Ovo je prva verzija (0.1.0). Najviše će se poboljšati iz stvarnih projekata, pa bilježi gdje griješi.
- Kod izmjena povećaj `version` u `.claude-plugin/plugin.json`, inače korisnici neće dobiti ažuriranje.

## English quick start

```bash
claude plugin marketplace add harymedire/paiasa-pm
```

```bash
claude plugin install paiasa-pm@paiasa-pm
```

Then, in a project folder, run `/paiasa-pm:pm-team <one sentence | URL | folder | resume | accept <evidence>>`. Documents follow the language of your input; dev prompts default to English.

## License

MIT
