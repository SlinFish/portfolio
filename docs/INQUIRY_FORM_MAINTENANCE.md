# SlinFish Software — website inquiry form maintenance

Last updated: 2026-10-24

## Purpose and implementation
The public business site is a static GitHub Pages website at https://slinfish.github.io/portfolio/. The source is in this repository. The inquiry form lives in `index.html` under `#contact`, with styles in `style.css`.

The initial version opened a visitor's email app using `mailto:`, which was unsuitable for visitors without an email client configured. It has been replaced with a direct AJAX submission to **FormSubmit.co** (not FormSubmit.io or FormSubmit.app).

- Endpoint: `https://formsubmit.co/ajax/slinfishsoftware@gmail.com`
- Recipient: `slinfishsoftware@gmail.com`
- Frontend: vanilla JavaScript `fetch`, no build tools or additional dependencies
- Form fields: name, email, company (optional), service, budget, timeline, project details
- Anti-spam: `_honey` honeypot; provider-side spam protection may also apply
- Browser: validates required fields; disables button while sending; shows success only when the provider explicitly reports success; shows an error otherwise
- Email and WhatsApp remain available as fallback contact methods.

## Required one-time activation — NOT YET VERIFIED
FormSubmit requires the recipient to verify ownership of the email address before submissions are delivered.

1. Open the published website at https://slinfish.github.io/portfolio/#contact.
2. Fill in the form with **clearly labeled test data**; do not use a real prospect's details.
3. Submit. The provider should send an **Activate Form** message to `slinfishsoftware@gmail.com`.
4. In that inbox, find the activation email (check Spam) and click the confirmation link.
5. Return to the site, submit another test inquiry, and verify it arrives in the business inbox.
6. Confirm the website shows success only when the provider accepts the submission.

**Until activation and the end-to-end test are confirmed, do not claim the form is operational or that customer inquiries are reliably delivered.** The page displays an activation-specific error when the provider reports it.

## Operational checks
- On mobile Safari and desktop Chrome, open `/#contact` and check layout and required-field validation.
- Send a test inquiry; verify email receipt and reply-to address.
- Verify the form does **not** open Apple Mail or Gmail.
- Confirm buttons under services and pricing scroll to `#contact`.
- Confirm fallback email address and WhatsApp still work.
- Check Spam and provider delivery if submissions stop arriving.
- Do not submit passwords, payment credentials, private API keys, or other sensitive information.

## Failure handling
- A network failure, unexpected JSON response, or provider rejection displays a delivery failure. It must never be treated as success.
- FormSubmit sometimes returns HTTP 200 with `success: "false"` (a string). The code explicitly checks `String(result.success).toLowerCase() === "true"`.
- If FormSubmit is down or blocks traffic, visitors should use the direct email or WhatsApp links.
- Never log form contents to browser analytics or public repositories.
- If the recipient address changes, update the AJAX endpoint and re-activate with the new address.

## Data and privacy
Visitor submissions are sent to the third-party provider FormSubmit.co for email delivery; the site itself has no database. The provider documents a 30-day submission archive. Review the provider's terms and privacy policy before relying on it for customer data. The page warns visitors not to submit secrets. No paid plan or marketing expenditure is required for this setup.

## Future improvements
- Add a privacy notice linking to the provider's privacy policy and stating the expected use of inquiry data.
- Evaluate a provider with domain restrictions, rate limiting, a dashboard and export if inquiry volume grows.
- Track qualified inquiries in the SlinFish sales spreadsheet **after** human review; do not automatically add untrusted form submissions to the pipeline.
- Consider a first-party backend later if privacy, auditability or reliability requires it.

## Relevant changes
- Original inquiry form: PR #1.
- Remaining quote links redirected to form: PR #2.
- AJAX provider integration and maintenance notes: this PR.

## Rollback
Revert the AJAX integration PR through GitHub if necessary; this restores the earlier `mailto:` form behavior, which is a fallback but not a fully functional online inquiry form. Prefer keeping visible direct email and WhatsApp options if the provider fails.

## Reference
Provider documentation: https://formsubmit.co/documentation and https://formsubmit.co/ajax-documentation
