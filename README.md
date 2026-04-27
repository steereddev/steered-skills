# steered-skills

> v2.0.0

Community knowledge base for [steered](https://github.com/steereddev/steered) —
the single binary Kubernetes advisor.

> Single binary. Zero setup. No cloud.
> Probes your live cluster, finds issues, guides you to the exact fix.
> Never changes your cluster.

---

## Update your skills

```bash
steered --update-skills
```

No binary update needed. Skills load on next run.

---

## Structure

```
skills/
  base.md                    # core AI instructions and principles
  resources/
    deployment.md            # deployment issue guidance
    pod.md                   # pod issue guidance
    namespace.md             # namespace issue guidance
    node.md                  # node issue guidance
    ingress.md               # ingress issue guidance
    pvc.md                   # pvc issue guidance
  security/
    cve.md                   # known CVE advisories
  community/                 # community contributed skills
```

---

## Contributing

No Go knowledge needed. Just edit a markdown file and submit a PR.

### Add a new CVE

```
1. open skills/security/cve.md
2. copy an existing CVE block
3. fill in the new CVE details
4. submit PR
```

### Add a new resource type

```
1. create skills/resources/statefulset.md
2. describe common issues and fixes
3. submit PR
```

### Fix existing guidance

```
1. edit the relevant .md file
2. submit PR
```

PRs reviewed within 24 hours.

---

## How it works

steered reads skills files on every run and passes them to the LLM as context.
The LLM uses this knowledge to detect issues and generate accurate fix commands.

```
steered starts
      ↓
loads ~/.steered/skills/
      ↓
collector probes live cluster
      ↓
LLM analyzes with skills context
      ↓
finds issues, guides to exact fix
```

---

## steered.dev

[steered.dev](https://steered.dev) · [GitHub](https://github.com/steereddev/steered) · MIT License