# Changelog

## 0.2.0 (2026-11-05)

Iz stvarnog projekta: tim se satima vrtio u krug (3 kruga revizije, sudija, ponovna provjera, druga presuda, provjera usklađenosti), uglavnom oko sve sitnijih neusklađenosti između dokumenata umjesto da dođe do odluke. Ova verzija zadržava strogost, ali proces brže dolazi do precizne odluke i jasno kaže šta treba od tebe.

**Brže do odluke**
- Najviše **2 kruga revizije** (bilo 3), pa **sudija jednom, sa zadnjom riječi**. Poslije sudije samo jedna ciljana provjera, bez novih nalaza i bez druge presude.
- **Detektor konvergencije:** ako broj kritičnih/značajnih nalaza u 2. krugu ne padne, ako se ponavljaju isti prigovori ili ako je većina nalaza mehanička, ide se odmah sudiji.
- **Tvrdi STOP kod tvoje odluke:** kad preostali nalazi zavise od otvorene odluke (budžet, +1 developer ili +1 sedmica, rez obima), proces ne radi novu doradu nego napiše `decision-needed.md` ("Odluka potrebna": odluka, opcije, posljedice, šta treba od tebe) i čeka.
- Novi gate status `pass-pending-user`: dokumenti su ispravni, čeka se samo tvoja odluka.
- Na kraju `SUMMARY.md`: **šta je spremno / šta treba od tebe / šta se mijenja ako odlučiš A ili B**, poznati nedostaci i potrošeni budžet revizije.
- Kad odgovoriš, nastavak radi samo ciljanu doradu pogođenih dijelova, a ne nove krugove.

**Manje lažnih nalaza**
- **Jedan broj, jedno mjesto:** tabela vlasništva (budžet, kapacitet, rok, broj priča, troškovi servisa). Ostali dokumenti se pozivaju na vlasničku sekciju, ne prepisuju broj.
- **Pravila preciznosti i tolerancije:** čovjek-dani cijeli (≥10 na 5), sedmice na 0,5, novac na 2 značajne cifre. Razlika unutar tolerancije nije nalaz; aritmetika se prikazuje jednom.
- **Test značaja** prije ocjene "značajno": mijenja li ispravka odluku, obim, rok, trošak ili ono što developer pravi?
- Unakrsne neusklađenosti se dijele na **mehaničke** (zastario prepisani broj, prenumerisan ID, referenca, zaokruživanje: sitno, orkestrator ih sam ispravi i zapiše u `sync-log.md`) i **suštinske** (vlasničke sekcije se stvarno ne slažu: značajno).
- **Disciplina 2. kruga:** recenzenti provjeravaju zatvaranje nalaza iz 1. kruga i promijenjene sekcije; novi nekritični nalaz na neizmijenjenom tekstu ne blokira.
- Nalazi koji zavise od otvorene korisničke odluke dobijaju `Depends on: U-xx` i ne traže ponovnu optimizaciju plana.

**Bez međusobnog gaženja fajlova**
- Samo orkestrator piše `decisions.md` i `decisions-for-you.md`; agenti predlažu unose u svojim fajlovima.
- Svaki autor ima svoj fajl odgovora (`responses-PO.md`, `responses-PM.md`, `responses-TS.md`).
- Rasponi ID-ova dodijeljeni unaprijed po agentu; ID-ovi su trajni (obrisano = `retired`, nikad prenumerisanje).

**Zadržano:** najviše 5 pitanja na početku pa označene pretpostavke, šutnja nikad nije odobrenje za novac/rokove/smjer, odluke se otvaraju samo uz nove dokaze/promijenjenu pretpostavku/grešku, Tech Skeptic, sudija može reći "nije spremno".

## 0.1.0

Prva verzija.
