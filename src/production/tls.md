# Ingress with TLS (HTTPS)

`resources/https` contains an Ingress resource configured with TLS (HTTPS) and a [Cert Manager](https://github.com/cert-manager/cert-manager) Certificate.

Deploy this Ingress and Certificate along with Example Voting App
- Make sure Example Voting App is deployed
- Deploy resources in `resources/https`. **You must replace `<YOUR_NAME>` in YAML files by your own name. **
- Observe creation of Ingress and Certificate resources
- Test functionnality. The Ingress should be reachable externally. 