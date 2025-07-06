# Kubernetes Secrets

Secrets in k8s are a way to store secret values that will be used by pods, controllers, etc.

By default the secrets are stored in plain text just encoded in base64.

There are some best pratices when dealing with secrets at production level, each one have their own pros and cons, from the limitation and manual intervation to the overhead to setup and maintain.

- [etcd encryption at rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)
- [SOPS (git + age)](github.com/getsops/sops)
- [external secrets operator](https://external-secrets.io/latest/)
- [Secrets Store CSI Driver](https://secrets-store-csi-driver.sigs.k8s.io/)

# References

- [Base64 Is NOT Encryption! Kubernetes Secrets Exposed by Mischa van den Burg](https://www.youtube.com/watch?v=mSJXn6XdEr0)
