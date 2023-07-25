# Edge Orchestrator

Azion **Edge Orchestrator** is an end-to-end encrypted orchestration service with cloud management and zero-touch provisioning, created for large-scale edge networks. You can manage and control resources on the edge in real time, as well as orchestrate your services quickly and easily to meet your needs.

With Edge Orchestrator you can:

- Manage and control edge resources in real time, including: provisioning, updating, and managing Edge Applications, Edge Firewalls, Edge Functions, Digital Certificates, Edge Nodes, Edge Services, and third party services via Marketplace.

- Operate and run on different types of architecture: microprocessors, like x86 and ARM and different sizes of equipment, including Raspberry PI, network equipment such as switches and SD-WAN routers as well as corporate servers, because it was designed for it.

- Use it with most network architecture, including local and public networks, and also behind NATs.

- Simplify software installation and upgrading, since it's compiled with all core and library dependencies.

---

## Implementation

| Scope | Guide |
| - | - | 
| WebAssembly | [How to create an edge function using WebAssembly on the Azion Edge platform](https://fun-cranberry.cloudvent.net/en/documentation/products/guides/webassembly-on-azion-platform/) |
| Examples | [Examples](https://fun-cranberry.cloudvent.net/en/documentation/products/edge-application/edge-functions/javascript-examples/) |
| Code samples | [GitHub repository](https://github.com/aziontech/azion-samples/tree/dev/samples) |

---


## How Edge Orchestrator works

![Orch](./orch.png)


An Azion Edge Orchestrator agent is installed on the edge nodes and provides end-to-end encrypted remote node management from the control panel [Real-Time Manager](https://manager.azion.com/) – Azion Control Panel – based in the cloud and API. 

It can be deployed in two different ways:

1. Through manual installation on each edge node.
2. Automatic installation along with the operating system: a Linux distro or the image of a client's OS or hardware supplier, for example, an SD-WAN router, a network switch or a Linux server. Customers can use an automatic registration mode, which makes it simpler to deploy (for example: new node locations or using automatic node scaling), update and manage a large number of scaling edge nodes.

All services linked to edge nodes will be orchestrated and configured from the moment the device is authorized via the control panel.

The orchestration is done sequentially and respects the dependencies between resources and triggers needed for its configuration.

---

## Edge Node

**Edge Node** enables the creation and management of devices, as well as integration with Azion. You need to install our agent so that Azion platform can orchestrate its settings and ensure secure communication between the devices and Azion.

[Learn more about Edge Node]({% tl documentation_products_edge_orchestrator_edge_nodes %})

---

## Edge Services

Edge Services enables the customer to create their own services. You can use your customized services and ensure your device is managed and orchestrated by Real-Time Manager.

[Learn more about Edge Services]({% tl documentation_products_edge_orchestrator_edge_services %})
