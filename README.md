# Kubernetes Secrets

Secrets in k8s are a way to store secret values that will be used by pods, controllers, etc.

By default the secrets are stored in plain text just encoded in base64.

There are some best pratices when dealing with secrets at production level, each one have their own pros and cons, from the limitation and manual intervation to the overhead to setup and maintain.

- [etcd encryption at rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)
- [SOPS (git + age)](github.com/getsops/sops)
- [external secrets operator](https://external-secrets.io/latest/)
- [Secrets Store CSI Driver](https://secrets-store-csi-driver.sigs.k8s.io/)

## SOPS (git filter + age)

### Age

Age is a simple encryption tool that can be used to encrypt and decrypt our secrets. For more detail information look at their [documentation](https://github.com/FiloSottile/age).

```bash
age-key -o key.txt
age -r age17wrvunvmx52augeju9635ad86mtva7hndp8rv37lm7t6k7a2jpmqqtz3re -o secrets.txt.age secrets.txt
age -d -i key.txt -o decrypted-secrets.t secrets.txt.age 
```

### SOPS

SOPS is a cli and editor to help encrypt files of json, yaml, ini formats using different sources of encryption like aws kms, gpg, age, etc.

```bash
kubectl create secret generic --dry-run=server my-secret -o yaml --from-literal=foo=bar > secret.yaml
sops -i -e secret.yaml
sops decrypt secret.yaml
```

# References

- [Base64 Is NOT Encryption! Kubernetes Secrets Exposed by Mischa van den Burg](https://www.youtube.com/watch?v=mSJXn6XdEr0)
- [Protect secrets in Git with the clean/smudge filter](https://developers.redhat.com/articles/2022/02/02/protect-secrets-git-cleansmudge-filter)
- [A hidden gem of Git: clean/smudge filter](https://medium.com/@dimst23/a-hidden-gem-of-git-clean-smudge-filter-6c27bee20081)
- [age is a simple, modern and secure file encryption tool, format, and Go library.](https://github.com/FiloSottile/age)
