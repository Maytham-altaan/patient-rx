# Pharmacy Triage Pilot — نموذج تجريبي (الإسهال)

A single-file prototype for the MSc proposal *Development, Validation, and Evaluation of an AI-Powered
Self-Medication Support Tool for Managing Patients with Minor Illness Symptoms* (University of Baghdad,
College of Pharmacy). Diarrhoea is the pilot ailment.

**Live demo:** https://maytham-altaan.github.io/pharmacy-triage-pilot/

## What it does
1. **Assessment** — 19 questions in Iraqi Arabic (WWHAM + diarrhoea-specific items).
2. **Decision** — physician referral if any referral criterion is met, otherwise pharmacy visit,
   with the triggering criteria shown to the patient.
3. **Direction** — GPS (or manual area choice) sorts demo pharmacies / physicians by distance,
   with a Google Maps route link.
4. **Follow-up** — the patient writes what the pharmacist dispensed and gets counselling on dose,
   timing, duration and side effects; outcome is recorded after the treatment timescale
   (24 h in children, 2 days otherwise).

## Referral criteria encoded
From *Community Pharmacy 2026* course notes and *Symptoms in the Pharmacy* (Blenkinsopp):
age < 3 months; > 1 day in infants < 1 y; > 2 days in children < 3 y and the elderly; > 24 h in diabetes;
> 3 days in older children and adults; ≥ 14 days (chronic); ≥ 6 stools/24 h; blood or mucus; severe or
prolonged vomiting; high fever; severe abdominal pain; any sign of dehydration; recent travel abroad;
diarrhoea with or after antibiotics; suspected drug-induced cause; IBD; immunosuppression; serious chronic
illness; pregnancy; recurrent diarrhoea or changed bowel habit; suspected food-poisoning outbreak.

## Pilot notes
- Triage is a deterministic rule set, not a language model — required so AI decisions can be compared
  against the pharmacists' gold standard (Cohen's kappa, sensitivity, specificity).
- The AI is used for the free-text counselling step, via the artifact `sample` capability. Without it the
  page falls back to a built-in medication knowledge base, so the demo works offline.
- Pharmacy and physician entries are demo data; replace `PLACES` in `index.html` with the four Wasit
  study pharmacies before fieldwork.
- "بيانات الحالة (للباحث)" in the footer exports every case as JSON for analysis. Data stays in the
  browser (localStorage); nothing is sent to a server.

Not a medical device. For research evaluation only.
