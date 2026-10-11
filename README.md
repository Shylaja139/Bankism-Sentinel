# Bankism Defensive AI Firewall

A GitHub Pages-ready hackathon prototype that demonstrates a blue-team policy gateway between untrusted natural-language requests and a **simulated** banking ledger. It uses only fictional identities and browser-local state.

## What works
- Deterministic prompt-injection, jailbreak, obfuscation, credential, phishing, ambiguity, and unauthorized-access checks
- Structured JSON verdicts: APPROVE, BLOCK, REVIEW
- Fictional account balances and transaction history
- Exact-detail confirmation before simulated transfer execution
- Duplicate-transfer protection for the current session
- Audit log with JSON export
- Safe attack-simulator cases
- Responsive dashboard and automated policy tests

## Important boundary
This is a client-side educational simulation, **not a production banking firewall**. It has no real authentication, durable server ledger, external AI model, banking API, or payment connectivity. Client code can be modified by a user. A production implementation must enforce authorization, policy, confirmation, idempotency, rate limits, audit integrity, and transaction atomicity on a trusted backend. Never enter real customer data or credentials.

## Run locally
Open `index.html` directly, or use a local server:

```powershell
python -m http.server 8000
```

Then browse to `http://localhost:8000`.

## Run tests
Install Node.js 20 or newer, then:

```powershell
npm test
```

## Publish with GitHub Pages
1. Create an empty GitHub repository.
2. Upload all files from this project, including the `.github` folder, to the repository root.
3. In **Settings → Pages**, set **Source** to **GitHub Actions**.
4. Push to `main`. The included workflow runs tests and deploys the page.
5. The live URL appears in the workflow deployment and in **Settings → Pages**.

Command-line option:

```powershell
git init
git add .
git commit -m "Add Bankism defensive prototype"
git branch -M main
git remote add origin YOUR_REPOSITORY_URL
git push -u origin main
```

## Demo walkthrough
1. Open **Firewall** and run a benign balance inquiry.
2. Run direct prompt injection and bypass-confirmation scenarios.
3. Open **Banking Sandbox**, prepare a transfer, inspect exact details, then confirm once.
4. Try the same transfer again to observe duplicate protection.
5. Open **Audit** and export the session log.

## Security design
Analysis can classify a transfer, but it always returns `execution_allowed: false`. Transfer execution is separated into preparation and exact-detail confirmation. The ledger checks accounts, amount, balance, and a session idempotency key again immediately before mutation. Blocked or review-required messages never reach the simulated execution function.

## Known limitations
- Pattern matching can produce false positives and false negatives.
- Browser state resets on reload.
- The demo identity model is intentionally simplified.
- Client-side controls are inspectable and are not an authoritative security boundary.
- The test suite validates selected invariants, not overall security.

## Suggested production evolution
Move policy enforcement and the ledger to a trusted API; add authenticated identity and account ownership checks; use durable, tamper-evident audit records; define expiring signed confirmation tokens; implement transactional database updates; add rate limiting and monitoring; and perform independent threat modeling and penetration testing.
