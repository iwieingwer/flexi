# Flexi

A free web app that helps people eat less meat, one meal at a time.
No account, no ads, no server: entries live in the phone's browser storage.

**Languages:** German, English · **Upper limit:** Austrian dietary guidelines (≈ 225 g meat per week). Lower is better.

## Put it online with GitHub Pages

1. Create a new public repository on GitHub, for example `flexi`.
2. Upload every file from this folder (`index.html`, `manifest.webmanifest`, `sw.js`, the icons and this README).
3. In the repository: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pick `main` and `/ (root)`, save.
4. After a minute the app is live at `https://<your-username>.github.io/flexi/`.

GitHub Pages serves over HTTPS, which the home-screen install needs.

**When you change something:** bump `VERSION` in `sw.js` (e.g. `flexi-v2`), otherwise installed copies keep the old files.

## How it works

| Part | Where |
|---|---|
| Foods and portion sizes | `FOODS` in `index.html` – one line per food: `[id, english, german, [[category, grams]]]` |
| Categories, CO2 factors, animals per kg | `CATS` |
| All texts | `T.en` and `T.de` |
| Coach names | `NAMES` |
| Targets | `GUIDE` (225 g), `MAXG` (600 g), `BIRD_G` (1,300 g of chicken per coach) |

### Add a language
Copy the `en` block inside `T`, rename it (e.g. `it`), translate the values, add a `[lang, englishName, ...]` column to `FOODS`
(or let it fall back to English), and add the language to the two language switches (search for `['de','en']`).

### Rules the app follows
- Days without an entry count as meat-free. The coach says "no meat **logged**", and a catch-up row asks to confirm gaps.
- Logging never triggers a punishment. The coach's mood follows the 7-day total.
- The whole UI gets sharper and warmer between 225 g and 600 g in 7 days (`--p` in the CSS). Above 600 g the bar breaks out of its box.
- 225 g is shown as an upper limit, not a goal. Each full week under the limit lowers the personal limit by 25 g.
- Every 1.3 kg of chicken eaten, the current coach is gone and the next one takes over. The Insights page keeps a memorial.

## Sources
- Austrian dietary guidelines 2024 (AGES / Sozialministerium)
- Statistik Austria, Versorgungsbilanzen 2025: 58.5 kg meat per person
- Poore & Nemecek 2018 via Our World in Data (CO2 per kg; beef uses the dairy-herd value, i.e. conservative)
- Animals per kg are rough estimates (chicken ≈ 1.3 kg meat, pig ≈ 80 kg, cattle ≈ 250 kg)

Flexi gives general information, not medical advice.
