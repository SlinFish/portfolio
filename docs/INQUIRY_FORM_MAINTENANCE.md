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

Fields: name, email, company (optional), service, budget, timeline, details. A hidden `_honey` anti-spam field is included. Formspree may have its own spam filtering; confirm provider behavior in the dashboard.

## Setup and verification
1. Sign in to the Formspree account associated with `slinfishsoftware@gmail.com`.
2. Confirm that **SlinFish Project Inquiry** exists and its recipient email is verified.
3. Open the live website on mobile Safari and submit a clearly labeled test with a valid email address.
4. Confirm that the website displays success and that the submission appears in Formspree's dashboard.
5. Confirm that the notification reaches the business Gmail inbox (check Spam if necessary).
6. Verify a test reply can be sent to the supplied sender address.
7. Check required-field validation, narrow-screen layout, and that service/pricing quote links scroll to `#contact`.

**Current verification status: pending live end-to-end test.** Do not claim that customer inquiries are delivered until steps 3–5 are confirmed.

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
