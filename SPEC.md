# Spacez Review Intelligence — Product Spec

## Problem framing
Spacez has premium villas with reviews scattered across Airbnb, Booking.com, and Google. The core failure is not the reviews themselves, but that the organization cannot synthesize them into stakeholder-specific actions. Without that synthesis, recurring hospitality issues remain invisible, caretakers are overloaded with noise, operations misses fixable maintenance cases, and business cannot compare portfolio performance across platforms.

The right product is an AI-enabled review agent that normalizes ratings, extracts themes, and routes signals to three stakeholder classes with distinct actions.

## Stakeholder outputs

### 1. Operations
What it gets:
- recurring, fixable item summary by property (pool, heating, cleanliness, WiFi, check-in) 
- priority ranking by frequency and impact
- property-level issue pulse and open trends

Who acts:
- operations managers, housekeeping leads, maintenance vendors

Action it drives:
- assign work orders, validate vendor performance, close the loop on repeat failures.

Why:
Operations needs patterns, not individual praise. The data shows repeat issues at Serenity Villa (pool), Cliffside Retreat (heating), Vineyard Villa (cleanliness), and Hilltop Haven (WiFi/AC), so the output must translate reviews into tickets, not just sentiment.

### 2. Business
What it gets:
- normalized reputation score across platforms
- portfolio health chart by property and caretaker
- outlier signal for properties to back, reprioritize, or inspect
- platform comparison with scale normalization

Who acts:
- commercial leadership, revenue managers, portfolio strategy

Action it drives:
- pricing adjustments, destination-backed investments, property review escalations, partner/vendor decisions.

Why:
Business cannot act on raw reviews from multiple scales. A normalized 5-point score plus a small set of portfolio signals makes the dataset operational for prioritization.

### 3. Caretakers (prototype focus)
What it gets:
- digest of bookings they hosted
- theme-based action list (what they can fix vs what they should escalate)
- customer praise summary and recurring risk calls
- read-once guidance like “reviewed pool cleaning, check-in delays, listing oversell.”

Who acts:
- caretaker on the ground and their coordinator

Action it drives:
- immediate guest recovery, vendor coordination, confirmation of resolved issues, and issue escalation when out of control.

Why:
This is the riskiest hypothesis because caretakers can be blamed for issues beyond their control (listing accuracy, road access, occupancy policy). The prototype confines caretaker output to their hosted reviews and explicitly separates caretaker-owned issues from property/listing issues.

## Flow
1. trigger: nightly ingestion of new reviews from all platforms
2. analysis: normalize rating scales, parse review text, tag themes, assign ownership, compute recurrence
3. output:
   - operations: issue summary dashboard by property
   - business: normalized portfolio score and trend signals
   - caretakers: focused digest with actionables and non-actionable warnings
4. who acts: operations team, business leadership, caretakers
5. action: fix recurring problems, back/drop properties, recover guests and coordinate local execution

## Prototype choice
I built the prototype for caretakers because the brief explicitly asks to pressure-test that hypothesis. The design makes caretaker reporting workable by:
- limiting it to reviews the caretaker actually hosted
- surfacing only the issues they can influence directly
- marking other issues as “property/listing risk” to avoid over-blaming
- preserving positive signals so caretakers can reinforce what works

This is a stronger product than a generic review report because it separates controllability from sentiment.

## Data judgment and seeded traps
Key dataset signals:
- caretaker Lokesh Gowda has the most reviews and 6 negative cases (check-in, heating, listing oversell), which validates the hypothesis that caretaker patterns can emerge.
- recurring venue issues: Serenity Villa pool, Cliffside Retreat heating, Vineyard Villa cleanliness, Hilltop Haven WiFi.
- not caretaker-controllable: oversold photos, bad road, occupancy policy, gate restrictions.
- label normalization: use 5-point equivalent scores and platform-aware issue tagging.

## Measuring success
Success should be measured by:
- review-to-action conversion rate: percent of negative review signals with a logged operational follow-up
- false-positive control: percent of current caretaker-reported issues that are actually listing or external platform issues
- time to resolution for recurring issues after the report is published
- net promoter score/reputation lift on the flagged properties after remediation

## Risks & pushback
- caretaker reports are risky if they mix actionable service issues with out-of-control problems. The prototype explicitly separates those, but any live system must validate the ownership model with caretakers and operations.
- the dataset is small and synthetic; recurring themes are strong in this sample, but the real signal/noise ratio may be much lower.
- platform-normalized scores are useful, but should not be blind-averaged if review scales or platform audiences differ sharply.
- “good service” reviews can mask serious operational issues; the model should not reduce input to a single score for caretakers.

### What to validate first
1. caretaker ownership labels: ask caretakers whether they own check-in, housekeeping, vendor coordination, or only guest relationships.
2. issue taxonomy: confirm whether “listing oversell” and “road conditions” should surface to caretakers or only to business/operations.
3. action-wrap: test whether a short digest with 3 highest-priority items is actually read and acted on.
4. platform normalization: compare weighted ratings and ordering against real booking performance.
