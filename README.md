# Thesis Repository

This repository contains configurations to accompany my thesis. It includes modified Helm values for Falco, a Pod configuration with a HostPath volume, and a Secret configuration. Please refer to the thesis for more information.

## Repository Contents

1. **Helm Values for Falco**
   - `falco-helm-values.yaml` can be used when installing Falco. The documentation (https://falco.org/docs/getting-started/learning-environments/#falco-with-multiple-sources) makes use of a Helm values file provided by Falco (https://raw.githubusercontent.com/falcosecurity/charts/master/charts/falco/values-syscall-k8saudit.yaml), and we modify this to exclude loading default rules and load our custom selected rules instead (in addition to the overrides specified in the documentation (`--set driver.kind=modern_ebpf` and `--set tty=true`).
   - _Note: In the Create Sensitive Mount Pod rule, to alert for _any_ host mount, the **exists** operator should be used instead of the **intersects** operator with a list, which only alerts for exact matches._
2. **Pod Configuration with HostPath**
   - A Pod configuration that mounts a sensitive directory using `hostPath` to simulate generating the respective alert. It can be applied using `kubectl apply -f hostpath-pod.yaml`. _Note: This is the correct version compared to the listing in the thesis._

3. **Secret Configuration**
   - A Kubernetes Secret configuration to simulate scenarios where Falco can detect sensitive access to secrets. It can be applied using `kubectl apply -f secretconfig.yaml`.
