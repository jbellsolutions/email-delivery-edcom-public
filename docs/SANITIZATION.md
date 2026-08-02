# Sanitization Notes

The private source repo contains live operational context and must not be mirrored directly.

## Exclude From Public Repos

- Live ESP URLs, sending domains, and hostnames.
- Server IPs, PTR hosts, SSH commands, SSH ports, and key paths.
- Admin emails, user IDs, customer IDs, company IDs, route IDs, warmup IDs, and API keys.
- Provider account details for VPS, DNS, mail bridge, SMTP, or proxy services.
- `.env` files, secret examples that include real names, private keys, DKIM private keys, and logs.
- Exact DNS zone state for production domains.
- Scripts that mutate live DNS, send live mail, or operate a real server.
- Customer names, campaign names, recipient data, and deliverability test outputs tied to real infrastructure.

## Safe To Publish

- General architecture.
- Placeholder-only configuration shape.
- Vendor-neutral deployment checklist.
- Deliverability principles.
- Sanitized scripts that require explicit placeholders and cannot target live infrastructure by default.

## Public Publishing Rule

Create a fresh public repo with fresh history. Do not delete sensitive files from a private repo and then push the same git history publicly.
