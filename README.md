# Email Delivery edcom Public

Sanitized public starter for a self-hosted EmailDelivery.com Community Edition deliverability stack.

The private `email-delivery-edcom` repo contains live infrastructure details, operational credentials references, server IPs, domains, admin identity, customer IDs, and runbooks for a real deployment. This public repo keeps only the reusable implementation pattern and safety guidance.

## What This Is

A clean public reference for building a self-hosted ESP/MTA setup around EmailDelivery.com CE (`edcom-ce`) with dedicated sending infrastructure, DNS authentication, warmup discipline, and deliverability checks.

Use this as a planning and implementation scaffold, not as a live deployment dump.

## Architecture Pattern

```text
Platform / ESP UI
  - Admin portal
  - Customer accounts
  - Postal routes
  - Delivery policies
  - Reporting

Dedicated Sending MTA
  - Own IP
  - Port 25 verified
  - PTR / HELO aligned
  - SPF, DKIM, DMARC, MX published
  - Warmup policy enforced

Optional Gray Lane
  - Separate IP
  - Separate sending domain
  - Separate customer/account route
  - Used only for lower-trust re-engagement after suppression
```

## Deployment Principles

- Prove outbound port 25 before building on any provider.
- Use one clean dedicated IP per sending lane.
- Keep clean traffic and re-engagement traffic separated.
- Match PTR, HELO, SPF, DKIM, DMARC, and MX before sending.
- Warm up only with engaged contacts.
- Never mix verification, scraping, or proxy egress with sending infrastructure.
- Keep credentials in a private secret store or ignored local environment file.
- Treat customer accounts, API keys, route IDs, and warmup state as private operating data.

## Safe Public Files

- [docs/DEPLOYMENT-TEMPLATE.md](docs/DEPLOYMENT-TEMPLATE.md) - generalized deployment checklist.
- [docs/SANITIZATION.md](docs/SANITIZATION.md) - what must stay out of public repos.
- [.env.example](.env.example) - placeholder-only configuration shape.

## Public vs Private

This public repo intentionally excludes:

- Live hostnames and IP addresses.
- Admin login details.
- SSH commands tied to a real server.
- Customer IDs and account names.
- API keys, passwords, private keys, DKIM private material, and provider credentials.
- Exact production DNS zone state.
- Scripts that directly operate a live server.

## License

MIT. Check upstream EmailDelivery.com CE licensing and provider terms before deployment.
