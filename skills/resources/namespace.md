# namespace issue guidance

## has no network policy
Namespace has no NetworkPolicy resources defined.
All pods communicate freely without restriction.
Fix: generate kubectl apply with a default-deny-all NetworkPolicy yaml.
Use the exact namespace name from THE AFFECTED RESOURCE section.

IMPORTANT:
- Only report network policy as missing if pods exist in the namespace
- Do NOT report missing ResourceQuota as an issue — quotas are optional
- Do NOT report missing LimitRange as an issue — these are optional
- Only report real security or availability issues