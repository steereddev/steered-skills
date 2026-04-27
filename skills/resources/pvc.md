# pvc issue guidance

## is unattached and billing
PVC is not mounted by any pod and is incurring storage costs.
Verify it is safe to delete before proceeding.
Fix: kubectl delete pvc NAME -n NAMESPACE
Use exact NAME and NAMESPACE from THE AFFECTED RESOURCE section.