---
title: "Melbourne cafe and tea retailer database"
date: 2026-03-02
updated: 2026-03-02
source: claude.ai web (account export 2026-07-18)
source_uuid: dee0166a-c052-48f0-b9a5-e7fc8d8419e2
messages: 4
---

# Melbourne cafe and tea retailer database

> Full transcript imported from a claude.ai web conversation (2026-03-02, 4 messages). Assistant *thinking* and raw *tool-result* payloads were omitted for readability; tool **use** is marked inline. Raw source: `_sources/Export Data 18072026/conversations.json`.

### 🧑 **Angela**

I would like to document a database of Melbourne (Australia)'s cafe's, tea retailers, and coffee retailers. Would you be able to generate a current database with the following fields.
Vendor Name
Location (address, postcode, suburb, State)
Trading hours
What they sell: Coffee, Matcha, Tea, Coffee Retailer, Tea Retailer

---

### 🤖 **Claude**

*[used view: /mnt/skills/public/xlsx/SKILL.md]*

Let me search for Melbourne cafes and retailers to populate this database.

*[used places_search]*

Now I have enough data to build a comprehensive spreadsheet. Let me compile this into an Excel file.

*[used bash_tool: cat << 'EOF' > /home/claude/create_db.py from openpyxl import Workbook from openpyxl.styles import F]*

*[used present_files]*

Here's your Melbourne vendor database with **23 entries** spanning cafes, matcha spots, and tea retailers. It includes:

- **Coffee cafes & roasters** — Patricia Coffee Brewers, Dukes, Seven Seeds, Proud Mary, Small Batch, and more
- **Matcha specialists** — Matcha Kobo, Balibola, K5 Kona, Hikari, Miyama
- **Tea retailers** — LUPICIA, T2, TEAMOO, Tea Tonic, Tea Leaves, Tea Drop

Each entry has full address fields, day-by-day trading hours, and Yes/No flags for Coffee, Matcha, Tea, Coffee Retailer, and Tea Retailer. The spreadsheet is colour-coded (green "Yes", grey "No") for easy scanning, and the top row is frozen for scrolling.

---

### 🧑 **Angela**

Thanks, I expect there to be more than 23 entries. Are there anymore ways of identifying as many vendors as possible?

---

### 🤖 **Claude**

Great point! Let me do a much broader search across more suburbs, vendor types, and search terms to build a more comprehensive database.

*[used places_search]*

*[used places_search]*

*[used places_search]*

Excellent — I now have a very rich dataset. Let me build the expanded spreadsheet with all unique vendors.

*[used bash_tool: cat << 'EOF' > /home/claude/build_db.py from openpyxl import Workbook from openpyxl.styles import Fo]*

*[used present_files]*

The updated database now has **90 vendors** across two sheets — the main database and a summary tab. Here's what was added compared to v1:

**New suburbs covered:** Fitzroy, Fitzroy North, Clifton Hill, Collingwood, Richmond, Cremorne, South Yarra, St Kilda, Brunswick, Brunswick East, Prahran, Windsor, Hawthorn, Hawthorn East, Preston, Northcote, Thornbury, Abbotsford, South Melbourne, Kew, and outlying roasters in Dingley Village, Clayton, Campbellfield, Pascoe Vale, and Reservoir.

**Strategies used to maximise coverage:**
- Searched by suburb across ~15 inner-Melbourne neighbourhoods
- Searched specifically by vendor type (matcha cafes, tea retailers, coffee roasters/wholesalers)
- Included dedicated wholesale roasters (Reverence, Strada, Bennetti, Gigante, Coffex) which are easy to miss if only searching "café"

To go even broader in future, you could also search shopping centre food courts, hotel lobbies, market stalls (e.g. Queen Victoria Market, South Melbourne Market), and outer suburbs like Footscray, Williamstown, Doncaster, and Glen Waverley.


Related: [[Reference/index|Reference]]