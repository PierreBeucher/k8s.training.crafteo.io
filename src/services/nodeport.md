# ClusterIP & NodePort

Example Voting App has a few services to access each component.

- Update `vote` and `result` service to use `NodePort` service type such as:
  ```yaml
  spec:
    type: NodePort
    ports:
    - name: "result-service"
        port: 5001
        targetPort: 80
        nodePort: 31001     # Mind port conflict !
  ```
- Access Vote and Result via a web browser using a Node's public IP address or hostname.
- What are `port`, `targetPort` and `nodePort` referring to?

Endpoint and EndpointSlices