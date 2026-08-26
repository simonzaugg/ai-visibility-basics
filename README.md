# AI Visibility Basics

Vorlagen und eine Checkliste, damit KI-Systeme deine Firma korrekt erfassen:
robots.txt, Person- und Organization-Schema, Grounding Page.

Gedacht für kleine und mittlere Unternehmen im deutschsprachigen Raum, die
selbst Hand anlegen. Kein Tool, keine Anmeldung, nichts zu kaufen. Kopieren,
Platzhalter ersetzen, fertig.

## Was hier drin liegt

| Datei | Wofür |
|---|---|
| `robots.txt` | Vorlage mit Sitemap-Zeile, offenen Retrieval-Bots und ohne crawl-delay |
| `schema/person-organization.jsonld` | Sitewide-Graph: ein Person-Knoten, ein Organization-Knoten, ein WebSite-Knoten |
| `schema/profilepage.jsonld` | Schema für die Grounding Page, die eine Seite mit `mainEntity` |
| `schema/aboutpage.jsonld` | Schema für die erzählende Über-mich-Seite, mit `about` statt `mainEntity` |
| `grounding-page-vorlage.md` | Aufbau und Regeln für die Faktenseite, mit Gerüst zum Kopieren |

## Die Checkliste

**1. Sitemap-Zeile in die robots.txt.** Fehlt sie, erfährt ein Crawler, der
deine Search Console nicht kennt, nichts von deinen Sitemaps. Das betrifft
jeden AI-Crawler.

**2. crawl-delay raus.** Google unterstützt es laut eigener Doku nicht, es ist
nicht Teil von RFC 9309, kein grosser AI-Anbieter dokumentiert Support.

**3. Retrieval-Bots offen lassen.** `OAI-SearchBot`, `ChatGPT-User`,
`PerplexityBot`, `Perplexity-User`, `Claude-SearchBot`, `Claude-User`. Sie
holen die Seite, die ein Modell gerade zitieren will. Wer sie sperrt,
verschwindet aus der Antwort. Trainings-Crawler (`GPTBot`, `ClaudeBot`,
`CCBot`, `Google-Extended`) zu sperren bringt dagegen keinen
Sichtbarkeitsvorteil. Das ist eine Wertentscheidung, keine Marketingfrage.

**4. Genau ein Person-Knoten, sitewide ausgeliefert.** Der häufigste Fehler in
WordPress-Installationen sind zwei konkurrierende Person-Knoten: einer aus dem
SEO-Plugin, einer aus dem Autorenprofil, mit unterschiedlichen Namen. Dann
existiert die Person im eigenen Graph zweimal, also gar nicht.

**5. Autorenprofil aufräumen.** Anzeigename, Slug und Beschreibung. Ein
Autoren-Slug wie `/author/isozulap/` ist ein eigener, falscher Datenpunkt.

**6. Eine Grounding Page.** Siehe `grounding-page-vorlage.md`. Der Ort, an dem
die Kernfakten so stehen, dass eine Maschine sie ohne Interpretation
übernehmen kann.

**7. sameAs-Kette schliessen.** Jedes Profil, das dir gehört, verlinkt zurück
auf die Grounding Page, und die Grounding Page verlinkt auf jedes Profil. Nimm
nur Profile auf, die gepflegt sind. Ein leeres Profil ist ein schwächeres
Signal als gar keines.

**8. Serverseitig rendern.** AI-Crawler führen kein JavaScript aus. Was erst
im Browser entsteht, existiert für sie nicht.

**9. Nachmessen statt hoffen.** Server-Logs auf AI-Crawler filtern, Bing
Webmaster Tools ansehen, und die eigene Marke plus den eigenen Namen in
ChatGPT, Gemini, Copilot und Perplexity abfragen. Das Ergebnis vor der Arbeit
notieren, sonst hast du später keinen Vorher-Wert.

## Was bewusst nicht drin ist

**llms.txt.** Ahrefs hat im Mai 2026 137'210 Domains ausgewertet: 97 Prozent
der llms.txt-Dateien wurden in einem Monat kein einziges Mal abgerufen.
Slackbot holte sie öfter als PerplexityBot. Wer sie anlegt, sollte das als
Experiment verbuchen, nicht als Massnahme.

**FAQPage-Schema.** Google hat die FAQ-Rich-Results im Mai 2026 entfernt. Der
Inhalt in Frage-Antwort-Form bleibt wertvoll, das Markup bringt nichts mehr.

**speakable.** Seit Einführung Beta und auf News-Publisher beschränkt.

**Keyword-Stuffing.** Im einzigen kontrollierten Feldexperiment dazu (KDD 2024)
liegt der Effekt auf Sichtbarkeit in generierten Antworten bei praktisch null.

## Der ehrliche Rahmen

Diese Vorlagen sind Aufräumarbeit, keine Wachstumsmassnahme. Ahrefs misst
über 75'000 Marken für Backlinks eine Korrelation von 0.218 zur Sichtbarkeit
in AI-Antworten und für Content-Menge nahezu null, aber für Markenerwähnungen
ausserhalb der eigenen Website 0.66 bis 0.71.

Übersetzt: was dich in KI-Antworten bringt, steht grösstenteils nicht auf
deiner Website. Es steht auf anderen Websites. Diese Checkliste sorgt nur
dafür, dass die Signale von aussen auf der richtigen Entität landen und nicht
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

MIT, siehe `LICENSE`. Benutz es, ändere es, verkauf es weiter. Ein Hinweis
freut mich, nötig ist er nicht.

## Wer das gebaut hat

Simon Zaugg, Berater für AI Visibility, GEO und AEO im Raum Zürich.
Kernfakten: https://www.content-engineer.ch/fakten/
