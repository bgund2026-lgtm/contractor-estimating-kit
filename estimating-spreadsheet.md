# Contractor Estimating Spreadsheet — Google Sheets Specification

> **Purpose:** Build a professional estimating spreadsheet in Google Sheets that calculates material costs, labor, equipment, subcontractors, markup, and produces a clean estimate you can print or email. Every formula, every cell, every sheet — specified below.

---

## Sheet Structure

| Sheet # | Sheet Name | Purpose |
|---------|-----------|---------|
| 1 | Job Info | Project details, client info, estimate number |
| 2 | Material Takeoff | All materials with quantities, unit costs, waste factors |
| 3 | Labor Calculator | Crew, hours, rates, productivity factors |
| 4 | Equipment | Equipment rentals, owned equipment costs |
| 5 | Subcontractor | Sub bids and quotes |
| 6 | Summary | Rolls up all sheets, applies markup, shows profit |
| 7 | Estimate Output | Client-facing estimate — clean, printable |

---

## Sheet 1: Job Info

**Layout:**

| Cell | Content | Example |
|------|---------|---------|
| A1 | **ESTIMATE NUMBER** | EST-2026-0042 |
| A2 | **Date** | 2026-04-16 |
| A3 | **Valid Until** | 2026-05-16 (30 days) |
| A5 | **Client Name** | Thompson, Robert |
| A6 | **Client Address** | 4820 Oakridge Dr, Calgary, AB T2V 3L6 |
| A7 | **Client Phone** | (403) 555-0192 |
| A8 | **Client Email** | r.thompson@email.com |
| A10 | **Project Name** | Thompson Bathroom Remodel |
| A11 | **Project Address** | 4820 Oakridge Dr, Calgary, AB T2V 3L6 |
| A12 | **Project Type** | Bathroom Remodel |
| A13 | **Trade** | General / Plumbing / Electrical / HVAC / Painting / Landscaping |
| A14 | **Square Footage** | 85 sq ft |
| A15 | **Project Description** | Full gut and remodel of master bathroom including new fixtures, tile, vanity, lighting, and exhaust fan |
| A17 | **Your Company Name** | [Your Company] |
| A18 | **Your License #** | [License] |
| A19 | **Your Contact** | [Phone / Email] |
| A20 | **Insurance Info** | [WCB / Liability policy #] |

**Named Ranges:** Set these up for cross-sheet references:
- `EstimateNumber` → Job Info!B1
- `ClientName` → Job Info!B5
- `ProjectName` → Job Info!B10
- `ProjectAddress` → Job Info!B11

---

## Sheet 2: Material Takeoff

**Header Row (Row 1):**

| Col | Header | Width |
|-----|--------|-------|
| A | Item # | 60px |
| B | Category | 120px |
| C | Description | 250px |
| D | Quantity | 80px |
| E | Unit | 60px |
| F | Unit Cost | 90px |
| G | Waste Factor % | 90px |
| H | Extended Cost | 100px |
| I | Markup % | 80px |
| J | Marked-Up Cost | 100px |
| K | Supplier | 120px |
| L | Notes | 200px |

**Formulas:**

| Cell | Formula |
|------|---------|
| H2 (and down) | `=D2*F2*(1+G2)` — Quantity × Unit Cost × (1 + Waste Factor) |
| J2 (and down) | `=H2*(1+I2)` — Extended Cost × (1 + Markup %) |

**Subtotals (Row 50 — or wherever your data ends):**

| Cell | Formula |
|------|---------|
| H50 | `=SUM(H2:H49)` — Total material cost before markup |
| J50 | `=SUM(J2:J49)` — Total material cost after markup |

**Named Ranges:**
- `MaterialCostBeforeMarkup` → Material Takeoff!H50
- `MaterialCostAfterMarkup` → Material Takeoff!J50

### Reference Data — Material Unit Costs (2026 Canadian/US Averages)

> **These are ballpark numbers for estimating. Always verify with your actual supplier quotes. Prices vary by region, availability, and season.**

#### Electrical

| Item | Unit | Cost (CAD) | Cost (USD) |
|------|------|-----------|-----------|
| 14/2 NM-B Romex | 1000' roll | $185 | $145 |
| 14/3 NM-B Romex | 250' roll | $68 | $52 |
| 12/2 NM-B Romex | 1000' roll | $220 | $170 |
| Single-pole switch | each | $8 | $6 |
| 3-way switch | each | $14 | $11 |
| 15A breaker (standard) | each | $12 | $9 |
| 20A breaker | each | $14 | $11 |
| Standard duplex receptacle | each | $5 | $4 |
| GFCI receptacle | each | $28 | $22 |
| AFCI breaker | each | $55 | $42 |
| 4" recessed LED housing (IC rated) | each | $32 | $25 |
| 6" recessed LED housing (IC rated) | each | $28 | $22 |
| LED trim (white) | each | $18 | $14 |
| Ceiling light fixture (basic) | each | $45 | $35 |
| Exterior LED floodlight | each | $65 | $50 |
| 100A main breaker panel (42-space) | each | $420 | $325 |
| 200A main breaker panel (42-space) | each | $580 | $450 |
| Service entrance cable (Aluminum 2/0) | per ft | $8 | $6 |
| Junction box (single gang) | each | $3 | $2 |
| Junction box (4" square) | each | $6 | $5 |
| Wire connectors (100-pack) | each | $18 | $14 |
| EMT conduit ½" | 10' stick | $12 | $9 |
| EMT conduit ¾" | 10' stick | $16 | $12 |
| MC cable 14/2 | 250' roll | $145 | $110 |

#### Plumbing

| Item | Unit | Cost (CAD) | Cost (USD) |
|------|------|-----------|-----------|
| ½" copper pipe (Type M) | 10' stick | $22 | $17 |
| ¾" copper pipe (Type M) | 10' stick | $32 | $25 |
| ½" PEX-A (Uponor) | 100' roll | $65 | $50 |
| ¾" PEX-A (Uponor) | 100' roll | $95 | $72 |
| PEX-A fittings ( assorted 25-pack) | pack | $45 | $35 |
| Shut-off valve (¼-turn, ½") | each | $12 | $9 |
| Toilet (2-piece, elongated, dual-flush) | each | $285 | $220 |
| Vanity (36", with top) | each | $450 | $350 |
| Drop-in bathroom sink | each | $85 | $65 |
| Shower valve (pressure-balanced) | each | $195 | $150 |
| Thermostatic shower valve | each | $340 | $260 |
| Bathtub (60" acrylic) | each | $520 | $400 |
| Walk-in shower pan (60" × 32") | each | $380 | $290 |
| Bathroom faucet (single-hole) | each | $85 | $65 |
| Kitchen faucet (single-handle pull-down) | each | $145 | $110 |
| Kitchen sink (stainless, dual basin) | each | $195 | $150 |
| Water heater (40 gal, electric) | each | $520 | $400 |
| Water heater (50 gal, gas) | each | $780 | $600 |
| Tankless water heater (gas, indoor) | each | $1,350 | $1,050 |
| PVC DWV pipe 3" | 10' stick | $18 | $14 |
| ABS DWV pipe 3" | 10' stick | $14 | $11 |
| Toilet flange (PVC) | each | $8 | $6 |
| Pipe insulation (½", 6' length) | each | $4 | $3 |

#### HVAC

| Item | Unit | Cost (CAD) | Cost (USD) |
|------|------|-----------|-----------|
| Furnace (80% AFUE, 60k BTU) | each | $2,200 | $1,700 |
| Furnace (95% AFUE, 80k BTU) | each | $3,400 | $2,600 |
| Central AC (14 SEER, 2-ton) | each | $2,800 | $2,150 |
| Central AC (16 SEER, 3-ton) | each | $4,200 | $3,200 |
| Ductless mini-split (12k BTU) | each | $2,100 | $1,600 |
| Ductless mini-split (18k BTU) | each | $2,800 | $2,150 |
| Ductless mini-split (24k BTU) | each | $3,600 | $2,750 |
| HRV (heat recovery ventilator) | each | $2,400 | $1,850 |
| ERV (energy recovery ventilator) | each | $2,800 | $2,150 |
| Thermostat (programmable) | each | $55 | $42 |
| Smart thermostat (ecobee/Google Nest) | each | $280 | $215 |
| Sheet metal duct (6" round, 5' length) | each | $22 | $17 |
| Flex duct (6" round, 25' length) | each | $28 | $22 |
| Duct insulation (R-8, 6", 50' roll) | each | $85 | $65 |
| Refrigerant line set (¼" × ½", 25') | each | $95 | $72 |
| Condensate pump | each | $65 | $50 |
| Air filter (4" pleated, 20×25) | each | $22 | $17 |

#### General Construction

| Item | Unit | Cost (CAD) | Cost (USD) |
|------|------|-----------|-----------|
| 2×4 SPF lumber (8') | each | $6.50 | $5.00 |
| 2×6 SPF lumber (8') | each | $8.50 | $6.50 |
| 2×10 SPF lumber (12') | each | $18 | $14 |
| 2×12 SPF lumber (14') | each | $28 | $22 |
| ½" drywall (4×8 sheet) | each | $14 | $11 |
| 5/8" drywall (4×8 sheet) | each | $16 | $12 |
| Cement board (3×5 sheet) | each | $22 | $17 |
| Plywood ½" (4×8 sheet) | each | $52 | $40 |
| Plywood ¾" (4×8 sheet) | each | $68 | $52 |
| OSB 7/16" (4×8 sheet) | each | $22 | $17 |
| Subfloor (5/8" tongue & groove) | each | $42 | $32 |
| Kerdi membrane (sheet, 54 sq ft) | roll | $110 | $85 |
| Red Guard (1 gal) | each | $58 | $45 |
| Thin-set mortar (50 lb) | each | $28 | $22 |
| Grout (sanded, 25 lb) | each | $22 | $17 |
| Ceramic tile (12×12, basic) | sq ft | $4 | $3 |
| Porcelain tile (12×24, mid-grade) | sq ft | $7 | $5.50 |
| Luxury vinyl plank (click-lock) | sq ft | $5 | $4 |
| Engineered hardwood (mid-grade) | sq ft | $9 | $7 |
| Paint (interior latex, 1 gal) | each | $48 | $38 |
| Paint (interior latex, 5 gal) | each | $195 | $150 |
| Primer (1 gal) | each | $38 | $28 |
| Baseboard (MDF, 3-5/8", 8') | each | $8 | $6 |
| Casing (MDF, 2-¼", 7') | each | $5 | $4 |
| Insulation R-12 (batt, 15", 78 sq ft) | bag | $42 | $32 |
| Insulation R-20 (batt, 23", 44 sq ft) | bag | $52 | $40 |
| Insulation R-28 (batt, 23", 32 sq ft) | bag | $58 | $45 |
| 6 mil vapor barrier (20×100 roll) | roll | $85 | $65 |
| Concrete mix (30 kg bag) | each | $8 | $6 |
| Tar paper (15 lb, 400 sq ft roll) | roll | $32 | $25 |
| Ice & water shield (2 sq roll) | roll | $85 | $65 |
| Asphalt shingles (bundle, 33 sq ft) | each | $38 | $28 |

---

## Sheet 3: Labor Calculator

**Header Row (Row 1):**

| Col | Header |
|-----|--------|
| A | Task # |
| B | Task Description |
| C | Crew Size |
| D | Hours Per Person |
| E | Total Hours |
| F | Hourly Rate |
| G | Burden Rate % |
| H | Burdened Rate |
| I | Total Labor Cost |
| J | Productivity Factor |
| K | Adjusted Labor Cost |

**Formulas:**

| Cell | Formula |
|------|---------|
| E2 | `=C2*D2` — Crew Size × Hours Per Person |
| H2 | `=F2*(1+G2)` — Hourly Rate × (1 + Burden Rate) |
| I2 | `=E2*H2` — Total Hours × Burdened Rate |
| K2 | `=I2*J2` — Total Labor × Productivity Factor |

**Productivity Factor:** This adjusts for real-world conditions. 
- 1.0 = standard conditions (easy access, normal pace)
- 1.15 = tight spaces, occupied home, moderate complexity
- 1.30 = difficult access, elderly client, historic home, winter work
- 1.50 = extremely difficult (confined space, extreme weather, complex integration)

**Subtotals (Row 30):**

| Cell | Formula |
|------|---------|
| E30 | `=SUM(E2:E29)` |
| I30 | `=SUM(I2:I29)` — Total labor before productivity |
| K30 | `=SUM(K2:K29)` — Total labor after productivity |

**Named Ranges:**
- `TotalLaborCost` → Labor Calculator!K30

### Labor Rate Reference (2026, Canadian/US averages, burdened)

| Trade | Hourly Rate (CAD) | Hourly Rate (USD) | Burden % |
|-------|------------------|------------------|----------|
| Licensed Electrician | $55–75 | $42–58 | 25% |
| Electrician Apprentice | $30–42 | $22–32 | 25% |
| Licensed Plumber | $55–78 | $42–60 | 25% |
| Plumber Apprentice | $30–42 | $22–32 | 25% |
| HVAC Technician | $55–80 | $42–62 | 25% |
| HVAC Apprentice | $30–42 | $22–32 | 25% |
| General Carpenter | $45–65 | $35–50 | 25% |
| Finish Carpenter | $50–70 | $38–55 | 25% |
| Drywaller/Taper | $38–55 | $28–42 | 25% |
| Painter | $35–50 | $28–38 | 25% |
| Tile Setter | $45–65 | $35–50 | 25% |
| Laborer (unskilled) | $25–35 | $18–28 | 20% |
| Foreman/Site Lead | $55–80 | $42–62 | 25% |

**Burden includes:** WCB/WSIB, CPP/EI, vacation pay, liability insurance, tools allowance. Add 20-30% to hourly wage to get your true cost.

---

## Sheet 4: Equipment

**Header Row (Row 1):**

| Col | Header |
|-----|--------|
| A | Item # |
| B | Equipment Description |
| C | Owned or Rented |
| D | Daily/Weekly Rate |
| E | Rental Period |
| F | Period Unit (days/weeks) |
| G | Total Cost |
| H | Fuel/Operating Cost |
| I | Total Equipment Cost |

**Formulas:**

| Cell | Formula |
|------|---------|
| G2 | `=D2*E2` — Rate × Period |
| I2 | `=G2+H2` — Rental + Operating |

**Subtotals (Row 20):**

| Cell | Formula |
|------|---------|
| I20 | `=SUM(I2:I19)` — Total equipment cost |

**Named Ranges:**
- `EquipmentCost` → Equipment!I20

### Equipment Rate Reference (2026)

| Equipment | Daily Rate | Weekly Rate |
|-----------|-----------|-------------|
| Excavator (mini, 1.5 ton) | $350 | $1,200 |
| Excavator (3 ton) | $500 | $1,800 |
| Skid steer | $400 | $1,400 |
| Dump trailer | $125 | $450 |
| Concrete mixer | $95 | $350 |
| Scaffolding set | $75 | $275 |
| Drywall lift | $65 | $225 |
| Tile saw (10" wet) | $75 | $275 |
| Pressure washer | $85 | $300 |
| Generator (5kW) | $125 | $450 |
| Boom lift (26') | $450 | $1,600 |
| Scissor lift | $325 | $1,150 |

---

## Sheet 5: Subcontractor

**Header Row (Row 1):**

| Col | Header |
|-----|--------|
| A | Sub # |
| B | Trade/Company |
| C | Contact |
| D | Quote Amount |
| E | Quote Date |
| F | Valid Until |
| G | Included Scope |
| H | Exclusions |
| I | Status (Received/Pending) |

**Subtotals (Row 20):**

| Cell | Formula |
|------|---------|
| D20 | `=SUM(D2:D19)` — Total subcontractor costs |

**Named Ranges:**
- `SubcontractorCost` → Subcontractor!D20

---

## Sheet 6: Summary

**Layout:**

| Row | A | B |
|-----|---|---|
| 1 | **COST SUMMARY** | |
| 2 | | |
| 3 | Materials (after markup) | `=MaterialCostAfterMarkup` |
| 4 | Labor (after productivity) | `=TotalLaborCost` |
| 5 | Equipment | `=EquipmentCost` |
| 6 | Subcontractors | `=SubcontractorCost` |
| 7 | | |
| 8 | **Total Direct Cost** | `=SUM(B3:B6)` |
| 9 | | |
| 10 | Overhead % | [input: e.g., 15%] |
| 11 | Overhead $ | `=B8*B10` |
| 12 | | |
| 13 | **Subtotal + Overhead** | `=B8+B11` |
| 14 | | |
| 15 | Profit % | [input: e.g., 15%] |
| 16 | Profit $ | `=B13*B15` |
| 17 | | |
| 18 | **TOTAL ESTIMATE** | `=B13+B16` |
| 19 | | |
| 20 | Contingency % | [input: e.g., 10%] |
| 21 | Contingency $ | `=B18*B20` |
| 22 | | |
| 23 | **ESTIMATE WITH CONTINGENCY** | `=B18+B21` |
| 24 | | |
| 25 | **Per Sq Ft** | `=B23/JobInfo!B14` |

**Overhead vs. Profit — They're different!**

- **Overhead** = costs of running your business that aren't on any job site: office rent, truck payment, insurance, accounting, phone, software, marketing, owner's salary not on tools. Most contractors need 10-20% overhead.
- **Profit** = what's left after ALL costs including overhead. This is what grows your business. Target 8-15% profit on residential, 5-10% on commercial.

**Named Ranges:**
- `EstimateTotal` → Summary!B18
- `EstimateWithContingency` → Summary!B23

---

## Sheet 7: Estimate Output (Client-Facing)

This is the clean sheet you print or PDF and send to the client. No formulas they can break — just formatted references.

**Layout:**

| Row | Content |
|-----|---------|
| 1 | [Your Company Logo] |
| 2 | [Your Company Name] |
| 3 | [License #] · [Phone] · [Email] |
| 4 | |
| 5 | **ESTIMATE** |
| 6 | Estimate #: `=JobInfo!B1` |
| 7 | Date: `=JobInfo!B2` |
| 8 | Valid For: 30 Days |
| 9 | |
| 10 | **Prepared For:** |
| 11 | `=JobInfo!B5` |
| 12 | `=JobInfo!B6` |
| 13 | `=JobInfo!B7` |
| 14 | |
| 15 | **Project:** `=JobInfo!B10` |
| 16 | `=JobInfo!B11` |
| 17 | |
| 18 | **Scope of Work:** |
| 19 | `=JobInfo!B15` |
| 20 | |
| 21 | **Cost Breakdown:** |
| 22 | |
| 23 | | Category | Amount |
| 24 | Materials | `=Summary!B3` |
| 25 | Labor | `=Summary!B4` |
| 26 | Equipment | `=Summary!B5` |
| 27 | Subcontractors | `=Summary!B6` |
| 28 | Overhead & Profit | `=Summary!B11+Summary!B16` |
| 29 | **TOTAL** | **`=Summary!B18`** |
| 30 | |
| 31 | *Contingency of `=Summary!B20`% (`=Summary!B21`) may apply for unforeseen conditions* |
| 32 | |
| 33 | **Payment Terms:** |
| 34 | 50% upon acceptance, 25% at midpoint, 25% upon completion |
| 35 | |
| 36 | **Change Orders:** Any work beyond the scope described above requires a signed Change Order with revised pricing before work proceeds. |
| 37 | |
| 38 | **This estimate is valid for 30 days from the date above.** |
| 39 | |
| 40 | Accepted by: _________________________ Date: __________ |
| 41 | Signature: _________________________ |

**Formatting the Output Sheet:**
- Hide gridlines (View → Show → Gridlines, uncheck)
- Set print area to A1:D41
- Use alternating row colors for the cost breakdown
- Bold and enlarge the TOTAL row
- Add your logo as an image in A1

---

## How to Use This Spreadsheet

1. **Duplicate the template** for every new estimate. Don't edit the master.
2. **Start with Job Info** — fill in all client and project details.
3. **Material Takeoff** — walk the job, measure everything, enter line items. Use the reference data as a starting point but get real quotes for large items.
4. **Labor Calculator** — break the job into tasks. Be realistic about hours (most contractors underestimate by 20-30%). Apply productivity factors honestly.
5. **Equipment** — list everything you need to rent or operate. Include your own equipment at rental rates — if you own it, you should still be paid for its use.
6. **Subcontractor** — enter quotes as you receive them. Flag pending ones in red.
7. **Summary** — review all costs. Adjust overhead and profit percentages. Review the contingency — 10% is standard for remodels, 5% for new construction, 15-20% for historic/unknown conditions.
8. **Estimate Output** — print or PDF this sheet. It's what the client sees.

**Pro tip:** Never show the client the Summary sheet with overhead and profit broken out. They don't need to see your margin — they need to see a fair price for quality work. The Estimate Output sheet shows a single total, which is what matters.