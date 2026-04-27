# pod issue guidance

## missing resource limits (standalone pod)
Standalone pod has no resource limits.
Cannot use kubectl run --limits or kubectl set resources on a standalone pod.
Fix requires delete and recreate using kubectl apply with inline yaml:

kubectl delete pod NAME -n NAMESPACE
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: NAME
  namespace: NAMESPACE
spec:
  containers:
  - name: CONTAINER_NAME
    image: CURRENT_IMAGE
    resources:
      limits:
        cpu: 500m
        memory: 512Mi
      requests:
        cpu: 100m
        memory: 128Mi
EOF

Use exact NAME, NAMESPACE, CONTAINER_NAME and CURRENT_IMAGE from THE AFFECTED RESOURCE section.
Never use kubectl run --limits flag — it does not exist.
Never use kubectl set resources on a pod — only works on deployments.

## unpinned image tag (standalone pod)
Standalone pod uses unpinned image — not managed by a deployment.
Fix requires delete and recreate with pinned tag:
kubectl delete pod NAME -n NAMESPACE && kubectl run NAME --image=IMAGE_BASE:<pinned-version> -n NAMESPACE
Use exact NAME, NAMESPACE and IMAGE_BASE from THE AFFECTED RESOURCE section.

## pod is crashing
Check logs for root cause.
Fix: kubectl logs NAME -n NAMESPACE --previous --tail=50

## pod is pending
Check scheduling constraints.
Fix: kubectl describe pod NAME -n NAMESPACE