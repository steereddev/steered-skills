# deployment issue guidance

## pods waiting: ImagePullBackOff / ErrImagePull
Image tag does not exist in the registry.
Fix: kubectl set image deployment/NAME CONTAINER=IMAGE_BASE:<valid-tag> -n NAMESPACE
Use exact CONTAINER_NAME and IMAGE_BASE from THE AFFECTED RESOURCE section.
Never use :latest as replacement tag.

## has no resource limits
No CPU or memory limits defined in container spec.
Fix: kubectl set resources deployment/NAME --limits=cpu=500m,memory=512Mi --requests=cpu=100m,memory=128Mi -n NAMESPACE
Use exact RESOURCE_NAME and NAMESPACE from THE AFFECTED RESOURCE section.

## pods are crashing / CrashLoopBackOff
Container exits and restarts repeatedly.
exitCode 1 = application error or wrong command
exitCode 137 = OOMKilled — memory limit too low
exitCode 139 = segfault

Investigation order:
1. check logs: kubectl logs deployment/NAME -n NAMESPACE --previous
2. if logs empty (container exits before writing):
   check command: kubectl get deployment NAME -n NAMESPACE -o jsonpath='{.spec.template.spec.containers[*].command}'
   check events: kubectl describe deployment NAME -n NAMESPACE
3. if OOMKilled: increase memory limits

Always check exitCode in container state to determine cause.
If exitCode 1 and logs empty → container command is wrong or missing required config.

## has 0 available pods
All pods are down.
Check events and pod states to determine cause.
If recent bad deployment: kubectl rollout undo deployment/NAME -n NAMESPACE