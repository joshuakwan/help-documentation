## Overview of the Box Panel Worker/ Agent Framework

The Box Panel Worker framework helps automate many of the tasks that an Operations team member might need to perform when managing your cloud. The framework lets the operator use Box Panel as an end-to-end deployment, upgrade, management, and expansion tool, while it also functions as the system of record for each cloud under management.

As part of the Box Panel Application Suite, the Messenger Application was created to collect from Box Panel the information needed for each type of automated task, and then to send a message containing that information to the message bus (RabbitMQ) on the Site Controller.

For each BPW service, there is an Agent. The agent communicates regularly with the RabbitMQ message bus, essentially “looking” for a job for its service to carry out.

This relationship between the Box Panel Worker service, the RabbitMQ, and the Box Panel messenger is illustrated in the figure below.

![figure]({{site.baseurl}}/img/Galtenberg-BPW-Figure.png)


**Example: Reboot**

To help clarify these concepts and relationships, let’s consider an example. Suppose there’s a need to reboot a specific host. This task can be accomplished through the Box Panel Worker Framework.

Here’s a general order of steps in the process:

1. The BP messenger gathers the information about the host from Box Panel, including its IP address and login credentials for IPMI access for remote reboot.

2. The BP messenger sends a message to the Site Controller / Rabbit MQ process with the relevant information about the host and the request for a reboot service.

3. The BPW Agent, which has been monitoring the message queue (RabbitMQ), picks up the reboot request and passes it to the BPW Service for execution.
