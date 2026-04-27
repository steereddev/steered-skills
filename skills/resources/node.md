# node issue guidance

## is not ready
Node is not in Ready state.
Investigate conditions and events to find root cause.
Could be disk pressure, memory pressure, or network issue.
Fix: kubectl describe node NAME to see conditions and events.
If safe to drain: kubectl drain NAME --ignore-daemonsets --delete-emptydir-data