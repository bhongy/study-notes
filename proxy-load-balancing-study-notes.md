## Proxy Server Tasks

- service discovery: what backends are available, what are their addresses
- health checking: what backends are healthy and available to accept requests
- load balancing: algorithm to use for balancing individual requests

## Benefits

- name abstraction: refer to backend group by name rather than knowing addresses
- fault tolerance: route around bad backend and transparently replace it
- system is likely span across network zones and regions - good balancing will keep the traffic within the same zone as much as possible (smaller latency) and lower cost

- load balancer and proxy is used interchangeably in the industry
- avoid sticky sessions
- observability: numeric stats, distributed tracing, and customizable logging
- security: rate limiting, authentication, and DoS mitigation
- To avoid the single point of failure and scaling issues inherent in middle proxy topologies, more sophisticated infrastructures have moved towards embedding the load balancer directly into services via a library

- deploying library upgrades across a large service architecture can be extremely painful, making it highly likely that many different versions of the library will be running concurrently in production, increasing operational cognitive load