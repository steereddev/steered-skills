# CVE Skills
# Community maintained — add new entries, remove patched/old ones via PR
# github.com/steereddev/steered-skills

GLOBAL RULE:
Report CVEs ONLY under the resource type that owns the component.
Never report the same CVE under both deployment AND namespace.
Namespace analysis covers only: network policy, quotas, idle resources.
Deployment analysis covers: image vulnerabilities, CVEs, misconfigurations.
Each CVE must be reported as a separate issue even if multiple CVEs affect the same component.
Never merge or collapse multiple CVEs into a single issue.
Only report CVEs rated HIGH or CRITICAL. Ignore MEDIUM and LOW.

## CVE-2025-15566 | ingress-nginx | HIGH (8.8)
affects: < v1.12.5, < v1.13.1
patched: v1.12.5, v1.13.1 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE via auth-proxy-set-headers annotation injection + Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --version <patched-chart-version>
reference: https://github.com/kubernetes/kubernetes/issues/136789

## CVE-2026-1580 | ingress-nginx | HIGH (8.8)
affects: < v1.13.7, < v1.14.3
patched: v1.13.7, v1.14.3 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE via auth-method annotation injection + Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --version <patched-chart-version>
reference: https://github.com/kubernetes/kubernetes/issues/136677

## CVE-2026-24512 | ingress-nginx | HIGH (8.8)
affects: < v1.13.7, < v1.14.3
patched: v1.13.7, v1.14.3 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE via rules.http.paths.path field injection + Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --version <patched-chart-version>
reference: https://github.com/kubernetes/kubernetes/issues/136678

## CVE-2026-3288 | ingress-nginx | HIGH (8.8)
affects: < v1.13.8, < v1.14.4, < v1.15.0
patched: v1.13.8, v1.14.4, v1.15.0 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE via rewrite-target annotation injection + Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --version <patched-chart-version>
reference: https://github.com/kubernetes/kubernetes/issues/137560

## CVE-2026-4342 | ingress-nginx | HIGH
affects: < v1.13.9, < v1.14.5, < v1.15.1
patched: v1.13.9, v1.14.5, v1.15.1 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: check container image version against affected versions
signal: image tag contains version below patched threshold
impact: RCE via comment-based paths.path bypass injection + Secret disclosure
fix: helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --version <patched-chart-version>
reference: https://github.com/kubernetes/kubernetes/issues/137893

## CVE-2026-3865 | csi-driver-smb | MEDIUM (6.5)
affects: < v1.20.1
patched: v1.20.1 and above are NOT vulnerable
resource type: deployment only — never report under namespace
detect: PersistentVolumes with provisioner smb.csi.k8s.io
signal: ../ sequence in PV volumeHandle field or CSI controller logs
impact: deletion or modification of unintended directories on SMB server
fix: upgrade csi-driver-smb to >= v1.20.1 or restrict PV creation to admins
reference: https://github.com/kubernetes/kubernetes/issues/138319