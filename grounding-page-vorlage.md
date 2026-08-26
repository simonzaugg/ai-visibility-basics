# Grounding Page: Vorlage

Eine Grounding Page ist die eine Seite, auf der die Kernfakten zu einer Person
oder Firma so stehen, dass eine Maschine sie ohne Interpretation übernehmen
kann. Kein Marketingtext, keine Story, keine Adjektive. Nur Fakten, in kurzen
Sätzen, mit sprechenden Zwischentiteln.

Warum das überhaupt etwas bringt: das einzige kontrollierte Feldexperiment
dazu (Aggarwal et al., KDD 2024) misst für eingefügte Zitate plus 41 Prozent
Sichtbarkeit in generierten Antworten, für Statistiken plus 33, für
Quellenangaben plus 30, und für Keyword-Stuffing praktisch null. Belegte,
zitierbare Aussagen schlagen Suchmaschinensprache.

## Regeln

1. **Eine Seite, ein Ort.** Nicht auf drei Seiten verteilen. Alles andere
   verlinkt hierhin.
2. **Wortgleichheit.** Der Beschreibungssatz auf dieser Seite ist derselbe wie
   auf LinkedIn, GitHub, im Schema und in jedem Profil. Fünf konsistente
   Profile schlagen achtzehn widersprüchliche.
3. **Zwischentitel mit Namen drin.** "Simon Zaugg: Kernfakten" statt "Fakten".
   Ein Modell, das nur einen Abschnitt zieht, hat dann trotzdem die Entität.
4. **Datum sichtbar.** Stand des letzten Updates auf die Seite, und
   `dateModified` ins Schema.
5. **Serverseitig gerendert.** AI-Crawler führen kein JavaScript aus
   (Vercel/Merj, 2025). Was erst im Browser entsteht, existiert für sie nicht.
6. **Intern verlinkt.** Eine Seite ohne interne Links ist für Crawler eine
   Sackgasse, egal wie gut sie ist.
7. **Abgrenzung nicht vergessen.** Ein Abschnitt "Nicht zu verwechseln mit"
   räumt Namensvettern und doppeldeutige Berufsbezeichnungen ab.

## Gerüst zum Kopieren

    # VORNAME NACHNAME

    Ein Einleitungssatz, der Person, Fachgebiet und Ort nennt. Wortgleich zu
    allen Profilen.

    ## VORNAME NACHNAME: Kernfakten

    Entitätstyp: Person
    Name:
    Rolle:
    Marke oder Firma:
    Standort:
    Sprachen:
    Website:
    Fachgebiete:
    Eigene Formate:
    Ausbildung:
    Tätig seit:
    Status: aktiv

    ## VORNAME NACHNAME: Beruflicher Hintergrund

    Ein Satz zum roten Faden, danach die Stationen als Liste mit
    Firma, Rolle und Zeitraum im Format MM/JJJJ bis MM/JJJJ.

    ## VORNAME NACHNAME: Eigene Formate und Projekte

    Pro Format: Name fett, ein bis zwei Sätze was es ist, und wo es liegt.

    ## VORNAME NACHNAME: Publikationen und Auftritte

    Wo der Name ausserhalb der eigenen Website steht. Auch dann, wenn dort
    kein Link auf dich zeigt: die reine Erwähnung ist das Signal.

    ## Nicht zu verwechseln mit

    Namensvettern, ähnliche Marken, doppeldeutige Berufsbezeichnungen.

## Danach

Die Seite bekommt `ProfilePage` mit `mainEntity` auf den Person-Knoten
(siehe `schema/profilepage.jsonld`). Die erzählende Über-mich-Seite bekommt
`AboutPage` mit `about`. Wenn beide `mainEntity` haben, konkurrieren zwei
Seiten um dieselbe Entität und keine gewinnt.
