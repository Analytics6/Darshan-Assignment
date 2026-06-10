# Spacez Review Intelligence Prototype

This repository contains a prototype for Spacez's AI-powered review synthesis system.

## What’s included
- `SPEC.md` — product spec, stakeholder design, flow, and risk analysis
- `prototype/` — working caretaker-focused prototype
- `spacez_reviews_dataset (1).xlsx` — input review dataset

## Prototype
The working prototype is in `prototype/index.html`.

### Run locally
1. Open a terminal in `/workspaces/Darshan-Assignment/prototype`
2. Run:
   ```bash
   python3 -m http.server 8000
   ```
3. Open:
   ```
   http://127.0.0.1:8000
   ```

The page shows the caretaker digest, plus operations and business summary panels.

## Notes
- The prototype focuses on the caretaker stakeholder, but also includes operation/business signal summaries.
- It normalizes ratings across Airbnb, Booking.com, and Google.
- `prototype/process_reviews.py` rebuilds the JSON data from the Excel file.
