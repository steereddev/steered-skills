# ingress issue guidance

## has no TLS configured
Ingress has no TLS configuration — traffic is unencrypted.
Fix requires two steps:
Step 1: create TLS secret:
  kubectl create secret tls NAME-tls --cert=<path/to/cert> --key=<path/to/key> -n NAMESPACE
Step 2: patch ingress to add TLS:
  kubectl patch ingress NAME -n NAMESPACE --type=merge -p '{"spec":{"tls":[{"hosts":["INGRESS_HOST"],"secretName":"NAME-tls"}]}}'
Use exact NAME, NAMESPACE and INGRESS_HOST from THE AFFECTED RESOURCE section.