# stebo-zora-bot

## Flugsuche Graz & Wien

`flugsuche/index.html` ist eine Seite, die als Claude-Artifact läuft und Live-Flugpreise über den Kiwi.com-Connector abruft.

- **Abflughafen:** Graz, Wien oder beide. Bei „Beide“ zeigt eine Tabelle für jedes Ziel, ab welchem Flughafen es günstiger ist.
- **Reise:** nur Hinflug oder Hin- und Rückflug. Bei Hin & Rück wird der Gesamtpreis für beide Flüge verglichen.
- **Reisedaten:** ein Zeitraum (Standard: die nächsten drei Monate, bei Hin & Rück mit Aufenthaltsdauer in Nächten) oder feste Hin- und Rückflugdaten mit ±0–3 Tagen Flexibilität.
- **Filter:** Budget, nur Direktflüge, nur das günstigste Angebot pro Ziel.
- **Aktualität:** Bei jedem Öffnen werden Flüge und Preise neu abgerufen. „Neu laden“ holt sie jederzeit erneut.

### Wie die Suche funktioniert

Das Kiwi.com-Tool `search-flight` liefert höchstens 15 Treffer pro Anfrage. Deshalb teilt die Seite den Zeitraum in Monatsabschnitte (höchstens 6) und fragt pro Abschnitt und Flughafen `flyTo: "anywhere"` mit `one_for_city: true` ab. Die Ergebnisse werden zusammengeführt und nach Preis sortiert.

Gabelflüge, bei denen der Rückflug in einer anderen Stadt startet oder woanders landet, werden bei Hin & Rück ausgeblendet. Budget und „günstigstes pro Ziel“ filtern die geladenen Ergebnisse sofort. „Nur Direktflüge“ geht als `max_sector_stopovers: 0` direkt an Kiwi.com.

### Veröffentlichen

Die Datei enthält nur den Seiteninhalt ohne `<html>`/`<head>`, weil das Artifact-System dieses Gerüst beim Veröffentlichen ergänzt. Das Artifact braucht die Fähigkeit `mcp` mit dem Server `Kiwi.com` und dem Tool `search-flight`. Außerhalb von Claude zeigt die Seite einen Hinweis statt Preisen.
