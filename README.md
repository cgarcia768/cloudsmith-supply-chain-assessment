# Software Supply Chain Self-Assessment

A single-file, customer-facing questionnaire used before a Cloudsmith supply chain
assessment engagement. The customer completes it in their browser and sends the
results back; those results are imported into the Assessment Tracker, scored, and
turned into a gap findings and roadmap document.

**Live form:** https://cgarcia768.github.io/cloudsmith-supply-chain-assessment/

---

## What it covers

Nine domains, each with a short capability check (statements answered
Yes / Partly / No / Not sure) followed by one overall maturity level
(Absent / Foundational / Intermediate / Advanced) that produces the score.

1. Artifact Architecture
2. Dependency Management
3. CI/CD & Build Integrity
4. Scanning & Security Controls
5. SBOM & Provenance
6. Signing & Integrity
7. Access Controls & Identity
8. Governance & Policy
9. Vulnerability Response

Plus organisation/scope context, a framework multi-select (EU CRA, DORA, FedRAMP,
SOC 2, S2C2F, SLSA, DSOMM, NIST SSDF, ISO 27001, PCI DSS, OWASP CI/CD Top 10,
FDA 524B), the compliance driver and any fixed deadline, and the customer's own
stated priorities and constraints.

---

## How it works

`index.html` is fully self-contained — HTML, CSS, JavaScript and the logo are all
in the one file. There are no external requests, no analytics, no backend, and no
build step.

**Nothing is transmitted anywhere.** The customer's answers exist only in their
own browser tab until they choose to export them. Each visitor gets a completely
independent session, so the same link can be sent to any number of customers with
no chance of their records mixing.

Because there is no backend, the form does not save progress. It is designed to be
completed in one sitting (20–30 minutes).

### The customer's export options

| Button | What it does |
|---|---|
| **Copy answers** | Copies a tab-separated block to the clipboard, to paste into an email |
| **Download as file** | Downloads a `.json` file to attach to a reply — the most reliable option |
| **Save as PDF** | Opens the browser print dialog for a clean record of their answers |

---

## Workflow

1. Send the customer the link above.
2. They complete it and send back either the copied text or the `.json` file.
3. In the Assessment Tracker: **Cloudsmith → Import self-assessment…**, paste the
   text or choose the file, and import. This populates three tabs —
   `Self-Assessments`, `Assessment Domains`, and `Assessment Capabilities` —
   joined by a shared Import ID.
4. Generate the gap findings and roadmap document from the scored results.

The intake script lives in the Tracker's Apps Script project
(`assessment_intake.gs`), not in this repo.

---

## Updating the form

Edit `index.html`, then:

```bash
git add index.html
git commit -m "Update assessment form"
git push
```

GitHub Pages redeploys automatically, usually within a minute. The URL never
changes, so links already sent to customers keep working and pick up the new
version.

If a customer has the form open while an update is published, their in-progress
answers are unaffected — the page they are using is already loaded.

---

## Notes

- The repository must be **public** for GitHub Pages to serve it on a free
  account. The form contains no credentials, no customer data, and no internal
  information — only the questionnaire itself.
- `.nojekyll` disables GitHub's Jekyll processing, which this static file does not
  need.
- The form uses system font stacks rather than the licensed Cloudsmith brand
  typefaces, so that it renders correctly and consistently on any machine without
  redistributing font files.
