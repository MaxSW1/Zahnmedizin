# Bereich 9: Technologie-Strategie

> Max' Software-/Tech-Background ist sein groesster Wettbewerbsvorteil gegenueber 99% aller Zahnaerzte. Dieses Kapitel dokumentiert, wie er diesen Vorteil systematisch in eine ueberlegene Praxisfuehrung, eigene Tools und ggf. ein Dental-Tech-Business umwandelt.

---

## 9.1 Praxissoftware-Landschaft Deutschland

### 9.1.1 Marktueberblick

Der deutsche Markt fuer zahnmedizinische Praxisverwaltungssoftware (PVS) wird von wenigen Anbietern dominiert. Laut KZBV-Statistik 2024 sieht die Verteilung bei elektronisch eingereichten Abrechnungen so aus:

| Rang | Software | Hersteller | Marktanteil (KZBV 2024) | Abrechnungen |
|------|----------|-----------|------------------------|-------------|
| 1 | DS-Win-Plus | Dampsoft | ~35% | ~12.000 |
| 2 | Z1 / Z1.PRO | CGM (CompuGroup Medical) | ~23% | ~8.100 |
| 3 | Charly | solutio GmbH & Co. KG | ~10% | ~3.500 |
| 4 | ivoris | Computer konkret AG | ~8% (KFO: >60%) | variabel |
| 5 | Weitere | div. | ~24% | variabel |

**Branchenstandard VDDS:** Der Verband Deutscher Dental-Software Unternehmen (VDDS e.V.) repraesentiert ~90% des Marktes und definiert standardisierte Schnittstellen (VDDS-media, aktuell Version 1.4) fuer den Datenaustausch zwischen PVS und Drittsystemen (Roentgen, Scanner, Kameras etc.).

### 9.1.2 Detailbewertung der relevanten Systeme

#### Dampsoft DS-Win / DS4

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktanteil** | ~35% – klarer Marktfuehrer, jede 3. Praxis in Deutschland |
| **Architektur** | DS-Win: klassisch Client-Server (Windows); DS4: neu, webbasiert/cloudfaehig |
| **Kernfunktionen** | Befunddokumentation, BEMA/GOZ-Abrechnung, Patientenverwaltung, Analysen, HKP, ePA 3.0 |
| **Erweiterungen** | Hygiene, Terminmanagement, Abrechnung/Finanzen, QM, Athena (digitale Anamnese/Aufklaerung) |
| **TI-Integration** | Vollstaendig (ePA, KIM, eRezept, eAU, eLABZ) |
| **Schnittstellen** | VDDS-media, TI-Konnektor (e-connect), Roentgensysteme, Dr. Flex (Online-Termine) |
| **API/Erweiterbarkeit** | Keine offene REST-API bekannt; Integration nur ueber VDDS-Standard und Partnerprogramme |
| **Kosten** | Individuell kalkuliert, nicht oeffentlich; geschaetzt: Einmalkosten 3.000-5.500 EUR + ~100 EUR/Monat Wartung |
| **Staerken** | Groesstes Oekosystem, meiste Schulungen/Webinare, breite Partnerlandschaft, DS4 als Zukunftspfad |
| **Schwaechen** | DS-Win technisch veraltet (Windows-only); DS4 noch im Aufbau; geschlossenes Oekosystem, keine offene API |

**Bewertung fuer Max:** DS-Win ist der sichere Standard. DS4 koennte interessant werden, wenn Dampsoft eine echte API oeffnet. Aktuell schwer erweiterbar fuer eigene Entwicklungen.

#### CGM Z1 / Z1.PRO

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktanteil** | ~23% – groesster Einzelanbieter nach Dampsoft |
| **Architektur** | Client-Server (Windows); Z1 als Basis in Z1.PRO integriert |
| **Kernfunktionen** | Patientenverwaltung, BEMA/GOZ/individuelle Abrechnung, Praxiskalender, Ressourcenplanung |
| **TI-Integration** | Vollstaendig (TI, KIM, Roentgensysteme) |
| **Schnittstellen** | TI-Konnektor, VDDS-media, DATEV-Export (neu), Roentgenintegration |
| **API/Erweiterbarkeit** | Keine offene REST-API; Integration ueber CGM-Oekosystem und VDDS |
| **Kosten** | Individuell, nicht oeffentlich; vergleichbar mit Dampsoft |
| **Staerken** | Grosser Konzern (CGM), breites Produktportfolio, DATEV-Anbindung, >7.000 aktive Zahnaerzte |
| **Schwaechen** | CGM als Grosskonzern langsam in Innovation; Z1 technisch nicht mehr modern; Support gemischt bewertet |

**Bewertung fuer Max:** Solides System, aber fuer eine technologie-getriebene Neugr. wenig innovativ. CGMs Groesse kann Vor- und Nachteil sein.

#### Charly (solutio)

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktanteil** | ~10%, ueber 27.000 Lizenzen |
| **Architektur** | **charly-Web**: browserbasiert, plattformunabhaengig (Windows, macOS, Linux), Container-Technologie |
| **Kernfunktionen** | Terminplanung, Behandlungsplanung, Abrechnung, Controlling, QM, Patientenkommunikation |
| **Modularitaet** | Drei Versionen (S, M, XL); modularer Aufbau – nur bezahlen was man nutzt |
| **Schnittstellen** | VDDS-media, Roentgen/Scanner/Kamera, Nelly-Schnittstelle, div. Drittanbieter |
| **API/Erweiterbarkeit** | Nelly-Integration dokumentiert; ansonsten keine offene API bekannt |
| **Kosten** | Monatliche Lizenz pro Arbeitsplatz (gilt als "teuer" in der Community); keine hohen Einmalkosten |
| **Staerken** | Moderne Web-Architektur (charly-Web!), plattformunabhaengig, Container-basierte Updates, Mac-kompatibel |
| **Schwaechen** | Hohe laufende Kosten; Marktanteil deutlich kleiner als Dampsoft/CGM |

**Bewertung fuer Max:** Charly-Web ist architektonisch am modernsten unter den etablierten Systemen. Die Plattformunabhaengigkeit und Container-Technologie sind positiv. Wenn Max ein PVS sucht, das technisch zukunftsfaehig ist, ist Charly-Web ein ernsthafter Kandidat.

#### teemer (ARZ.dent GmbH)

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktanteil** | Wachsend, Teil der ARZ-Gruppe (~17.000 Kunden, 9 Tochtergesellschaften, ~1.000 Mitarbeiter) |
| **Architektur** | **Vollstaendig cloudbasiert** – erste cloudbasierte Loesung seit 2014 bei KZBV zugelassen |
| **Kernfunktionen** | Anamnese bis Abrechnung, digitale Patientenaufnahme, KI-gestuetzte Rechnungspruefung |
| **KI-Integration** | Dentero-Integration (seit Okt. 2025) fuer KI-gestuetzte Sprachdokumentation und Abrechnung |
| **Schnittstellen** | Offen fuer Integrationen, Dentero-Anbindung, Cloud-basiert |
| **Kosten** | Einmalig: Customizing + Training; monatlich: nach Behandlern und Standorten; alles inklusive (keine Modulkosten) |
| **Datensicherung** | Georedundant in konzerneigenen Rechenzentren in Deutschland |
| **Staerken** | Echte Cloud-Native-Architektur, kein lokaler Server noetig, KI-Integration, modernes UX, alles-inklusive-Preismodell |
| **Schwaechen** | Kleinerer Marktanteil als die "Grossen Drei"; abhaengig von Internetverbindung |

**Bewertung fuer Max:** teemer ist der innovativste Kandidat – echte Cloud, KI-Integration, modernes Konzept. Fuer eine Neugruendung 2030+ die logischste Wahl. Die ARZ-Gruppe als Mutterkonzern bietet Stabilitaet.

#### Roger

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktposition** | Kein vollstaendiges PVS, sondern **Ergaenzungssoftware** zum bestehenden PVS |
| **Architektur** | Cloud-basiert, Mac- und Windows-kompatibel |
| **Kernfunktionen** | Automatische HKP-Nachverfolgung (+25% Umsetzungsquote), WhatsApp-Kommunikation, Recall, digitale Anamnese, eSigning |
| **Integration** | Kompatibel mit fast allen gaengigen PVS; Synchronisation in 20 Min eingerichtet |
| **Kosten** | Ab 129 EUR/Zahnarzt/Monat |
| **Staerken** | Sofort einsetzbar neben bestehendem PVS; starker Fokus auf Umsatzsteigerung und Patientenkommunikation |
| **Schwaechen** | Kein vollstaendiges PVS – man braucht immer noch ein Hauptsystem; zusaetzliche Kosten |

**Bewertung fuer Max:** Roger ist kein PVS-Ersatz, sondern ein Automatisierungs-Add-on. Kann in der Anfangsphase sinnvoll sein, um schnell Automatisierung zu bekommen, waehrend man mit einem klassischen PVS arbeitet. Mittelfristig: Max koennte aehnliche Funktionalitaet selbst bauen.

#### Dental4Windows (Centaur Software)

| Kriterium | Bewertung |
|-----------|-----------|
| **Marktposition** | Marktfuehrer in Australien (~50% Marktanteil dort), international expandierend (Dubai, MENA) |
| **Architektur** | Web-basiert und On-Premise verfuegbar, Mobile App (D4W Mobile) |
| **Kernfunktionen** | Terminplanung, Klinisches Charting, Inventar, Marketing, Reporting |
| **Relevanz DE** | **Gering** – nicht fuer den deutschen Markt (BEMA/GOZ) angepasst |
| **Staerken** | Moderne Architektur, gutes UX, Enterprise-Loesung fuer grosse Praxisketten |
| **Schwaechen** | Keine deutsche Lokalisierung, kein BEMA/GOZ, keine TI-Anbindung |

**Bewertung fuer Max:** Fuer eine deutsche Praxis nicht relevant. Aber als **Benchmark** fuer modernes Praxissoftware-Design interessant – falls Max eigene Software entwickelt, lohnt ein Blick auf D4Ws UX und Feature-Set.

### 9.1.3 Bewertungsmatrix: Welches System fuer eine moderne 2030+ Praxis?

| Kriterium (Gewichtung) | DS-Win/DS4 | Z1.PRO | Charly-Web | teemer | Roger* |
|------------------------|-----------|--------|------------|--------|--------|
| Cloud/Web-Architektur (25%) | 3/5 (DS4) | 2/5 | 4/5 | **5/5** | 4/5 |
| API/Erweiterbarkeit (20%) | 2/5 | 2/5 | 3/5 | **4/5** | 3/5 |
| KI-Integration (15%) | 2/5 | 2/5 | 3/5 | **5/5** | 3/5 |
| Oekosystem/Partner (15%) | **5/5** | 4/5 | 3/5 | 3/5 | 3/5 |
| Zukunftssicherheit (15%) | 3/5 | 2/5 | 4/5 | **5/5** | 4/5 |
| Kosten-Leistung (10%) | 3/5 | 3/5 | 2/5 | 4/5 | 3/5 |
| **Gewichteter Score** | **2,85** | **2,40** | **3,30** | **4,40** | **3,35** |

*Roger ist kein vollstaendiges PVS und daher nur bedingt vergleichbar.

### 9.1.4 Empfehlung fuer Max

**Primaerwahl: teemer** – Cloud-native, KI-Integration (Dentero), modernes Konzept, alles-inklusive-Preis. Fuer eine Neugruendung ~2030 die zukunftssicherste Wahl.

**Alternative: Charly-Web** – Falls teemer nicht ueberzeugt, ist Charly-Web architektonisch ebenfalls modern und hat ein groesseres Oekosystem.

**Ergaenzend: Roger** – Unabhaengig vom PVS als Automatisierungs-Layer fuer Patientenkommunikation, HKP-Nachverfolgung und Recall einsetzbar.

**Strategische Ueberlegung:** Max sollte waehrend des Studiums alle Systeme ueber Demos und Hospitationen kennenlernen. Der PVS-Markt wird sich bis 2030 weiter Richtung Cloud und KI bewegen – die finale Entscheidung sollte erst 12-18 Monate vor Praxiseroeffnung fallen.

---

## 9.2 Automatisierungspotenziale in der Zahnarztpraxis

### 9.2.1 Terminmanagement und Online-Buchung

| Loesung | Typ | Kosten/Monat | Staerken | Schwaechen |
|---------|-----|-------------|---------|------------|
| **Doctolib** | Plattform + Terminbuchung | 139 EUR/Behandler | Hoechste Google-Sichtbarkeit, groesste Patientenbasis, starke Marke | Datenschutz nur Note 3,6; hohe Kosten bei mehreren Behandlern; Plattform-Abhaengigkeit |
| **Jameda** | Bewertungsportal + Termine | 99 EUR/Arzt (Gold Pro) | Guter Datenschutz (Note 1,9), starke Bewertungsplattform, guenstiger | Geringere Sichtbarkeit als Doctolib, weniger Buchungsfunktionen |
| **Dr. Flex** | Online-Termine | guenstiger | Bester Datenschutz (Note 1,6), direkte PVS-Integration (z.B. DS-Win, Charly) | Geringere Bekanntheit bei Patienten |
| **Eigene Loesung** | Selbst entwickelt | Entwicklungskosten | Volle Kontrolle, keine Abhaengigkeit, individuelle Anpassung | Aufwand, keine Plattform-Sichtbarkeit |

**Empfehlung:** Doctolib oder Jameda fuer Sichtbarkeit UND gleichzeitig eigene Online-Buchung auf der Praxis-Website (via PVS-Integration oder Eigenentwicklung). Die Plattformen als Akquise-Kanal nutzen, aber nicht abhaengig werden.

### 9.2.2 Recall-Automatisierung

Recall (Wiedereinbestellung zur PZR, Kontrolle etc.) ist einer der wichtigsten Umsatztreiber. Automatisierung spart bis zu **1,5 Stunden pro Tag** und reduziert No-Shows um **bis zu 30%**.

**Rechtliche Voraussetzung:** Patienten muessen schriftlich einwilligen, per WhatsApp/SMS/E-Mail erinnert zu werden.

| Loesung | Kanal | Integration | Besonderheiten |
|---------|-------|-------------|----------------|
| **Roger** | WhatsApp, SMS (Fallback) | Fast alle PVS | Automatischer Kanalwechsel; DSGVO-konform; Server in DE |
| **dentportSMS** | SMS | Div. PVS | Spezialist fuer SMS-basierte Terminerinnerungen |
| **recallclinics** | WhatsApp | Div. PVS | WhatsApp-basierte Patientenkommunikation |
| **PVS-intern** | E-Mail, Brief | Nativ | Meist nur E-Mail/Brief; weniger automatisiert |

**Max' Automatisierungspotenzial:** Ein selbst entwickeltes Recall-System koennte:
- Intelligente Recall-Intervalle basierend auf Patientenrisikoprofil (Parodontitis-Patienten haeufiger)
- Multi-Channel-Kommunikation (WhatsApp > SMS > E-Mail > Brief als Fallback-Kaskade)
- Automatische Terminvorschlaege basierend auf Praxisauslastung
- A/B-Testing von Recall-Nachrichten fuer optimale Response-Rate

### 9.2.3 Patientenkommunikation

| Kanal | Tool | DSGVO-Status | Anwendung |
|-------|------|-------------|-----------|
| **WhatsApp Business** | Roger, recallclinics | Konform (mit Einwilligung, Server in DE) | Terminerinnerung, Recall, HKP-Nachverfolgung |
| **SMS** | dentportSMS, Roger (Fallback) | Konform (mit Einwilligung) | Terminerinnerung (fuer Patienten ohne WhatsApp) |
| **E-Mail** | PVS-intern, Nelly | Konform (mit Einwilligung) | Befundmitteilung, Rechnungen, Informationen |
| **Praxis-App** | Eigenentwicklung | Volle Kontrolle | Termine, Befunde, Recall, Dokumente, Bonusheft digital |

**Strategische Idee:** Eine eigene Patienten-App (PWA = Progressive Web App, kein App-Store noetig) koennte:
- Digitales Bonusheft
- Terminuebersicht und -buchung
- Behandlungsplaene einsehen und akzeptieren
- Rechnungen und Dokumente
- Push-Benachrichtigungen fuer Recall
- Spart Drittanbieter-Kosten und schafft Patientenbindung

### 9.2.4 Abrechnungsautomatisierung

Die Abrechnung in der Zahnmedizin ist zweigeteilt:
- **BEMA** (Bewertungsmassstab): Fuer gesetzlich Versicherte, Abrechnung ueber KZV
- **GOZ** (Gebuehrenordnung fuer Zahnaerzte): Fuer Privatpatienten und Zusatzleistungen

| Loesung | Funktion | Besonderheit |
|---------|----------|-------------|
| **Dentero** | KI-Sprachdokumentation → automatische Abrechnungsvorschlaege (BEMA, GOZ, GOAe) | In teemer integriert; erkennt Abbreviaturen und Fachbegriffe |
| **Sonia** | KI-Sprachassistent; transkribiert Behandlungen automatisch | 12 Mio. EUR Seed-Finanzierung; spart 5-10 Min/Arbeitsstunde; deckt 12-15% vergessene Abrechnungspositionen auf |
| **Doctos** | KI-Transkription + automatische Abrechnungserfassung | Bis zu 60% Zeitersparnis |
| **Dentiscribe** | KI-Dokumentation und Abrechnung | Neuerer Marktteilnehmer |
| **Nelly** | Automatisierte Privatpatientenabrechnung + digitale Anamnese | Direkte PVS-Schnittstelle (u.a. Charly) |
| **KZV-Factoring** | Sofortige Auszahlung statt quartalsweiser Kassenabrechnung | Verbessert Liquiditaet erheblich |

**Umsatzpotenzial durch KI-Abrechnung:** Sonia-Kunden berichten von **10-15% Umsatzsteigerung** durch vollstaendigere Erfassung. Bei einem Praxisumsatz von 500.000 EUR/Jahr sind das 50.000-75.000 EUR zusaetzlich – allein durch bessere Dokumentation.

### 9.2.5 Digitale Anamnese und Aufklaerung

| Loesung | Funktion | PVS-Integration |
|---------|----------|----------------|
| **Nelly** | Digitale Anamnese, DSGVO-konforme Einwilligung, automatischer Import ins PVS | Charly, weitere |
| **Athena (Dampsoft)** | Digitale Anamnese und Aufklaerung | DS-Win, DS4 |
| **Idana** | Digitale Anamnese + 2.000+ Thieme-Aufklaerungsboegen + Formulare | Div. PVS |
| **Roger** | Digitale Anamnese via Smartphone | Fast alle PVS |

**Rechtlicher Rahmen:** Digitale Anamnese ist zulaessig, solange sie denselben Anforderungen wie Papierformulare genuegt (vollstaendige Dokumentation, nachvollziehbare Speicherung, jederzeitige Abrufbarkeit). Patienten duerfen nicht gezwungen werden – eine Papier-Alternative muss bleiben.

### 9.2.6 KI-gestuetzte Roentgendiagnostik

| Loesung | Herkunft | Zulassung | Funktionen | Kosten (ca.) |
|---------|----------|-----------|-----------|-------------|
| **dentalXr.ai** (ehem. dentalXrai) | Berlin (Charite-Spinoff) | CE, MDR | Karies, Infektionen, Restaurationen erkennen; 5-10 Sek. Analyse; >98% Genauigkeit | k.A. (DE-Markt) |
| **Overjet** | USA | FDA (Karies + Knochenlevel) | Karies, Zahnstein, PARL, Restaurationen; quantitativer Knochenlevel; Praxis-Dashboard | 250-500 USD/Monat |
| **Pearl (Second Opinion)** | USA | FDA (2D + 3D CBCT) | Karies-Erkennung, Practice Intelligence, Precheck, Claimcheck | 250-500 USD/Monat |
| **VideaHealth** | USA | FDA | KI-Roentgenanalyse | 250-500 USD/Monat |
| **Planmeca Romexis AI** | Finnland | CE | In Planmeca-Roentgensysteme integriert | Teil des Planmeca-Oekosystems |

**ROI-Betrachtung KI-Roentgen:**
- Kosten: ~250-500 EUR/Monat = 3.000-6.000 EUR/Jahr
- Nutzen: Fruehere Karieserkennung → mehr Behandlungen; Rechtssicherheit durch Zweitmeinung; Patientenbegeisterung ("Die Patienten sind begeistert!")
- Geschaetzter Mehrwert: 10.000-30.000 EUR/Jahr durch fruehere Diagnosen

**Empfehlung fuer Max:** dentalXr.ai fuer den deutschen Markt beobachten (Charite-Qualitaet, CE-Zulassung). Ab Praxisstart KI-Roentgen als Standard einsetzen – der ROI ist klar positiv.

---

## 9.3 CAD/CAM und digitale Workflows

### 9.3.1 Chairside CAD/CAM: CEREC-System

Das CEREC-System von Dentsply Sirona ist der Goldstandard fuer chairside Zahnersatzfertigung (Krone, Inlay, Onlay, Veneer in einer Sitzung).

**Komponenten des aktuellen Systems:**

| Komponente | Funktion | Besonderheit |
|-----------|----------|-------------|
| **Primescan 2** | Intraoralscanner (kabellos) | Neueste Generation; Cloud-basiert via DS Core |
| **CEREC Primemill** | Schleif-/Fraeseinheit (nass/trocken) | Composite-Krone in ~4 Min, Zirkon-Krone in ~5 Min |
| **CEREC Speedfire** | Sinterofen (fuer Zirkon) | Schnellsintern fuer chairside Zirkon |
| **CEREC SW / DS Core** | Planungssoftware | Cloud-basiert, geraeteunabhaengig |

**Investitionskosten (2025):**

| Position | Kosten (geschaetzt) |
|----------|-------------------|
| Komplettsystem (Primescan AC + Primemill + Speedfire) | ~120.000-180.000 EUR |
| Monatliches Leasing (inkl. Wartung) | ~2.050-2.350 EUR/Monat |
| Leasingdauer typisch | 60-72 Monate |
| Materialkosten pro Einheit | ~15-50 EUR (je nach Material) |

**ROI-Rechnung (vereinfacht):**

| Faktor | Wert |
|--------|------|
| Monatliche Kosten (Leasing + Material) | ~2.500-3.000 EUR |
| Chairside-Kronen pro Monat (konservativ) | 15-20 Stueck |
| Zusatzertrag pro Krone vs. Labor | ~150-250 EUR (Laborkosten-Ersparnis + hoehere Patientenakzeptanz) |
| Monatlicher Zusatzertrag | ~2.250-5.000 EUR |
| **Break-Even** | **Ab ~12-15 Kronen/Monat** |

**Was Max waehrend des Studiums lernen sollte:**
- CEREC-Kurse besuchen (Dentsply Sirona bietet Fortbildungen an)
- Digitale Abformung mit Intraoralscanner ueben
- CAD-Design-Grundlagen (CEREC SW ist intuitiv, aber Uebung ist noetig)
- Materialwissen: Welche Keramik/Composite fuer welche Indikation?

### 9.3.2 Alternative Intraoralscanner

| Scanner | Hersteller | Besonderheit | Preis (ca.) |
|---------|-----------|-------------|------------|
| **Primescan 2** | Dentsply Sirona | Kabellos, CEREC-Integration | Im CEREC-System enthalten |
| **TRIOS 5** | 3Shape | Offenes System, breite Kompatibilitaet | ~30.000-40.000 EUR |
| **Medit i900** | Medit | Sehr gutes Preis-Leistungs-Verhaeltnis, VDDS-Integration | ~15.000-20.000 EUR |
| **iTero Element 5D+** | Align Technology | Invisalign-Integration, NIRI-Technologie | ~35.000-45.000 EUR |

**Empfehlung:** Fuer Max ist ein offenes System (3Shape TRIOS oder Medit) sinnvoller als CEREC-Lock-in, WENN er nicht chairside fertigen will. Falls chairside → CEREC ist das einzige vollstaendig integrierte System.

### 9.3.3 3D-Druck in der Zahnarztpraxis

**Technologien:** SLA (Stereolithografie), DLP (Digital Light Processing), MSLA (Masked SLA)

**Anwendungen:**

| Anwendung | Druckzeit | Materialkosten | Sonst via Labor |
|-----------|----------|---------------|----------------|
| Bohrschablonen (Chirurgie/Implantologie) | 30-60 Min | ~5-10 EUR | ~50-100 EUR |
| Schienen (Knirscherschiene, Retainer) | 1-2 Std | ~10-20 EUR | ~50-150 EUR |
| Modelle (Studienmodelle, Implantatmodelle) | 1-3 Std | ~5-15 EUR | ~30-60 EUR |
| Provisorien (Kronen, Bruecken) | 30-60 Min | ~10-20 EUR | ~40-80 EUR |
| Totalprothesen | 3-6 Std | ~30-50 EUR | ~200-400 EUR |

**Geraete-Investition (2025):**

| Kategorie | Preis | Beispielgeraete |
|-----------|------|----------------|
| Einstieg | 5.000-7.500 EUR | Formlabs Form 3B+ |
| Mittelklasse | 7.500-15.000 EUR | Formlabs Form 4B, SprintRay Pro 2 |
| High-End | 15.000-50.000 EUR | Ackuretta, 3D Systems NextDent |
| + Nachbearbeitung (Wash + Cure) | 2.000-5.000 EUR | Formlabs Wash + Cure |

**ROI-Beispiel 3D-Druck (Formlabs Form 4B):**

| Position | Wert |
|----------|------|
| Investition (Drucker + Zubehoer) | ~10.000-12.000 EUR |
| Bohrschablonen/Monat | 10 Stueck x 40 EUR Ersparnis = 400 EUR |
| Schienen/Monat | 15 Stueck x 80 EUR Ersparnis = 1.200 EUR |
| Modelle/Monat | 20 Stueck x 30 EUR Ersparnis = 600 EUR |
| **Monatliche Ersparnis** | **~2.200 EUR** |
| **Amortisation** | **~5-6 Monate** |

**Besonders relevant fuer Max + Alex:** Bohrschablonen fuer navigierte Implantologie koennen direkt in der Praxis gedruckt werden → schnellerer Workflow, geringere Kosten, hoehere Flexibilitaet.

---

## 9.4 Navigierte Implantologie

### 9.4.1 Warum navigierte Implantologie fuer Max + Alex entscheidend ist

Alex wird MKG-Chirurg – Implantologie ist sein Kerngeschaeft. Navigierte (computergestuetzte) Implantologie ist der moderne Standard und bietet:
- Hoehere Praezision als Freihand-OP
- Bessere Planbarkeit des prothetischen Ergebnisses (Backward-Planning)
- Kuerzere OP-Zeiten
- Geringeres Komplikationsrisiko
- Bessere Patientenkommunikation durch 3D-Visualisierung

### 9.4.2 Digitaler Implantologie-Workflow

```
DVT/CBCT-Scan → Intraoralerscan → Virtuelle Planung → Bohrschablone → OP → Prothetik
     ↓              ↓                    ↓                   ↓            ↓        ↓
  DICOM-Daten    STL-Daten      coDiagnostiX o.ae.     3D-Druck     Navigation  CAD/CAM
```

**Schritt-fuer-Schritt:**

1. **Diagnostik:** DVT/CBCT-Aufnahme (DICOM-Daten) + Intraoralscan (STL-Daten)
2. **Virtuelle Planung:** Import in Planungssoftware → Implantate virtuell positionieren unter Beruecksichtigung von Knochenangebot, Nervenverlaeufen, prothetischem Ziel
3. **Bohrschablonen-Design:** Software generiert Bohrschablone → Export fuer 3D-Druck
4. **3D-Druck:** Bohrschablone in der Praxis drucken (30-60 Min, ~5-10 EUR Material)
5. **Chirurgie:** Schablonengefuehrte Implantation (Alex)
6. **Prothetik:** CAD/CAM-basierte Versorgung (Max oder Labor)

### 9.4.3 Software-Tools fuer navigierte Implantologie

| Software | Hersteller | Besonderheiten | Kosten |
|----------|-----------|----------------|--------|
| **coDiagnostiX** | Straumann/Dental Wings | Marktfuehrer; offene Architektur; KI-gestuetzte Zahnextraktion; alle gaengigen Implantatsysteme | Abo-Modell (Dongle-frei) |
| **Implant Studio** | 3Shape | Integration mit TRIOS-Scanner; intuitives UI | Teil des 3Shape-Oekosystems |
| **DTX Studio Implant** | Nobel Biocare | Enge Integration mit Nobel-Implantaten | Teil des Nobel-Oekosystems |
| **BlueSkyPlan** | Blue Sky Bio | Open-Source-Alternative; kostenlos fuer Planung | Kostenlos (Basisversion) |
| **Romexis Smile Design** | Planmeca | Integration mit Planmeca-Roentgen | Teil des Planmeca-Oekosystems |

### 9.4.4 Zusammenspiel Max (Zahnarzt) + Alex (MKG-Chirurg)

| Phase | Wer | Was | Digital-Tool |
|-------|-----|-----|-------------|
| Erstbefund + Planung | Max | Patientengespraech, Scan, HKP | PVS + Intraoralscanner |
| Implantatsplanung | Max + Alex | Gemeinsame virtuelle Planung | coDiagnostiX (Bildschirm-Sharing oder gemeinsamer Zugang) |
| Bohrschablone | Max | Design + 3D-Druck | coDiagnostiX → 3D-Drucker |
| Chirurgie | Alex | Schablonengefuehrte Implantation | Bohrschablone + ggf. Navigation |
| Prothetik | Max | CAD/CAM-Versorgung | CEREC oder Labor |
| Nachsorge | Max | Kontrolle, Recall | PVS + Recall-System |

**Vorteil der Duo-Praxis:** Der gesamte Workflow von Planung bis Prothetik findet unter einem Dach statt. Kein Ueberweisungsverlust, keine Kommunikationsprobleme zwischen Chirurg und Prothetiker, ein einheitliches digitales System.

### 9.4.5 Lernkurve und Vorbereitung

- **Waehrend des Studiums:** Grundlagen der Implantatplanung in Implantologie-Kursen; coDiagnostiX-Demozugang nutzen; 3D-Anatomie-Verstaendnis aufbauen
- **Fortbildungen:** Curriculum Implantologie (DGI); Guided Surgery Workshops
- **Kosten fuer Praxis-Setup:** coDiagnostiX-Lizenz + 3D-Drucker + DVT = ~50.000-100.000 EUR (DVT ist der groesste Posten mit ~60.000-120.000 EUR)

---

## 9.5 Dental-Tech-Startup-Szene (DACH)

### 9.5.1 Aktive Startups und Scale-ups

| Startup | Standort | Bereich | Status | Finanzierung |
|---------|---------|---------|--------|-------------|
| **Sonia** | Hamburg | KI-Sprachdokumentation + Abrechnung | Aktiv, wachsend | 12 Mio. EUR Seed (UVC Partners, Lucid Capital, Blue Lion) |
| **Dentero** | Deutschland | KI-Dokumentation + Abrechnung | In teemer integriert | k.A. |
| **Doctos** | Deutschland | KI-Transkription + Abrechnung | Aktiv | k.A. |
| **Dentiscribe** | Deutschland | KI-Dokumentation + Abrechnung | Aktiv | k.A. |
| **dentalXr.ai** | Berlin | KI-Roentgendiagnostik (Charite-Spinoff) | Aktiv | k.A. |
| **Nelly** | Deutschland | Digitale Patientenreise (Anamnese, Payment, Kommunikation) | Aktiv, wachsend | k.A. |
| **teemer** | Deutschland | Cloud-PVS | Aktiv (ARZ.dent-Gruppe) | Konzernintern |
| **Roger** | Deutschland | Praxisautomatisierung (Add-on) | Aktiv | k.A. |
| **PlusDental** | Berlin | Aligner/Digitale Kieferorthopaedie | Aktiv | 35 Mio. EUR |
| **Dr. Flex** | Deutschland | Online-Terminbuchung | Aktiv | k.A. |

### 9.5.2 Investmentlandschaft DACH Dental-Tech

Der DACH-Venture-Capital-Markt verzeichnete 2024/2025 insgesamt ~2.049 Finanzierungsrunden mit 12,1 Mrd. USD Volumen. Dental-Tech ist ein Nischensegment, aber mit steigendem Interesse:

**Trends:**
- **KI-Dokumentation:** Heissester Bereich – Sonia (12 Mio.), mehrere Wettbewerber
- **Cloud-PVS:** Langsamer Wandel von On-Premise zu Cloud
- **Patientenreise-Digitalisierung:** Nelly, Roger – digitale Anamnese bis Payment
- **KI-Diagnostik:** Roentgen-KI mit CE-Zulassung gewinnt an Traktion

**Was fehlt im Markt (Lueckenanalyse):**

| Luecke | Beschreibung | Chance |
|--------|-------------|--------|
| **Offene PVS-API** | Kein deutsches PVS bietet eine echte REST-API fuer Drittentwickler | Riesig – wer die "Shopify fuer Zahnaerzte"-Plattform baut, gewinnt |
| **Integriertes Praxis-Dashboard** | Kein System liefert Echtzeit-KPIs auf einen Blick | Hoch – BI-Tool speziell fuer Zahnaerzte |
| **Patienten-App (B2C)** | Keine ueberzeugende Patienten-App mit Bonusheft, Termine, Befunde | Mittel – regulatorisch komplex |
| **Cross-Praxis-Benchmarking** | Anonymer Leistungsvergleich zwischen Praxen | Hoch – "Glassdoor fuer Zahnarztpraxen" |
| **Automatisiertes QM** | Qualitaetsmanagement ist Pflicht, aber manuell und nervig | Mittel – regulatorisch eng |
| **Labor-Praxis-Schnittstelle** | eLABZ ist ein Anfang, aber der Workflow ist noch fragmentiert | Mittel |

### 9.5.3 Investment-Optionen fuer Max

Max koennte waehrend des Studiums als Angel-Investor in Dental-Tech investieren:

**Vorteile:**
- Domain-Expertise als angehender Zahnarzt + Tech-Background
- Fruehe Marktkenntnis und Netzwerk
- Potenziell hochattraktive Returns in einem unterdurchdrungenen Markt

**Risiken:**
- Kapital ist waehrend des Studiums begrenzt
- Dental-Tech ist ein langsamer Markt (lange Vertriebszyklen, regulatorische Huerden)

**Konkrete Moeglichkeiten:**
- An Dental-Tech-Meetups teilnehmen (IDS Koeln alle 2 Jahre, DMEA Berlin, Health-i Conference)
- Kontakt zu UVC Partners, Lucid Capital (Sonia-Investoren) aufbauen
- Eigene Side-Projects als Proof-of-Concept fuer groessere Ventures nutzen

---

## 9.6 Eigene Software-Tools: Was Max selbst bauen kann

### 9.6.1 Identifizierte Luecken und Entwicklungsideen

Max hat als ehemaliger Software-Unternehmer die seltene Kombination aus Tech-Skills und (bald) zahnmedizinischem Domain-Wissen. Das ist ein massiver Wettbewerbsvorteil.

#### Idee 1: Praxis-Dashboard (KPI-Cockpit)

**Problem:** Kein PVS liefert Echtzeit-KPIs. Praxisinhaber muessen Zahlen manuell zusammensuchen oder teure Berater engagieren.

**Loesung:** Web-basiertes Dashboard, das sich an das PVS anbindet (via VDDS-Schnittstelle oder Datenbank-Zugriff) und Echtzeit-KPIs anzeigt.

**Features:**
- Tagesumsatz (BEMA + GOZ + Privat), Wochenverlauf, Monatstrend
- Auslastung pro Behandler und Stuhl
- HKP-Annahmequote und offene HKPs
- Recall-Compliance-Rate
- Neupatienten vs. Bestandspatienten
- Durchschnittlicher Umsatz pro Patient
- Materialverbrauch und -kosten
- Personalkosten-Quote

**Technologie:** Next.js Frontend, Python/Node Backend, Datenbankanbindung an PVS

**Vermarktung:** Erst intern nutzen, dann als SaaS fuer andere Praxen anbieten. Einstieg: 49-99 EUR/Monat/Praxis.

**Aufwand:** MVP in 2-3 Monaten Teilzeit; groesste Huerde ist die PVS-Anbindung (VDDS-Schnittstelle implementieren).

#### Idee 2: Intelligentes Recall-System

**Problem:** Bestehende Recall-Systeme sind "dumm" – feste Intervalle, gleiche Nachrichten fuer alle.

**Loesung:** KI-gestuetztes Recall-System mit personalisierten Intervallen und Nachrichten.

**Features:**
- Risikoprofilbasierte Intervalle (Paro-Patienten alle 3 Monate, Low-Risk alle 6-12 Monate)
- A/B-Testing von Nachrichtentexten
- Multi-Channel-Kaskade (WhatsApp → SMS → E-Mail → Brief)
- Automatische Terminvorschlaege basierend auf Praxiskalender
- Churn-Prediction: Welche Patienten drohen abzuwandern?
- Response-Rate-Analytics

**Technologie:** WhatsApp Business API, Twilio (SMS), PVS-Anbindung, einfaches ML-Modell

**Aufwand:** MVP in 1-2 Monaten; WhatsApp Business API ist der technisch anspruchsvollste Teil.

#### Idee 3: Patienten-PWA (Progressive Web App)

**Problem:** Patienten interagieren mit der Praxis nur telefonisch oder vor Ort. Kein digitaler Touchpoint.

**Loesung:** PWA (keine App-Store-Abhaengigkeit), die Patienten auf dem Smartphone nutzen.

**Features:**
- Online-Terminbuchung und -aenderung
- Digitales Bonusheft (automatisch aktualisiert)
- Behandlungsplaene einsehen und digital akzeptieren
- Rechnungen und Dokumente
- Recall-Erinnerungen als Push-Notification
- Praxis-News und Gesundheitstipps

**Technologie:** React/Next.js PWA, Firebase Push, PVS-Anbindung

**Aufwand:** MVP in 3-4 Monaten; groesste Huerde: PVS-Anbindung und Datenschutz (Patientendaten!).

#### Idee 4: Automatisiertes QM-System

**Problem:** Qualitaetsmanagement ist gesetzlich vorgeschrieben (QM-Richtlinie des G-BA), aber extrem manuell und zeitaufwaendig.

**Loesung:** Digitales QM-System, das Pflichtdokumentation automatisiert.

**Features:**
- Digitale Checklisten fuer taegliche/woechentliche/monatliche QM-Aufgaben
- Automatische Erinnerungen an faellige Pruefungen (Hygiene, Geraetewartung)
- Dokumentenmanagement fuer SOPs, Arbeitsanweisungen, Schulungsnachweise
- Audit-Trail fuer Praxisbegehungen
- Automatische Generierung des QM-Handbuchs

**Technologie:** Web-App mit Checklisten-Engine, PDF-Generator, Erinnerungssystem

**Aufwand:** MVP in 2-3 Monaten; relativ wenig technische Komplexitaet, aber viel Domain-Wissen noetig.

#### Idee 5: PVS-Middleware / API-Layer

**Problem:** PVS-Systeme sind geschlossene Silos ohne offene APIs. Jede Integration ist eine Einzelloesung.

**Loesung:** Middleware, die sich zwischen PVS und Drittanbieter-Tools setzt und eine standardisierte API bereitstellt.

**Features:**
- Liest Daten aus dem PVS (via VDDS-Schnittstelle oder Datenbank-Zugriff)
- Stellt REST-API bereit fuer: Patienten, Termine, Behandlungen, Rechnungen
- Ermoeglicht Drittentwicklern, Apps zu bauen
- Webhooks fuer Echtzeit-Events (neuer Patient, neuer Termin, neue Rechnung)

**Technologie:** Node.js/Python API-Server, VDDS-Adapter, Datenbank-Connector

**Aufwand:** 4-6 Monate fuer ein PVS; jedes weitere PVS = 2-3 Monate. Groesste Huerde: Reverse-Engineering der PVS-Datenbanken.

**Potenzial:** Dies waere die "Plaid fuer Dental" – eine Plattform, auf der andere Entwickler aufbauen koennen. Enormes Potenzial, wenn es gelingt.

### 9.6.2 Priorisierte Entwicklungs-Roadmap

| Prioritaet | Tool | Aufwand | Impact | Wann starten |
|-----------|------|---------|--------|-------------|
| 1 | Praxis-Dashboard (KPI) | 2-3 Monate | Hoch (intern + SaaS) | Semester 5-6 (wenn PVS-Erfahrung vorhanden) |
| 2 | Intelligentes Recall-System | 1-2 Monate | Hoch (Umsatzsteigerung) | Semester 7-8 |
| 3 | Patienten-PWA | 3-4 Monate | Mittel (Differenzierung) | Semester 8-10 |
| 4 | Automatisiertes QM | 2-3 Monate | Mittel (Zeitersparnis) | Nach Praxisstart |
| 5 | PVS-Middleware | 4-6 Monate | Sehr hoch (Plattform) | Nach Praxisstart + Validierung |

### 9.6.3 Build vs. Buy Entscheidungsmatrix

| Funktion | Kaufen (Tool) | Selbst bauen | Empfehlung |
|----------|-------------|-------------|-----------|
| PVS (Kernverwaltung) | teemer, Charly-Web | Unrealistisch (zu komplex, regulatorisch) | **Kaufen** |
| Online-Termine | Doctolib, Dr. Flex | Machbar, aber Plattform-Effekt fehlt | **Kaufen + eigene Buchung** |
| Recall | Roger | Besser individuell loesbar | **Selbst bauen** |
| KI-Roentgen | dentalXr.ai, Overjet | Unrealistisch (ML-Expertise, Zulassung) | **Kaufen** |
| KI-Dokumentation | Sonia, Dentero | Unrealistisch (NLP, Training) | **Kaufen** |
| Dashboard/Analytics | Keiner gut genug | Machbar und differenzierend | **Selbst bauen** |
| Patienten-App | Keiner ueberzeugend | Machbar und differenzierend | **Selbst bauen** |
| QM-System | Div. generische Loesungen | Machbar | **Selbst bauen** (wenn Zeit) |
| CAD/CAM | CEREC, 3Shape | Unrealistisch | **Kaufen** |

---

## 9.7 Daten und Analytics

### 9.7.1 Warum Max einen unfairen Vorteil hat

Die durchschnittliche Zahnarztpraxis nutzt ihre Daten kaum. Praxissoftware generiert taeglich Hunderte Datenpunkte, die nie analysiert werden. Max kann mit seinem Tech-Background:

1. **Daten systematisch erfassen** (strukturierte Dokumentation von Anfang an)
2. **Daten auswerten** (eigene Dashboards statt Excel)
3. **Daten nutzen** (datengetriebene Entscheidungen statt Bauchgefuehl)

### 9.7.2 KPI-Framework fuer eine datengetriebene Zahnarztpraxis

#### Finanzielle KPIs

| KPI | Definition | Zielwert | Frequenz |
|-----|-----------|---------|----------|
| Tagesumsatz (brutto) | Gesamtumsatz pro Tag (BEMA + GOZ + Privat) | >2.000 EUR/Behandler/Tag | Taeglich |
| Umsatz pro Patient | Durchschnittlicher Umsatz pro Patientenbesuch | >150-200 EUR | Monatlich |
| Privatanteil | Anteil GOZ/Privat am Gesamtumsatz | >40-50% | Monatlich |
| HKP-Annahmequote | Anteil akzeptierter Heil- und Kostenplaene | >70% | Monatlich |
| Materialkosten-Quote | Materialkosten / Umsatz | <7-10% | Monatlich |
| Personalkosten-Quote | Personalkosten / Umsatz | <25-30% | Monatlich |
| Praxisgewinn-Marge | Gewinn / Umsatz | >30-40% | Quartalsweise |

#### Operative KPIs

| KPI | Definition | Zielwert | Frequenz |
|-----|-----------|---------|----------|
| Auslastung | Anteil belegter Behandlungszeit | >85% | Taeglich |
| No-Show-Rate | Anteil nicht wahrgenommener Termine | <5% | Woechentlich |
| Wartezeit (Patient) | Durchschnittliche Wartezeit im Wartezimmer | <10 Min | Taeglich |
| Behandlungszeit vs. Plan | Ist- vs. Soll-Behandlungszeit | +/- 10% | Woechentlich |
| Neupatienten/Monat | Anzahl erstmalig behandelter Patienten | 30-50 | Monatlich |
| Recall-Compliance | Anteil Patienten, die zum Recall kommen | >70% | Monatlich |

#### Qualitaets-KPIs

| KPI | Definition | Zielwert | Frequenz |
|-----|-----------|---------|----------|
| Reklamationsquote | Anteil nachzubessernder Arbeiten | <3% | Monatlich |
| Patientenzufriedenheit | NPS oder aehnliches Mass | >50 NPS | Quartalsweise |
| Bewertung (Google/Jameda) | Durchschnittliche Online-Bewertung | >4,5 Sterne | Laufend |
| Weiterempfehlungsquote | Anteil Neupatienten durch Empfehlung | >30% | Monatlich |

### 9.7.3 Predictive Analytics: Konkrete Anwendungsfaelle

| Anwendungsfall | Datenquellen | Methode | Nutzen |
|---------------|-------------|---------|--------|
| **Churn-Prediction** | Terminhistorie, Zahlungsverhalten, Recall-Compliance | Logistische Regression / Random Forest | Fruehwarnung bei abwanderungsgefaehrdeten Patienten → gezielte Ansprache |
| **No-Show-Prediction** | Historische No-Shows, Wochentag, Uhrzeit, Patientenprofil | Gradient Boosting | Ueberbuchung bei hohem Risiko, SMS-Erinnerung verdoppeln |
| **Umsatz-Forecasting** | Historische Umsaetze, saisonale Muster, Terminbuchungen | Zeitreihenanalyse (Prophet) | Liquiditaetsplanung, Personalplanung |
| **Behandlungsplan-Optimierung** | Diagnosen, Behandlungshistorie, Erfolgsraten | Entscheidungsbaeume | Optimale Behandlungssequenz vorschlagen |
| **Personalbedarfs-Prediction** | Terminkalender, historische Auslastung, Krankheitstage | Regressionsmodelle | Optimale Schichtplanung |

### 9.7.4 Technologie-Stack fuer Praxis-Analytics

| Schicht | Tool | Warum |
|---------|------|-------|
| **Datenquelle** | PVS (via VDDS/DB), Buchhaltung (DATEV), Online-Bewertungen | Primaerdaten |
| **ETL / Daten-Pipeline** | Python (pandas, SQLAlchemy) oder dbt | Datenaufbereitung |
| **Datenbank** | PostgreSQL oder BigQuery (Cloud) | Strukturierte Speicherung |
| **Analytics / ML** | Python (scikit-learn, Prophet, XGBoost) | Modelle und Analysen |
| **Visualisierung** | Eigenes Dashboard (React + D3.js) oder Metabase/Superset | KPI-Anzeige |
| **Alerting** | Eigene Logik (Slack/E-Mail bei Schwellwerten) | Proaktive Benachrichtigung |

### 9.7.5 Datenschutz und Compliance

Jede Datenanalyse in der Zahnarztpraxis muss folgende Regeln beachten:

- **DSGVO:** Patientendaten sind besonders schuetzenswerte Gesundheitsdaten (Art. 9 DSGVO)
- **Aerztliche Schweigepflicht:** Paragraph 203 StGB – Verletzung ist strafbar
- **Pseudonymisierung:** Fuer Analytics muessen Daten pseudonymisiert werden
- **Aufbewahrungspflichten:** 10 Jahre Aufbewahrung (Paragraph 630f BGB)
- **Keine Cloud-Analyse ohne Auftragsverarbeitungsvertrag (AVV)**
- **Patienteneinwilligung:** Fuer erweiterte Analysen (ueber Behandlungszweck hinaus) ist eine Einwilligung noetig

**Empfehlung:** Alle Analytics lokal oder in einer deutschen Cloud (DSGVO-konform) betreiben. Keine Patientendaten in US-Cloud-Dienste.

---

## 9.8 Gesamtstrategie: Technologie-Fahrplan

### Phase 1: Studium (Semester 1-4) – Wissen aufbauen

| Aktion | Zeitpunkt | Aufwand |
|--------|----------|---------|
| PVS-Demos anschauen (teemer, Charly, Dampsoft) | Semester 1-2 | Wenige Stunden |
| VDDS-Schnittstellenspezifikation lesen | Semester 2 | 1 Tag |
| CEREC-Einsteigerkurs besuchen | Semester 3-4 | 1-2 Tage |
| 3D-Druck-Grundlagen (Formlabs/Prusa) | Semester 2-3 | Privat testen |
| coDiagnostiX Demozugang + Tutorials | Semester 3-4 | Wenige Stunden |
| Dental-Tech-Startups verfolgen (Newsletter, LinkedIn) | Laufend | 1h/Woche |

### Phase 2: Studium (Semester 5-8) – Erste Tools bauen

| Aktion | Zeitpunkt | Aufwand |
|--------|----------|---------|
| KPI-Dashboard MVP entwickeln | Semester 5-6 | 2-3 Monate Teilzeit |
| Recall-System MVP entwickeln | Semester 7-8 | 1-2 Monate Teilzeit |
| Hospitationen in digitalisierten Praxen | Semester 5-7 | 2-3 Hospitationen |
| CEREC-Anwenderkurs (Fortgeschritten) | Semester 6 | 2 Tage |
| IDS Koeln besuchen (wenn im Turnus) | Alle 2 Jahre | 2 Tage |

### Phase 3: Studium (Semester 9-10) – Praxisvorbereitung

| Aktion | Zeitpunkt | Aufwand |
|--------|----------|---------|
| PVS-Entscheidung treffen | Semester 9 | Evaluierung |
| Patienten-PWA MVP entwickeln | Semester 9-10 | 3-4 Monate Teilzeit |
| Tech-Stack fuer die Praxis definieren | Semester 9 | 1-2 Wochen |
| Geraetebeschaffung planen (Scanner, 3D-Drucker, ggf. CEREC) | Semester 10 | Angebote einholen |

### Phase 4: Praxisstart (Jahr 1-2) – Implementieren und skalieren

| Aktion | Zeitpunkt | Aufwand |
|--------|----------|---------|
| PVS einrichten + alle Integrationen | Monat 1-3 | Intensiv |
| KI-Tools aktivieren (Roentgen, Dokumentation) | Monat 1-3 | Setup + Training |
| Dashboard live schalten | Monat 3-6 | Feintuning |
| Recall-System live schalten | Monat 3-6 | Feintuning |
| Patienten-PWA launchen | Monat 6-12 | Beta-Phase |
| Daten-Analytics aufsetzen | Monat 6-12 | Iterativ |
| PVS-Middleware evaluieren (als SaaS-Produkt?) | Jahr 2 | Strategische Entscheidung |

### Geschaetzte Technologie-Investitionen zum Praxisstart

| Kategorie | Investition | Monatliche Kosten |
|-----------|-----------|-------------------|
| PVS (teemer oder Charly-Web) | 5.000-10.000 EUR (Setup) | 300-600 EUR |
| Intraoralscanner (Medit i900 oder Primescan) | 15.000-40.000 EUR | – |
| CEREC Komplettsystem (optional) | 120.000-180.000 EUR (oder Leasing) | 2.050-2.350 EUR |
| 3D-Drucker (Formlabs Form 4B + Zubehoer) | 10.000-15.000 EUR | ~200 EUR (Material) |
| DVT/CBCT (fuer Alex' Implantologie) | 60.000-120.000 EUR | – |
| KI-Roentgen (dentalXr.ai) | – | 250-500 EUR |
| KI-Dokumentation (Sonia oder Dentero) | – | 200-500 EUR |
| Roger oder aehnliches Add-on | – | 129-199 EUR/Behandler |
| Doctolib/Jameda | – | 99-139 EUR/Behandler |
| Eigene Tools (Dashboard, Recall, PWA) | Eigenleistung | ~50 EUR (Hosting) |
| IT-Infrastruktur (Server, Netzwerk, TI) | 10.000-20.000 EUR | 200-400 EUR |
| **Gesamt (ohne CEREC)** | **~100.000-225.000 EUR** | **~1.500-3.000 EUR/Monat** |
| **Gesamt (mit CEREC)** | **~220.000-405.000 EUR** | **~3.500-5.500 EUR/Monat** |

---

## 9.9 Zusammenfassung: Max' Tech-Wettbewerbsvorteil

Max hat eine einzigartige Position im Zahnarztmarkt:

1. **Er versteht Software** – waehrend 99% der Zahnaerzte Anwender sind, kann Max Systeme evaluieren, integrieren und selbst bauen.

2. **Er kann Luecken schliessen** – die groessten Luecken im Dental-Tech-Markt (offene APIs, intelligentes Analytics, Patienten-Apps) sind genau die Dinge, die ein Software-Unternehmer bauen kann.

3. **Er hat einen eingebauten Testmarkt** – die eigene Praxis ist das perfekte Testlabor fuer eigene Tools, bevor sie fuer andere Praxen vermarktet werden.

4. **Das Timing stimmt** – der Dental-Tech-Markt ist im Umbruch (Cloud, KI, Automatisierung). Wer jetzt einsteigt, kann Standards setzen.

5. **Die Duo-Praxis mit Alex potenziert den Vorteil** – navigierte Implantologie + digitale Workflows + eigene Software-Tools = eine Praxis, die technologisch 10 Jahre voraus ist.

**Der strategische Imperativ:** Max sollte die 5 Studienjahre nicht nur fuer die zahnmedizinische Ausbildung nutzen, sondern parallel seinen Tech-Vorteil systematisch in konkrete Tools, Netzwerke und ggf. ein Dental-Tech-Side-Business uebersetzen. Das unterscheidet ihn fundamental von jedem anderen Berufseinsteiger.
