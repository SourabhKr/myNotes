# Physical Layer

Layer 1, also known as the physical layer, is the first and lowest layer in the OSI model. It is responsible for the physical transmission of data over a communication channel, such as a wire, cable, or wireless signal. This layer defines the physical characteristics of the communication medium, including voltage levels, cable types, and signaling methods, to ensure that data is transmitted accurately and reliably between devices.

The physical layer basically physically connect two or more devices over a shared medium. The shared medium can be a copper cable, a fiber cable or even wifi. The layer set some ground rules required to use the physical medium, for example in case of copper cable, electricity will be used to transmit the data and different voltage levels can define different bits, and this can would be decided by physical layer.

In physical layer, the data is broadcasted over the shared medium. This causes anyone in the network to broadcast or listen the messages. This comes with some drawbacks:

1. No individual device addresses.
2. If multiple devices transmits at once - a collision can occur.

The devices that comes under Physical layer are:

1. Network cards
2. Hubs

An image explaining the same:
![Physical-Layer](/asset/images/networking/physical_layer.png)

----
Reference:
<https://learn.cantrill.io/courses/2022818/lectures/45636946>
