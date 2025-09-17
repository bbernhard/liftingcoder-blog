+++
title = "Music Button"
date = "2024-09-11T13:01:25+02:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

thumbnail = "/images/music_button_final.jpg"
tags = ["projects",]
+++

Recently I stumbled across a big arcade button on Amazon. You know, that big red buzzer buttons that people slam down in Quiz Shows if they know the answer. I always wanted to have one - even though I didn't know what to actually build with it at that point. 

{{< figure src="/images/red-arcade-button.jpg" class="center-image" width=200 alt="The Arcade Button I found on Amazon" caption="The Arcade Button I found on Amazon">}}

After the button was sitting in a drawer for several weeks, one day while listening to music, I got an inspiration: Wouldn't it be cool to slam down a button to turn the music on and off?

At my home I am using several piCorePlayer instances which form a multiroom audio system, controlled by the Lyrion Music Server (formerly known as Logitech Media Server, LMS). Fortunately LMS has a json-rpc REST API, which makes it possible to control the media server remotely.

As (most of the time) I do not care what songs are playing in my workshop, I usually use Spotify pretty much like a radio. That means, I select a song which suits my mood and let Spotify pick similar songs. This also makes it really simple to automate - all I need is a way to play/pause music when the arcade button gets slammed down.

I already mentioned that the Lyrion Music Server has an REST API. It isn't the most beautiful and intuitive API but it will get the job done. So, whenever the red button is hammered down, we need to do a REST API call which plays/pauses the music.

So far so good. But how do we do that? That's an ideal use case for one of my favorite microcontrollers: the ESP32. The ESP32 is, as the name suggests, a cheap 32bit microcontroller with WiFi capabilities, which makes it perfect for this usecase (a ESP8266 would be equally fine, but since they are equally cheap I usually just go with the ESP32 as my go-to microcontroller).

Okay, now we now know which microcontroller to use. But how should the whole thing be powered? With a power cord? I don't know...I really hate power cords for my hardware projects. They are ugly and make the whole thing less portable. So, a battery powered application it is.

That's the schematic I finally came up with:

{{< figure src="/images/music-button-schematic.png" class="center-image" alt="Schematic" caption="Schematic">}}

The cornerstone of this design lies in its self-holding circuit, enabling complete shutdown in idle mode. Once triggered by an external push button (in this case the big red button), the circuit activates, with the microcontroller taking charge of its subsequent shutdown.

The board is powered by a single 3.3V LiFePO4 battery. With its almost linear discharge curve it eliminates the need for additional voltage regulation and therefore minimizes power loss. The brains of this project is (as already mentioned) a ESP-32 microcontroller, which is due to its cheap price and the WiFi capabilities perfectly suited for that task.

Here is a rendering of the PCB that I got manufactured:

{{< figure src="/images/dashbutton_rendering.png" alt="3D rendering of the PCB" class="center-image" caption="3D rendering of the PCB">}}

Finally I've put everything inside a nice wooden frame:

{{< figure src="/images/music_button_final.jpg" alt="Music button sitting on my drawer in my workshop" class="center-image" caption="Music button sitting on my drawer in my workshop">}}

And here's a look inside the wooden frame:

{{< figure src="/images/music_button_backside.jpg" alt="A look inside" class="center-image" caption="">}}

I am really pleased with how it turned out and how much fun it is to slam the button to turn the music on. Since the circuit only draws power for a few seconds when pressed and then completely turns off a battery charge easily lasts for several months. 
