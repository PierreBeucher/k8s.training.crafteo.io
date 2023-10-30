# Advanced Services concepts

## Endpoints and EndpointSlices

Services uses EndpointSlices (and Endpoints) under the hood to redirect traffic.

- Scale Vote deployment to 3 replicas
- Identify EndpointSlices and Endpoints created for Vote service

Historically, Endpoints were used to link Services to Pods. EndpointSlices provide a more complete API and will eventually replace Endpoints. See [Kubernetes doc for details](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/#motivation)

## Headless Services

Headless services can be used when load balancing is not required for Services. Headless services won't have any IP.

Using selectors, internal DNS query will directly return all IPs from existing pods.

- Scale Vote and Service deployments to 3 replicas
- Delete Vote service
- Update Vote service template with `spec.clusterIP: "None"`
- Re-deploy Vote service
- Execute a shell in Vote Pod and observe DNS record behavior between `vote` and `result` service

```
# Install DNS utils on the fly for testing
apt update && apt install dns-utils

nslookup vote
nslookup result
```

## Service discovery

Services are exposed to Pods via environment variables. 

- Execute a shell in Vote pod and explore available services
  - Use `env` to show all environment variables, and `env | grep` to filter
- Find Result service environment variables 

A more common approach is to use DNS records pointing to Services.