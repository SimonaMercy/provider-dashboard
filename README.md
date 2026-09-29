# UpNow Provider Workspace — HTML pages + Figma guide

## 1. What's in the folder
```
provider-workspace/
  pages.html            ← START HERE: links to every page
  index.html            ← main page (opens on Demand)
  design-system.html    ← colours, type, spacing, every component
  design-tokens.json    ← tokens for Figma Variables / Tokens Studio

  Shared UpNow OS
    demand.html         lead sources, funnel, reply queue, today
    leads.html          pipeline board + list
    calendar.html       week / agenda, scheduling
    inbox.html          Communications — one inbox for all channels
    money.html          cash, bills, payouts, deposits, expenses, profit
    settings.html       grouped settings + channel connect flow
    (finance.html and business.html also open Money, so old links keep working)

  Vertical pack  (add ?pack=spaces|services|experiences|memberships|programs|health|insurance)
    overview.html  portfolio.html  deals.html  ops.html
    perf.html      cases.html      reports.html

  css/ pw/ js/ img/     shared code + photos — keep these next to the pages
```
Every page works on its own and links to the others through the sidebar. Changes (moved leads, sent messages, activated packs) carry across pages.
To reset sample data: open the browser console and run `localStorage.removeItem('upnow.pw.v1')`.

## 2. Put it online (Figma plugins import from a URL)
Pick one:
- **Netlify Drop** (easiest): drag the whole project folder (with `Home.html` next to `provider-workspace/`) onto app.netlify.com/drop. You get a link like `https://xyz.netlify.app/provider-workspace/pages.html`.
- **GitHub Pages / Vercel**: push the folder and turn on Pages.
- **Local only**: run `npx serve .` in the project folder. Works with the Chrome-extension route below.

## 3. Build the design system in Figma first
1. Install the fonts **DM Serif Display** and **Plus Jakarta Sans** from Google Fonts, otherwise Figma swaps them.
2. Install the **Tokens Studio for Figma** plugin → Load from file → `design-tokens.json` → create Variables (Colour, Radius, Spacing).
3. Install **html.to.design** (Figma Community plugin). Import `design-system.html` at 1440 wide with "Create local styles" ticked.
4. Turn each block into a component (select → ⌥⌘K / Ctrl+Alt+K):
   | Component | Variants |
   |---|---|
   | Button | Primary · Outline · WhatsApp · Ghost × md / sm |
   | Chip | default · selected |
   | Status pill | live · warn · risk · mute · info |
   | Source tag | one per channel colour |
   | KPI card | with / without sparkline |
   | Attention strip | 4 cells |
   | Lead card | hot · warm · cold, late / on time |
   | Listing card | live · in review · draft · paused |
   | Sidebar item | Shared OS on/off (dark green) · Pack on/off (light green) |
   | Chat bubble | in · out · note · system |
   | Tabs, Segmented, Toggle, Table row, Drawer, Modal | — |
5. Use Auto Layout on cards, the sidebar and the top bar so they resize.

## 4. Import the pages
For each page in `pages.html`:
1. Run html.to.design → paste the page URL → viewport **1440 × 900** → Import.
2. Put each on its own Figma page: `01 Demand`, `02 Leads`, `03 Calendar`, `04 Communications`, `05 Money`, `06 Settings`, `10 Pack Overview` … `16 Reports`.
3. Swap imported layers for your components (right-click → Select matching layers → swap instance).

**Open states** (drawers, pop-ups, steps) need the html.to.design **Chrome extension**: open the page, click into the state, capture.
| Frame to capture | How to get there |
|---|---|
| Demand · Spaces and Services | demand.html, switch pack in sidebar |
| Leads · board, list, lead drawer | leads.html → toggle view → click a card |
| Inbox · thread, internal note, draft reply | inbox.html → Internal note / Draft reply |
| Calendar · week, agenda, event pop-up, schedule form | calendar.html → click an event → New |
| Money · each of the 8 tabs, transaction drawer | money.html → tabs → click a row |
| Portfolio · listing drawer, add-listing steps 1–7 | portfolio.html → click a card / Add listing |
| Settings · overview, each section, channel connect steps | settings.html → Channels → Connect |
| Pack switcher, activate pack | click the pack switcher in the sidebar |
| Arabic (right-to-left), USD view | language and currency selects in the header |

## 5. Wire the prototype in Figma
- Sidebar items → On click → **Navigate to** the matching page frame.
- Lead card, listing card, transaction row → **Open overlay** (drawer frame, position right, close on outside click).
- Add listing, Connect channel → **Navigate** through the step frames (Smart animate).
- Pack switcher → **Open overlay** (manual position, next to the button).
- Set **Demand** as the starting frame → Present.

## 6. Tips
- Other sizes: import again at 1280 or 834 (tablet). The pages are responsive.
- Images come in as fills; keep them or replace with your own photos.
- If a page looks stale after edits, hard-refresh (Ctrl/Cmd + Shift + R) before capturing.
