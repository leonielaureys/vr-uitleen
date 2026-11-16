# AR-Bouw v1.0 — structuur, wapening en technieken in AR (Meta Quest 3)

Webapp: er is niets te installeren op de bril. Ze draait in de Quest-browser via WebXR (passthrough-AR).

## Online zetten (GitHub Pages, repo `ar-bouw-5`)
1. Pak `ar-bouw.zip` uit en upload **de inhoud** (index.html, qr.html, js/, projecten/) naar de hoofdmap van de repo › Commit.
2. Na 1–2 min staat de app op `https://leonielaureys.github.io/ar-bouw-5/` (eventueel `?v=…` erachter om de oude kopie te omzeilen).
3. Vaste modellen staan in `projecten/` en worden opgesomd in `projecten/index.json`.

## Werkwijze in een ruimte
1. Kies het project (of **QR scannen**) › **Start AR**.
2. Het menu hangt boven je linkercontroller. Wijs met de rechtercontroller en druk de trekker.
3. Eerste keer: **Kalibreren** (zie hieronder).
4. **Inmeten › Uit ruimte-scan** neemt de echte muren, het plafond, de deur en de ramen over uit de ruimte-instelling van de Quest.
5. **Plaatsen**: duid echte stopcontacten, schakelaar, lavabo, schacht enz. aan. Die gelden als *bevestigd*, en de app trekt de leidingen er volgens de regels naartoe.
6. **QR-bladen printen** (vanop de online versie!) › blad ophangen › **Kalibreren › QR registreren** (kruisje L, dan R).
   Volgende keer: QR scannen › Start AR › L en R aantikken. Of: **Bewaar positie** (persistent anchor).

## Kalibreren — twee stappen
**Kalibreren** is een eigen knop in het bedieningspaneel. De knoppen staan in twee rijen, in de volgorde waarin je ze gebruikt.

**Stap 1 — grof uitlijnen** (kies één van de vier):
| knop | wanneer |
|---|---|
| **1 · Scan uitlijnen** | je hebt de ruimte met de Quest gescand; de app legt het model op de muren van de scan (snelst, één druk) |
| **1 · 2 hoeken** | geen scan: wijs vloerhoek 1 en vloerhoek 2 aan volgens het plannetje |
| **1 · QR-kruisjes** | QR-blad opgehangen: tik kruisje L en kruisje R aan |
| **1 · Deur aanwijzen** | wijs de echte deur aan; de app draait het model naar de deur op plan |

**Stap 2 — handmatig bijstellen met de joysticks.** Na stap 1 springt **2 · Bijstellen** vanzelf op AAN (groen).
- linker joystick: het model **verschuiven** (voor/achter, links/rechts)
- rechter joystick: **draaien** (links/rechts) en de **hoogte** regelen (voor/achter)
- **Stap: fijn / grof** — grof gaat vier keer sneller, fijn voor de laatste centimeters
- rechtsboven in het paneel lees je af hoeveel je verschoven bent t.o.v. stap 1: `Δ 12 cm · +1,4° · +3 cm`
- **Terug naar stap 1** zet het model terug zoals de scan of de hoeken het zetten
- **Vastleggen ✓** bewaart de stand als persistent anchor; de bijgestelde stand wordt dan de nieuwe nulstand

Zet **2 · Bijstellen** op uit als je niet wil dat de joysticks het model verplaatsen terwijl je rondloopt.

## Modi
Verkennen · Kalibreren · Inmeten · Plaatsen · Snede · Meten (boorcheck + meetlint) · Notities · Bouwfasen · Presentatie

## Volle lijn = volgens plan · gestreept = aanname
- **Volle lijn, „✔ VOLGENS WAPENINGSPLAN &lt;blad&gt;"**: exact overgenomen van een wapeningsplan
  (staven, diameters, lengtes, beugelafstanden, staalkwaliteit). Er wordt niets herrekend.
  Voor het VR-lokaal: OB75 (kolommen 30/30 en 40/60), OB73 (balk B.6), OB76 (oplegging prefab vloer),
  staal BE 40 (TOR 40) / beugels BE 22 (A37).
- **Gestreept, „⚠ AANNAME"**: berekend omdat er geen plan voor bestaat. Gebruik dit nooit om te boren.
  Grondslag: EN 1990/1991/1992 (+ANB) voor de vloeren en de betonwanden, EC6/EC5 voor metselwerk en hout,
  het AREI voor elektriciteit, EN 12056-2 voor de afvoer, NBN D 50-001 voor ventilatie en het KB Basisnormen voor brand.
In het rapport staat per onderdeel of het van een plan komt (met bladnummer) of een aanname is;
onderaan staat uitdrukkelijk wat níét op de plannen staat.

Een plan meegeven in een eigen project: `"wapeningPlan"` in de ruimte (per kolomtype/balk de staven
en beugels, met `"bron": "<blad>"`), `"wapeningOntbreekt"` voor wat niet op de plannen staat,
en `"fyk"`/`"qk"`/`"vloerBekend"` in `"gebouw"` voor de gegevens die uit de plannen komen.

## Projecten toevoegen
- `projecten/*.json` + vermelden in `projecten/index.json` (vaste modellen). Een gebouw als IFC: zet `"ifc": "bestand.ifc"` in de JSON en het IFC-bestand in `projecten/`.
- **Exporteer project** in de app levert zo'n JSON op, inclusief inmeting, QR-bladen en notities.
