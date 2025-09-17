+++
title = "Useless Machine"
date = "2022-01-16T16:03:54+01:00"

thumbnail = "/images/useless-machine-case-top.jpg"
tags = ["projects"]
+++


I've always wanted to build my own useless machine. What is a useless machine you ask? It's a simple gadget with a switch that, when flipped on, immediately switches itself off. Sounds like a quirky project, right?

{{< figure src="/images/useless-machine-minecraft.gif" alt="A Useless Machine in Minecraft" class="center-image" caption="A Useless Machine in Minecraft">}}

Even though there are plenty of useless machine designs out there, I wanted mine to differ in these points: 

* The device shouldn't drain its battery when not in use.
* I wanted my useless machine to have a more human touch and play with the user a bit.
* the case should be fully 3d printed.

The first point was especially crucial for me. Nothing is more frustrating than a device languishing in a corner for months or even years, only to realize that its batteries need charging just when you're eager to engage with it.

For the hardware aspect of this project, I repurposed the schematics and PCB from another project of mine.

{{< figure src="/images/useless-machine-schematic.png" class="center-image" alt="Schematic" caption="Schematic">}}

The cornerstone of this design lies in its self-holding circuit, enabling complete shutdown when the switch is turned off. Once triggered by an external push button (in this case, the machine's switch), the circuit activates, with the microcontroller taking charge of its subsequent shutdown.

A 3.3V LiFePO4 battery powers the board, chosen for its almost linear discharge curve, eliminating the need for additional voltage regulation and minimizing power loss. The brains of this project is a ESP-12E microcontroller, admittedly oversized for this task but utilized due to availability. A smaller microcontroller, like an ATtiny, would be more efficient, but given the short operational duration, the difference is negligible.


A Micro SG90 servo operates the finger of the Useless Machine. Despite its compact size, this servo surprises with its torque, effortlessly toggling the switch.


{{< figure src="/images/dashbutton_rendering.png" alt="3D rendering of the PCB" class="center-image" caption="3D rendering of the PCB">}}

As I embarked on this project, my sole tool for constructing the case was a 3D printer. Thus, ensuring that both the case and the servo finger could be entirely printed was a priority. Intrigued by the industrial style and the weathered look of rust, I decided to experiment with metal filaments and rusting techniques.

After the rusting process the 3d printed case looks like this:

{{< figure src="/images/useless-machine-case-top.jpg" class="center-image" alt="Useless Machine Case">}}

{{< figure src="/images/useless-machine-hinge2.jpg" class="center-image" alt="Useless Machine Hinge" caption="3D Printed (and rusted) case">}}

{{< figure src="/images/useless-machine-inside.jpg" class="center-image" alt="Useless Machine Case" caption="The insides of the Useless Machine">}}
