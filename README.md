# Clinic Metrics & Case Review Dashboard (Front-End Only, Offline)

Build a small single-page app that explores clinic performance and captures review notes. Choose **React** or **Angular**. **No backend.** All data is local.

## Constraints
- Must run **offline** (no network calls).
- **No external APIs/CDNs**; use only local files included in the repo.
- Load data from local JSON (e.g., `data/*.json`) or imported modules.
- Keep dependencies minimal (no heavy UI libraries).

## Data & Metrics
Create a non-trivial local dataset (e.g., ~6 clinics, ~12–15 providers, ~80–100 visits, ~160–220 procedures).

data shapes:
- `clinics`: `{ id, name, lob, profession, city, state }`
- `providers`: `{ id, clinic_id, name, npi }`
- `visits`: `{ id, clinic_id, provider_id, service_date (ISO), allowed_amount (number), services_count (int) }`
- `procedures`: `{ id, visit_id, cpt_code, units (int), charge (number) }`

Per-clinic metrics to display:
- **Total Visits**
- **Total Allowed**
- **Services/Visit** = (sum of `services_count`) ÷ (visit count)
- **CPT Mix**: percentage of **units** by CPT code (e.g., `97110`, `97112`, `97140`, `97530`)

## Clinics Table
- Show clinics with the derived metrics.
- **Filters**: LOB, text search (clinic name).
- **Sort**: by **Total Allowed** (toggle asc/desc).
- **Pagination**: page size 8.
- Filters, sort, and pagination must **compose** correctly.

## Clinic Detail Drawer
When a row is clicked, open a drawer/dialog showing:
- **Providers** for the clinic (name, NPI, visit count).
- **Mini bar chart** for CPT Mix (simple `<div>` widths or lightweight SVG; no chart libraries).
- **Recent 5 visits** with `service_date`, `allowed_amount`, and total **units** (sum of that visit’s procedures).

## Case Review
Inside the drawer, add a review:
- Fields: `reviewer_name` (required), `status` (`"Watch" | "Investigate" | "Clear"`), `notes` (20–300 chars).
- On submit: **optimistically** append to a local “Reviews” list and persist in **localStorage**.
