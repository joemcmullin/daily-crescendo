# Email Routing & Configuration — pointer

Email routing for **Daily Crescendo** follows the studio-wide SOP, which is the
single source of truth. This repo does not duplicate the procedure or the values.

- **Procedure (how):** `Apex Development Studio LLC/Applications/Development Standards/SOP — Email Routing & Support (New App).md`
- **This app's field values (what):** `Apex Development Studio LLC/Applications/Daily Crescendo/email-routing-spec.md`

Summary: `support@dailycrescendo.com` → GoDaddy DNS (MX) → MXroute (forwarder) →
Fernand; replies go out via Postmark. The reserve form should POST to the Fernand
API once the workspace slug is set.
