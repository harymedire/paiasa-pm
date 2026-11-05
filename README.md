# PAIASA PM

Plugin za Claude Code koji radi **PM i PO posao**. Daš mu klijentovu dokumentaciju (fajl, folder, link ili tekst), a on je vjerno pretvori u **plan razvoja i procjenu**: obim, faze, napor, tim, budžet, kalendar i rizike. Uz to izdvoji **rupe u dokumentaciji** i **pitanja za klijenta**.

Radi sam. Agente pokreće samo kad kažeš **„DA“**, i to tek nakon što ti pokaže koje agente predlaže i koliko bi to koštalo.

Za strogu, nezavisnu provjeru opravdanosti projekta (strogi recenzenti, sudija, više rundi) koristi zaseban plugin **PAIASA Validate** (`paiasa-validate`).

Par plugin: [PAIASA DEV Team](https://github.com/harymedire/paiasa-dev), koji implementira promptove.

## Instalacija

Potreban je [Claude Code](https://claude.com/claude-code). U terminalu:

```bash
claude plugin marketplace add harymedire/paiasa-pm
```

```bash
claude plugin install paiasa-pm@paiasa-pm
```

**Ažuriranje:**

```bash
claude plugin marketplace update paiasa-pm
```

```bash
claude plugin update paiasa-pm@paiasa-pm
```

U otvorenoj sesiji nakon ažuriranja pokreni `/reload-plugins`. Izmjene se rade u ovom repozitoriju, ne u lokalnoj kopiji pod `.claude/plugins/cache`, jer se ona prepiše pri ažuriranju.

## Korištenje

Otvori Claude Code u folderu projekta i pokreni:

```
/paiasa-pm:pm-team specifikacija.docx
/paiasa-pm:pm-team docs/
/paiasa-pm:pm-team napiši promptove za DEV tim
/paiasa-pm:pm-team recenziraj plan
/paiasa-pm:pm-team accept .dev/evidence/P-03.md
```

## Pravila

- **Obim je dokumentacija.** U plan ulazi samo ono što dokument traži, s njegovim ID-jevima. Popunjava se samo ono što dokument ostavlja prazno (napor, tim, budžet, kalendar), i sve je označeno kao procjena s osnovom i rasponom.
- **Bez izmišljanja.** Rupe i kontradikcije se navode, ne rješavaju. Nepoznato ide u „Pitanja za klijenta“: zašto je bitno, šta plan pretpostavlja i do kada treba odgovor.
- **Tvoje je da biraš.** Ideje modela idu u prilog „Opciono“, s cijenom.
- **„Presudi“ znači presudi.** Model odluči sam i ne vraća ti pitanje.
- **Agenti samo uz „DA“.** Bez toga model radi sam, uz najviše oko 5 web pretraga. Ako vidi da će preći odobreni trošak za više od 30 %, staje i pita.
- **Preciznost prema odluci.** Cijeli osoba-dani, sedmice na 0,5, novac kao raspon na dvije cifre.
- **Recenzije, DEV promptovi i prihvatanje rade se samo na zahtjev.** Recenzija ima jednu rundu, a recenzent daje presudu i najviše 5 blokirajućih nalaza.

## Šta dobiješ

```
<projekat>/plan/
├── plan-razvoja.md   ← 11 poglavlja: sažetak, obim, faze i kalendar, napor, kritični put,
│                        tim, budžet, rizici, rupe, pitanja za klijenta, opciono (+ dnevnik izmjena)
└── prompts/          ← samo na zahtjev: promptovi za DEV tim
```

U chatu dobiješ samo 5–10 redova: gdje je fajl, raspon napora i budžeta, 3 najveća rizika i broj pitanja za klijenta.

## Agenti (samo uz tvoje „DA“)

| Agent | Model | Za šta | Orijentacioni trošak |
|---|---|---|---|
| researcher | Opus | jedna tema istraživanja s izvorima | 130–230k tokena |
| plan-reviewer | Opus | jedna recenzija: proizvod, isporuka ili tehnika | 140–310k tokena |

Trošak je izmjeren na jednoj stvarnoj sesiji: ~45 pokretanja agenata potrošilo je ~26 % sedmičnog limita.

## Struktura plugina

```
.claude-plugin/plugin.json, marketplace.json
skills/pm-team/SKILL.md            ← cijeli način rada
skills/pm-team/reference/          ← standardi istraživanja, format DEV prompta
agents/                            ← researcher, plan-reviewer
```

Promjene su u [CHANGELOG.md](CHANGELOG.md). Kod izmjena povećaj `version` u `.claude-plugin/plugin.json`, inače korisnici neće dobiti ažuriranje.

## English quick start

Install with the commands above. Then, in a project folder, run `/paiasa-pm:pm-team <client documentation>`. You get one development plan with estimate and client questions, in the language of your input. No agents run without your explicit yes.

## License

MIT
