# PAIASA PM Team

Tim agenata za Claude Code u ulozi **Product Ownera i Project Managera**. Daš mu jednu rečenicu, link ili folder. On istraži tržište i konkurenciju, napiše definiciju proizvoda i plan realizacije i provede ih kroz najviše dva nezavisna kruga revizije, a sudija ima zadnju riječ. Na kraju uskladi dokumente i napravi **promptove za DEV tim**, plus preporuku kakav tim projekat treba. Kad ne može dalje bez tebe, stane i na jednoj stranici kaže tačno šta mu treba.

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
   Trijaža       → mehaničke neusklađenosti (zastario broj, ID, referenca, zaokruživanje) = sitno,
                   orkestrator ih sam ispravi; nalazi koji zavise od tvoje odluke se ne vrte u krug
   Gate          → svi obavezni kriteriji zadovoljeni i 0 otvorenih kritičnih/značajnih nalaza
   Dorada        → ispravka ili obrazloženje (dnevnik odluka); najviše 2 kruga
   STOP          → ako preostali nalazi zavise od tvoje odluke: "Odluka potrebna" i čeka tebe
4. Sudija        → jednom, zadnja riječ: poslije 2. kruga, ako broj nalaza ne pada ili se ponavljaju
                   isti prigovori; poslije njega samo jedna ciljana provjera
5. Usklađenost   → orkestrator ispravi mehaničko, provjerivač jednom, autor jednom za suštinsko
6. Predaja       → promptovi za DEV, redoslijed i paralelizam, team.md (ljudi + agenti + modeli)
7. Tebi          → SUMMARY.md: šta je spremno / šta treba od tebe / šta se mijenja ako odlučiš A ili B
```

**Agenti predlažu, ti odlučuješ.** Sve što mijenja novac, obaveze, rokove ili osnovni smjer stiže u `decisions-for-you.md` s opcijama, posljedicama i preporukom. Šutnja nikad nije odobrenje.

### Kako se sprječava vrtenje u krug (od 0.2.0)

- **Jedan broj, jedno mjesto.** Budžet, kapacitet, rok, broj Must priča i troškovi servisa pišu se samo u svojoj "vlasničkoj" sekciji; ostali dokumenti se na nju pozivaju (`→ delivery-plan.md §7`), ne prepisuju je.
- **Preciznost prema odluci.** Procjene u cijelim čovjek-danima, sedmice na 0,5, novac na dvije značajne cifre. Razlika unutar tolerancije nije nalaz.
- **Test značaja.** Nalaz je značajan samo ako njegova ispravka mijenja odluku, obim, rok, raspon troška ili ono što developer pravi.
- **Fiksan budžet revizije.** Najviše 2 kruga, 1 sudija, 1 ciljana provjera. Detektor konvergencije: ako broj nalaza ne pada, ide se odmah sudiji.
- **Ne optimizuje se oko neodlučenog.** Ako je otvoreno npr. "+1 developer ili +1 sedmica", svaka opcija se izračuna jednom, plan ide na preporučenu kao označenu pretpostavku, a kad sve ostalo čeka na to, proces stane i pita tebe.
- **Bez međusobnog gaženja.** Samo orkestrator piše `decisions.md` i `decisions-for-you.md`; svaki agent ima unaprijed dodijeljen raspon ID-ova i svoj fajl odgovora. ID-ovi se nikad ne prenumerišu.

## Šta dobiješ (u folderu projekta)

```
.product/
├── STATE.md               ← gdje smo, šta je sljedeće, šta čeka tebe, potrošeni budžet revizije
├── SUMMARY.md             ← šta je spremno / šta treba od tebe / šta se mijenja ako odlučiš A ili B
├── decision-needed.md     ← "Odluka potrebna": jedna stranica, kad proces čeka tebe
├── research/              ← istraživanje; svaka tvrdnja: [FACT] (izvor + datum) / [INFERENCE] / [ASSUMPTION] / [PROPOSAL]
├── product.md             ← problem, korisnici, MVP, backlog s user stories i kriterijima prihvatanja, metrike
├── delivery-plan.md       ← faze, zadaci, zavisnosti, procjene s osnovom, rizici, budžet (raspon), QA/UAT/release
├── tech-assessment.md     ← tehničke pretpostavke, arhitektura, sigurnost, troškovi
├── decisions.md           ← dnevnik odluka (sprječava vrtenje u krug)
├── decisions-for-you.md   ← tvoje odluke
├── reviews/               ← nalazi po krugovima, trijaža, odgovori autora, presuda sudije, sync-log.md
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
| Consistency Checker | Opus | unakrsna provjera (mehaničko vs suštinsko) |

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
                                   stanje i odluke, izlazi za korisnika (odluka potrebna, sažetak),
                                   format dev prompta, preporuka tima
agents/                          ← 8 agenata
```

## Napomene

- Jedan potpuni prolaz koristi desetine agentskih poziva. Istraživanje se radi jednom, a revizija ima fiksan budžet (2 kruga + sudija + 1 provjera).
- Trenutna verzija: 0.2.0. Promjene su u [CHANGELOG.md](CHANGELOG.md). Najviše se poboljšava iz stvarnih projekata, pa bilježi gdje griješi.
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
