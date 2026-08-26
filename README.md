# AI Visibility Basics

Vorlagen und eine Checkliste, damit KI-Systeme deine Firma korrekt erfassen:
robots.txt, Person- und Organization-Schema, Grounding Page.

Gedacht fuer kleine und mittlere Unternehmen im deutschsprachigen Raum, die
selbst Hand anlegen. Kein Tool, keine Anmeldung, nichts zu kaufen. Kopieren,
Platzhalter ersetzen, fertig.

## Was hier drin liegt

| Datei | Wofuer |
|---|---|
| `robots.txt` | Vorlage mit Sitemap-Zeile, offenen Retrieval-Bots und ohne crawl-delay |
| `schema/person-organization.jsonld` | Sitewide-Graph: ein Person-Knoten, ein Organization-Knoten, ein WebSite-Knoten |
| `schema/profilepage.jsonld` | Schema fuer die Grounding Page, die eine Seite mit `mainEntity` |
| `schema/aboutpage.jsonld` | Schema fuer die erzaehlende Ueber-mich-Seite, mit `about` statt `mainEntity` |
| `grounding-page-vorlage.md` | Aufbau und Regeln fuer die Faktenseite, mit Geruest zum Kopieren |

## Die Checkliste

**1. Sitemap-Zeile in die robots.txt.** Fehlt sie, erfaehrt ein Crawler, der
deine Search Console nicht kennt, nichts von deinen Sitemaps. Das betrifft
jeden AI-Crawler.

**2. crawl-delay raus.** Google unterstuetzt es laut eigener Doku nicht, es ist
nicht Teil von RFC 9309, kein grosser AI-Anbieter dokumentiert Support.

**3. Retrieval-Bots offen lassen.** `OAI-SearchBot`, `ChatGPT-User`,
`PerplexityBot`, `Perplexity-User`, `Claude-SearchBot`, `Claude-User`. Sie
holen die Seite, die ein Modell gerade zitieren will. Wer sie sperrt,
verschwindet aus der Antwort. Trainings-Crawler (`GPTBot`, `ClaudeBot`,
`CCBot`, `Google-Extended`) zu sperren bringt dagegen keinen
Sichtbarkeitsvorteil. Das ist eine Wertentscheidung, keine Marketingfrage.

**4. Genau ein Person-Knoten, sitewide ausgeliefert.** Der haeufigste Fehler in
WordPress-Installationen sind zwei konkurrierende Person-Knoten: einer aus dem
SEO-Plugin, einer aus dem Autorenprofil, mit unterschiedlichen Namen. Dann
existiert die Person im eigenen Graph zweimal, also gar nicht.

**5. Autorenprofil aufraeumen.** Anzeigename, Slug und Beschreibung. Ein
Autoren-Slug wie `/author/isozulap/` ist ein eigener, falscher Datenpunkt.

**6. Eine Grounding Page.** Siehe `grounding-page-vorlage.md`. Der Ort, an dem
die Kernfakten so stehen, dass eine Maschine sie ohne Interpretation
uebernehmen kann.

**7. sameAs-Kette schliessen.** Jedes Profil, das dir gehoert, verlinkt zurueck
auf die Grounding Page, und die Grounding Page verlinkt auf jedes Profil. Nimm
nur Profile auf, die gepflegt sind. Ein leeres Profil ist ein schwaecheres
Signal als gar keines.

**8. Serverseitig rendern.** AI-Crawler fuehren kein JavaScript aus. Was erst
im Browser entsteht, existiert fuer sie nicht.

**9. Nachmessen statt hoffen.** Server-Logs auf AI-Crawler filtern, Bing
Webmaster Tools ansehen, und die eigene Marke plus den eigenen Namen in
ChatGPT, Gemini, Copilot und Perplexity abfragen. Das Ergebnis vor der Arbeit
notieren, sonst hast du spaeter keinen Vorher-Wert.

## Was bewusst nicht drin ist

**llms.txt.** Ahrefs hat im Mai 2026 137'210 Domains ausgewertet: 97 Prozent
der llms.txt-Dateien wurden in einem Monat kein einziges Mal abgerufen.
Slackbot holte sie oefter als PerplexityBot. Wer sie anlegt, sollte das als
Experiment verbuchen, nicht als Massnahme.

**FAQPage-Schema.** Google hat die FAQ-Rich-Results im Mai 2026 entfernt. Der
Inhalt in Frage-Antwort-Form bleibt wertvoll, das Markup bringt nichts mehr.

**speakable.** Seit Einfuehrung Beta und auf News-Publisher beschraenkt.

**Keyword-Stuffing.** Im einzigen kontrollierten Feldexperiment dazu (KDD 2024)
liegt der Effekt auf Sichtbarkeit in generierten Antworten bei praktisch null.

## Der ehrliche Rahmen

Diese Vorlagen sind Aufraeumarbeit, keine Wachstumsmassnahme. Ahrefs misst
ueber 75'000 Marken fuer Backlinks eine Korrelation von 0.218 zur Sichtbarkeit
in AI-Antworten und fuer Content-Menge nahezu null, aber fuer Markenerwaehnungen
ausserhalb der eigenen Website 0.66 bis 0.71.

Uebersetzt: was dich in KI-Antworten bringt, steht groesstenteils nicht auf
deiner Website. Es steht auf anderen Websites. Diese Checkliste sorgt nur
dafuer, dass die Signale von aussen auf der richtigen Entitaet landen und nicht
bei deinem Namensvetter. Das ist notwendig und es ist nicht hinreichend.

## Quellen

- Ahrefs, llms.txt-Logfilestudie: https://ahrefs.com/blog/llmstxt-study/
- Ahrefs, Korrelationen zu AI Overviews: https://ahrefs.com/blog/ai-overview-brand-correlation/
- Aggarwal et al., Generative Engine Optimization, KDD 2024: https://arxiv.org/abs/2311.09735
- Vercel/Merj, AI-Crawler rendern kein JavaScript: https://vercel.com/blog/the-rise-of-the-ai-crawler
- OpenAI, Bots: https://developers.openai.com/api/docs/bots
- Anthropic, Crawler: https://support.claude.com/en/articles/8896518
- Perplexity, Bots: https://docs.perplexity.ai/guides/bots
- Grounding Page Standard: https://groundingpage.com/spec/

## Lizenz

MIT, siehe `LICENSE`. Benutz es, aendere es, verkauf es weiter. Ein Hinweis
freut mich, noetig ist er nicht.

## Wer das gebaut hat

Simon Zaugg, Berater fuer AI Visibility, GEO und AEO im Raum Zuerich.
Kernfakten: https://www.content-engineer.ch/fakten/
