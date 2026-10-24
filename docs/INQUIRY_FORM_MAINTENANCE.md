# SlinFish Software — inquiry form maintenance

Updated: 2026-10-24

## Production integration
- Website: https://slinfish.github.io/portfolio/#contact
- Repository: `SlinFish/portfolio`
- Form markup and JavaScript: `index.html`, form ID `project-inquiry`
- Responsive styling: `style.css`
- Form provider: **Formspree** (https://formspree.io/)
- Form name: **SlinFish Project Inquiry**
- Form endpoint (public): `https://formspree.io/f/mljjdeyz`
- Recipient email configured by account owner: `slinfishsoftware@gmail.com`
- Hosting: GitHub Pages; no backend server in this repository.

## Submission behavior
The browser validates required fields and posts `FormData` using `fetch` to Formspree with `Accept: application/json`. The submit button is disabled while sending. Only a successful HTTP response with a recognized success value results in a success message; errors show a failure message. No redirect to Apple Mail is required.

Fields: name, email, company (optional), service, budget, timeline, stage, details. A hidden `_honey` anti-spam field is included. Formspree may have its own spam filtering; confirm provider behavior in the dashboard.

## Setup and verification
1. Sign in to the Formspree account associated with `slinfishsoftware@gmail.com`.
2. Confirm that **SlinFish Project Inquiry** exists and its recipient email is verified.
3. Open the live website on mobile Safari and submit a clearly labeled test with a valid email address.
4. Confirm that the website displays success and that the submission appears in Formspree's dashboard.
5. Confirm that the notification reaches the business Gmail inbox (check Spam if necessary).
6. Verify a test reply can be sent to the supplied sender address.
7. Check required-field validation, narrow-screen layout, and that service/pricing quote links scroll to `#contact`.

**Verification status: passed on 2026-10-24.** A test submission from the mobile website displayed the success message, and a Formspree notification email with subject "New submission from SlinFish Project Inquiry" was received at `slinfishsoftware@gmail.com` on 2026-10-24 at 13:32 Cambodia time. This verifies submission and email delivery for that test; continue monitoring for future failures. Dashboard inspection and reply-to behavior were not independently verified.

## Troubleshooting
- Network/cross-origin error: open https://formspree.io/ in the affected browser and check certificate trust. Test on another network if needed; do not bypass TLS warnings.
- Provider rejection: inspect Formspree's dashboard and verify the form ID, recipient address, spam settings, and account status.
- Unexpected response: check whether Formspree returned JSON and whether the endpoint is correct.
- Notification missing but dashboard has the submission: check Gmail Spam and Formspree notification settings.
- No dashboard submission: the browser request may not have reached Formspree; inspect browser developer tools or test from another device.
- If Formspree is unavailable, keep email and WhatsApp contact links working.

## Mobile styling
Legacy `.contact-section` styles conflicted with the original inquiry form, producing compressed inline fields and a visible anti-spam honeypot on iPhone. More-specific `.contact-section .contact-inner .inquiry-form` CSS now forces stacked labels and a single column below 640px and hides the honeypot. Retest after CSS changes.

## Data handling and security
Form submissions go to a third-party provider (Formspree) and are forwarded to business email. Avoid collecting passwords, payment card details, API keys, or sensitive personal information. Review Formspree's privacy policy, retention rules, and free-plan limits periodically. Keep a visible privacy notice and alternative contact options. The endpoint is public and **not a secret**; account credentials are never committed.

## Previous provider and rollback
The initial `mailto:` submission required a configured email app. FormSubmit.co was subsequently tried but failed on mobile; Safari showed a certificate trust warning for `formsubmit.co`. Do not restore that endpoint without validating its security and connectivity.

To roll back this integration, revert the Formspree migration PR or replace the endpoint with a tested alternative. Do not silently fall back to `mailto:` and call it a working online form.

## Future maintenance
- Monitor Formspree's dashboard and Gmail for failed or spam-filtered submissions.
- Revalidate after endpoint, email, DNS, or privacy-policy changes.
- Log qualified inquiries manually into the commercial pipeline after reviewing them.
- Document any future provider migration and preserve the field names for reporting.

## Lead qualification and service positioning (2026-10-24)
The homepage prioritizes three entry services: Android fixes/maintenance, backend/API integrations, and workflow automation. Custom app and software MVPs remain a fourth offer; the studio is not limited to those services. The pricing section clarifies that pilots are paid and scoped before work starts.

The inquiry form adds a required `stage` select. Existing Formspree endpoint and notification destination remain unchanged. After deployment, send a clearly labeled test to ensure the new field arrives in Formspree and Gmail. Keep the contact experience short; avoid asking visitors to upload credentials or confidential files.

### Manual lead qualification workflow
1. Review the service, project stage, problem statement, timeline and budget; verify that a real reply address is present.
2. Mark **Qualified** when the request is specific enough to discuss, appears feasible with available capacity, and has a plausible budget or a willingness to scope a paid pilot. Otherwise mark **Needs clarification**, **Not a fit**, or **Spam**.
3. For qualified leads, reply with 2–3 specific questions and propose a short discovery call or a written fixed-scope pilot. Do not promise price or start date before reviewing the requirements.
4. Record the inquiry in the existing sales pipeline, including received date, service, stage, budget range, next action, owner and follow-up date. Avoid storing private customer details in public GitHub issues.
5. For unqualified but legitimate inquiries, offer an appropriately scoped alternative or decline politely. Do not count automated messages or test submissions as sales leads.

### Maintenance checks
Confirm service buttons still navigate to `#contact`, the required `stage` field validates on mobile, and Formspree email contains the new field. The provider's free-tier limits and privacy policy should be reviewed periodically.
