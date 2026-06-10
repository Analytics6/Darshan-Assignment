# Spacez Review Intelligence — Submission Summary

## Deliverables
- Spec: `SPEC.md`
- Prototype: `prototype/index.html` with `prototype/data/reviews.json`
- Data processing: `prototype/process_reviews.py`
- Local prototype preview: run `python3 -m http.server 8001` in `/workspaces/Darshan-Assignment/prototype`, then open `http://127.0.0.1:8001`.

> Loom walkthrough link: TBD (record after review).

## What this solves
Spacez reviews are scattered across Airbnb, Booking.com, and Google. The prototype synthesizes them into three stakeholder views:
- Operations: recurring fixable issues and property-level patterns
- Business: normalized portfolio health and platform-comparison signals
- Caretakers: focused digest for reviews they hosted, with actionable issues and explicit escalation flags

The prototype is deeply built for caretakers because the brief asks us to pressure-test that hypothesis and because this is where ownership noise is highest.

## Stakeholder outputs

### Operations
- Summary of recurring issues by property and tag
- Priority list of themes that drive vendor/maintenance action
- Action: create work orders, fix recurring housekeeping/maintenance issues, and close the loop on repeating problems

### Business
- Normalized 5-point rating score per property
- Portfolio signal for reputational risk and high-value assets
- Action: decide which properties to back, inspect, or reprioritize; adjust pricing and marketing around quality signals

### Caretakers (prototype)
- Reviews filtered to the caretaker’s hosted stays
- Theme-based issue summary with current priorities
- Explicit separation of caretaker-owned issues from business/listing-level problems
- Action: recover guests, coordinate vendors, confirm fixes, and escalate non-actionable issues to operations/business

## Caretaker hypothesis pressure test
This is risky because caretakers can be blamed for problems outside their control, such as:
- mis-sold listing photos
- bad road access
- occupancy policy enforcement
- platform-scale differences

The prototype handles this by classifying tags into ownership buckets. Caretaker-owned issues are mostly check-in and service. Operations-owned issues include pool, heating, cleanliness, and WiFi. Business-owned issues include listing accuracy and policy communication.

## Data judgment and traps caught
The dataset reveals real seeded traps:
- `Serenity Villa` has recurring pool maintenance issues across platforms.
- `Cliffside Retreat` has repeated heating failures.
- `Vineyard Villa` shows consistent cleanliness failures.
- `Hilltop Haven` has WiFi and listing-accuracy issues.
- `Misty Estate` and `Coorg Canopy` show caretaker check-in delays tied to `Lokesh Gowda`.
- `Backwater Bungalow` is strong on caretaker service, weaker on humidity/mosquito environment.
- `Occupancy policy` and `road condition` issues are correctly treated as business/listing signals, not caretaker-owned service failures.

## Execution and outputs
The prototype includes:
- `process_reviews.py`: reads the attached Excel file, normalizes ratings, extracts themes, and assigns ownership labels
- `data/reviews.json`: processed review dataset used by the web UI
- `index.html`: interactive prototype for caretaker digest, operations snapshots, and business signals

## How to validate
1. Run `python3 process_reviews.py` in `/workspaces/Darshan-Assignment/prototype`
2. Start the preview server in `/workspaces/Darshan-Assignment/prototype`:
   ```bash
   python3 -m http.server 8001
   ```
3. Open `http://127.0.0.1:8001`
4. Use the caretaker dropdown to inspect each caretaker’s review digest
5. Confirm that operations and business panels surface recurring issues and normalized scores

## Risks & pushback
- The dataset is synthetic and small; real Supply/Occupancy data may introduce more noise.
- Caretaker reports must not become blame reports. The prototype assigns issue ownership to reduce that risk, but live validation with caretakers is needed.
- Platform normalization is simplified to a 10->5 conversion; real review platforms may require additional weighting.
- The current prototype uses rule-based review parsing rather than a full generative LLM pipeline. It is a strong design prototype, but a production implementation should add a trained extraction layer or prompt-driven AI for more nuanced themes.

## Next steps
- Record the Loom walkthrough describing the prototype, system flow, and dataset traps
- Add a shareable Google Doc using this summary as the submission document
- If available, connect the prototype to a real LLM service for live review summarization and ownership classification
