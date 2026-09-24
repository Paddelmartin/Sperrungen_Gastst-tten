# Spreewald-Sperrkarte

Liest täglich automatisch die Sperrungsseite des LBV Brandenburg aus und zeigt auf einer
OpenStreetMap-Karte, welche Spreewald-Gewässer aktuell gesperrt oder eingeschränkt sind.
Zusätzlich, über einen eigenen Reiter: Gaststätten in der Nähe mit Öffnungszeiten/Ruhetag.

Gehört zu: Bootsverleih Richter / Kajaksports, Lübbenau.

## Ersteinrichtung (einmalig)

1. Dieses Paket komplett in ein neues, **öffentliches** GitHub-Repository hochladen
   (Ordnerstruktur beibehalten, auch den versteckten Ordner `.github`).
2. Unter **Settings → Pages** bei „Source“ **GitHub Actions** auswählen.
3. Unter **Settings → Secrets and variables → Actions** anlegen:
   - Secret `KONTAKT` – eine allgemeine Mailadresse (Höflichkeitsangabe für OpenStreetMap-Abfragen)
   - Secret `NTFY_TOPIC` – ein langer, zufälliger Kanalname für Push-Benachrichtigungen (ntfy.sh)
4. Unter **Actions** den Workflow „Spreewald-Sperrkarte täglich“ einmal manuell starten
   („Run workflow“).
5. Danach ist die Karte erreichbar unter:
   `https://<dein-github-name>.github.io/<repository-name>/`
   Das Formular zum Erfassen von Gaststätten unter `.../erfassen.html`.

## Wichtige Dateien zum selbst Pflegen

| Datei | Zweck |
|---|---|
| `gewaesser.yaml` | Kartenposition der Wasserwege (automatisch per OpenStreetMap oder von Hand) |
| `eigene-sperrungen.yaml` | Zusätzliche Sperrungen, die nicht von der LBV kommen |
| `gaststaetten.yaml` | Kuratierte Liste der angezeigten Gaststätten (am einfachsten über `docs/erfassen.html` pflegen) |

Alle drei Dateien sind ausführlich kommentiert, mit Beispielen zum Kopieren.

## Lokal testen (optional)

```
pip install -r requirements.txt
python spreewald_sperrungen.py --html tests/fixture.html --no-osm --date 2026-09-20
cd docs && python -m http.server 8000
```

## Hinweis zu `docs/index.html` und `docs/sperrungen.json`

Diese beiden Dateien entstehen automatisch bei jedem Lauf und sind daher **nicht** in diesem
Paket enthalten (siehe `.gitignore`). Nach dem ersten Workflow-Lauf bei GitHub liegen sie
im `docs`-Ordner des Repositories.
