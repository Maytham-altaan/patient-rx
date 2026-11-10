# Patient Rx — نموذج تجريبي للتوجيه الدوائي

A single-file prototype for the MSc proposal *Development, Validation, and Evaluation of an AI-Powered
Self-Medication Support Tool for Managing Patients with Minor Illness Symptoms* (University of Baghdad,
College of Pharmacy). Ten minor ailments are covered; diarrhoea is the fully built pilot ailment.

**Live demo:** https://maytham-altaan.github.io/patient-rx/

## What it does
0. **Complaint picker** — the patient first chooses the body area and the ailment from the 10 covered.
1. **Assessment** — Iraqi-Arabic questions: shared ones (who, age, duration, chronic illness, recurrence)
   plus the ailment's own pack. Diarrhoea carries the full WWHAM + diarrhoea-specific set (19 questions);
   the other nine run the shared engine with their own red-flag checklist.
2. **Decision** — physician referral if any referral criterion is met, otherwise pharmacy visit,
   with the triggering criteria shown to the patient.
3. **Direction** — GPS (or manual area choice) sorts demo pharmacies / physicians by distance,
   with a Google Maps route link.
4. **Expected medicines** — before the visit, the result page lists example medicines for that ailment,
   marking any that are inappropriate for the patient's age (e.g. loperamide under 12).
5. **Handoff** — the patient taps "أرسل حالتي لهنا" on the pharmacy or physician he picked. The app builds
   an Arabic case summary (every answer, the decision, the triggering referral criteria) and gives him a
   4-digit code; the target opens "شاشة الصيدلي / الطبيب", enters the code and reads the case before the
   patient walks in. In the prototype the summary is stored on the device (localStorage) and can be copied
   or sent over WhatsApp — the production version posts it to the pharmacy's own account on a server.
6. **Follow-up** — on return the patient ticks which of those medicines was actually dispensed (or types
   another), and gets counselling on dose, timing, duration and side effects, with a warning when the
   dispensed drug does not fit the age. Outcome is recorded after the treatment timescale.

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
- Adding an ailment means adding one entry to `DIS` in `index.html`: name, body area, red-flag list,
  example medicines, treatment timescale. Diarrhoea shows the depth each of the 10 reaches once its
  content is translated and approved by the expert panel.
- The AI is used for the free-text counselling step, via the artifact `sample` capability. Without it the
  page falls back to a built-in medication knowledge base, so the demo works offline.
- The study runs in **Baghdad**. Demo entries in `PLACES` (`index.html`) are placed across Baghdad
  districts — Karrada, Mansour, Kadhimiya, Adhamiya, Zayouna, Dora, Jadriya, Sadr City — and must be
  replaced with the actual study pharmacies and referral sites before fieldwork. The proposal text still
  says Wasit; Baghdad is the current plan.
- "بيانات الحالة (للباحث)" in the footer exports every case as JSON for analysis. Data stays in the
  browser (localStorage); nothing is sent to a server.

Not a medical device. For research evaluation only.
