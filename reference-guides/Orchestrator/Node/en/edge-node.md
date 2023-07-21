---
title: Edge Node
description: Azion Edge Node enables you to create your own edge infrastructure, allowing you to install services and resources in real time.
meta_tags: Azion Edge Node, Edge Computing
namespace: documentation_products_edge_orchestrator_edge_nodes
permalink: /documentation/products/edge-orchestrator/edge-node/
---

Azion **Edge Node** enables you to create your own edge infrastructure, allowing you to install services and resources in real time.

It is an open software which can be run on different types of microprocessor architecture: x86 and ARM, and different sizes of equipment, including Raspberry PI, network equipment such as network switches and SD-WAN routers as well as corporate servers.

---

## Agent commands and options

The Edge Orchestrator agent has additional commands and options to make it easier to use.

|  | Description |
| :--- | :--- |
| --debug or -d | It sets the agent logs to debug mode. |
| --help or -h | It helps on the commands that the agent can execute. |
| install | It installs the agent to the client’s device, copies the binary to the installation location; adds the Edge Orchestrator agent to the device's service manager (if any) and; sets up credentials to authenticate the Edge Node. |
| start \[--foreground\] | It initializes the Edge Orchestrator agent through the device's service manager.<br /> Note: The foreground option is used to run it in the foreground. |
| start -g OR --join-group | By using these flags followed by a comma separated list of group names, you can enroll your edge-node with the specified group(s) through commandline while starting your node for the first time. <br/> Example: sudo edge-orchestrator start -g GROUP1,GROUP2,GROUP3 --foreground |
| start \[-n OR --set-name\] | By using these flags followed by the desired name, you can specify your new node’s name through commandline while starting your node for the first time . By not using them, the hostname is used as default value. <br/> Example: sudo edge-orchestrator start -n Edgenodename --foreground |
| status | It reports on the status of the execution of the Edge Orchestrator agent. |
| stop | It stops the Edge Orchestrator agent through the device's service manager. |
| uninstall | It uninstalls the agent from the client’s device, removes the binary from the installation location; removes the Edge Orchestrator agent from the device's service manager (if any).<br />Note: authentication credentials remain on the device and can be removed using the Azion control panel. |
| --version or -v | It displays the installed version of the agent. |

---

## Watcher

To avoid any configuration changes to the resources managed by Orchestrator, the agent provides a feature called **Watcher**.

It's a non-manageable feature of Azion agent that restores any tampered file. It consists of a group of *workers* that periodically scan all provisioned files looking for any drift—modification or removal—based on the last applied manifest, restoring the desired state, if necessary.

You can verify any action made by Watcher by looking at the *logfile* `/var/log/azion/edge-orchestrator.log`.

```
    # /var/log/azion/edge-orchestrator.log
    {"level":"info","time":"2021-09-22T17:31:16Z","message":"finished applying resources for version 3128"}
    {"level":"info","time":"2021-09-22T17:31:16Z","message":"apply manifest 3128 finished"}
    {"level":"info","time":"2021-09-22T17:31:16Z","message":"watcher: started with period of 60 seconds using 5 workers"}
    {"level":"info","time":"2021-09-22T17:32:16Z","message":"watcher: dispatching workers"}
    {"level":"info","time":"2021-09-22T17:32:16Z","message":"watcher: dispatched 5 workers"}
    {"level":"info","time":"2021-09-22T17:32:16Z","message":"watcher: workers finished"}
    {"level":"info","time":"2021-09-22T17:32:16Z","message":"watcher: checked 19576 artifacts, 0 drifted from manifest."}
```