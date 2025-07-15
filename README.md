# bq-academy-static-code-analysis
## Ziel

Ein Testautomatisierungsprojekt mit Playwright aufsetzen und sicherstellen, dass der Code einheitlich, sauber und fehlerfrei bleibt, indem die Tools Husky, Prettier und ESLint integriert werden. Diese Tools sollen automatisch arbeiten, bevor ein Commit ins Git-Repository erfolgt.

## Setup

```
npm install
npx playwright install
```

## Prüfen der Tools Husky, Prettier und ESLint
### Fehler einbauen
Editiere die test/example.spec.ts Datei, um Fehler zu enthalten.
```
import { test, expect } from "@playwright/test"

const unused = 123    //bad comment, also unused variable

test(  "has title" , async ( {page} ) => {
    await page.goto("https://playwright.dev/")

    await expect(page).toHaveTitle(/Playwright/)
} )


test("get started link", async ({page}) => {
    await page.goto("https://playwright.dev/")

await page.getByRole("link", {name: "Get started"}).click()


await expect( page.getByRole("heading", {name: "Installation"}) ).toBeVisible()
})

```

### Versuche den Code zu comitten
```
git add .
git commit -m "trying precommit hooks"
```
### Error von Lint
Die ungenutzte Variable lässt den Commit scheitern. Kommentiere die Zeile mit der Variable aus.
### Erfolgreicher Commit mit Prettier
Wiederhole den Commit. Diesmal läuft Lint erfolgreich durch und Prettier wird auch ausgeführt. Der Commit läuft erfolgreich und könnte jetzt gepusht werden.

## Script vor Commit ausführen
Mit folgendem Aufruf kann man vor einem Commit prüfen, ob alles in Ordnung ist:
```
npm run check
```
