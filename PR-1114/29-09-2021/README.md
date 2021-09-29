# SUMMARY

Deployment Infra | Deployments Counts | Success | Failures | Remarks
--- | --- | --- | --- | ---
AWS | 0 | 0 | 0 |
GCE | 1 | 0 | 1 | Error in ./hack/arktos-up.sh:138. 'make -j4 -C "${KUBE_ROOT}"
On-Prem | 1 | 1 | 0 | warning 'Containerd is required for Arktos'. Started containerd service manually
