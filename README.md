# What is Service Mesh?
- A `service mesh` is a platform layer on top of the infrastructure layer that enables managed, observable, and secure communication between individual services.
- They are transparent to the application. The service mesh monitors all traffic trough a proxy, this proxy is deployed by a `sidecar patern`.
- The Service Mesh provides:
  - Service Discovery
  - Observability (metrics)
  - Rate Limiting
  - Circuit Breaking
  - Traffic Shifting
  - Load Balancing
  - Authentication and Authorization
  - Distributed Tracing

>## Diagram example using [Istio Service Mesh](https://istio.io/latest/about/service-mesh/)
>  - Communication before Service Mesh:
>    - ![image](https://user-images.githubusercontent.com/114915009/193802207-8ad36fb7-5fa9-4c94-9678-11f5c83e954a.png)
>  - Communication after Service Mesh:
>    - ![image](https://user-images.githubusercontent.com/114915009/193802366-2f8a72e8-63fb-47f1-ac14-34e80e2f787a.png)

# Architecture
- At a basic level, a service mesh consists of services and proxies running as sidecars to the services. It also includes some authority that configures those proxies to combine the proxies and services into a proper distributed system, including a `data plane` and a `control plane`. 
- All requests to or from a service, pass through two proxies within the mesh: 
  - The proxy for the calling service.
  - The proxy for the receiving service.
- This abstracts all functions that are not related to the business logic away from services. There are 2 planes:
  -  ![image](https://user-images.githubusercontent.com/114915009/193798805-40433034-62b0-4804-9920-c635df7e399a.png)
  - ## Control Plane
    - ### The service mesh control plane enables the proxies to perform the following functions:
      - Service discovery
      - Service routing
      - Load balancing
      - Authentication and authorization
      - Observability
    - ### The control plane is responsible for the following:
      - #### Service Registry:
        - The control plane must have a list of available services and endpoints to provide them to the proxies.
        - Compiles this registry by querying the underlying infrastructure scheduling system, like `Kubernetes`, to get a list of all available services.
      - #### Sidecar Proxy Configuration
        - The configuration of sidecar proxies includes policies and mesh-wide configurations that the proxies need to be aware of to appropriately perform their functions.
    - Too check a diagram with services that interact with the `control plane`, check [proxies running as sidecars](https://hackernoon.com/service-mesh-with-envoy-101-e6b2131ee30b) 
  - ## Data Plane
    - In contrast to the control plane, which determines how packets should be forwarded, the data plane actually forwards the packets. The `data plane` is also called the `forwarding plane`.
 
![image](https://user-images.githubusercontent.com/114915009/193803761-82be04a7-adba-468e-a418-8c268858dfe3.png)
>For example, the `control plane` is the stoplights that operate at the intersections of a city. Meanwhile, the `data plane` (or the `forwarding plane`) is more like the cars that drive on the roads, stop at the intersections, and obey the stoplights.
