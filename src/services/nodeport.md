# NodePort

Example Voting App has a few services to access each component.

- Update `vote` and `result` service to use `NodePort` service type such as:
  ```yaml
  spec:
    type: NodePort
    ports:
    - name: "result-service"
        port: 5001
        targetPort: 80
        # Mind port conflict !
        # Since we're all on the same cluster, 
        # everyone needs to use different ports. 
        # Use a port between 31000 and 36000
        nodePort: 31001
  ```
- Access Vote and Result via a web browser using a Node's public IP address or hostname.
  - Even if Node port is open and listening, we also need a network and firewall rules to accept incoming traffic 
- What are `port`, `targetPort` and `nodePort` referring to?