# FOODSOLUTIONS IS-RR SYSTEM

A Receiving Report (RR) and Issue Slip (IS) system, modeled on the MEATPLUS IS-RR system. Built as a single-file web app backed by Supabase.

## How to run
Open `index.html` in a web browser (double-click it, or host it on any static web server / Netlify / internal share). No build step required — it connects directly to the Supabase backend.

## Login
- **Email:** `itadmin@foodsolutions.ph`
- **Password:** `FoodSolutions2026`  *(change this after first login by adding your own admin user in the Users tab and deleting/repurposing this one)*

## Modules
- **Dashboard** — counts, net stock, depleted items, recent RR/IS.
- **Receiving Reports** — record goods received (supplier, storage, PO/CV, transaction type, line items with boxes, net weight, production/expiry dates). RR code auto-generated as `RR{YYMM}{0001}`. Print-ready document.
- **Issue Slips** — record goods issued out (origin, transport/driver, checker, received by, line items with boxes, net & actual weight). IS code auto-generated as `IS{YYMM}{0001}`. Print-ready document.
- **Inventory** — live stock balance per item & brand: received (RR) minus issued (IS). Issued weight uses actual weight when recorded. CSV export.
- **Masters** *(admin)* — Items, Brands, Suppliers, Storage Locations.
- **Users** *(admin)* — add users and assign roles.

## Roles
- **admin** — full access including Masters, Users, and delete.
- **approver** — encode RR/IS and delete.
- **encoder** — encode RR/IS only.

## Backend (Supabase)
- Project: `bom-system` (`emkcwukiqxnvcbhkjiqz`), region ap-southeast-1.
- Tables are prefixed `fsisrr_` (separate from MEATPLUS `isrr_`).
- Row Level Security is enabled; only authenticated users can read/write. RR/IS numbering is handled by atomic Postgres functions (`fsisrr_next_rr`, `fsisrr_next_is`).

## Notes
- Sample data (2 receiving reports, 1 issue slip, master lists) is preloaded so the app isn't empty. Delete it anytime from within the app.
- Config (Supabase URL + publishable key) is at the top of the `<script>` block in `index.html`.
