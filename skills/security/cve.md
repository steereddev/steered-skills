# CVE Skills
# Community maintained — add new entries, remove patched/old ones via PR
# github.com/steereddev/steered-skills

GLOBAL RULE:
Report CVEs ONLY under the resource type that owns the component.
Never report the same CVE under both deployment AND namespace.
Namespace analysis covers only: network policy, quotas, idle resources.
Deployment analysis covers: image vulnerabilities, CVEs, misconfigurations.

## CVE-2026-3288 | ingress-nginx | HIGH (8.8)
affects: < v1.13.8, < v1.14.4, < v1.15.0
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE + cluster-wide Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx
     --namespace ingress-nginx --version <patched-version>
reference: https://github.com/kubernetes/kubernetes/issues/137560