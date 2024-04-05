+++
title = "Mindful Picture Frame"
date = "2021-07-28T10:01:25+02:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["projects",]
+++

Who knows this problem? Over the years, one has accumulated gigabytes of photos, capturing a snapshot of every moment worth remembering, only to hardly ever look at the photos again. That's how it was for me too - on my Nextcloud Share, there are tens of thousands of photos, neatly organized and sorted, condemned to gather digital dust.

But I wanted to change that. And thus, the Mindful Picture Frame was born. The idea is quite simple: I want a digital, battery-powered photo frame based on an E-ink display, which shows a photo taken exactly x years ago today. Although an E-ink display is notoriously ill-suited for displaying images compared to other display technologies, its use was a deliberate choice.

On one hand, it allowed me to operate the picture frame on battery power (with a runtime of several months), and on the other hand, the black-and-white, poorly resolved images remind me of pictures from old newspapers.

The project was divided into two parts: the actual picture frame and the "server component."

## The Picture Frame

For the picture frame, I used the [Inkplate 6](https://www.crowdsupply.com/soldered/inkplate-6) Display Board from Soldered Electronics. This is a recycled 6'' Kindle E-paper Display, which is controlled by an ESP32 and can be powered by an external 3.3V battery. According to the product description of the Inkplate 6 board, it only requires 25uA in deep sleep mode, making it ideal for battery-powered operation over months. Unfortunately, my board had a defect and consumed significantly more power in deep sleep mode than stated by the manufacturer, causing the 3.3V 18650 battery I used for power to drain within a few weeks.

To fix the problem, I designed a small "Wake-Up-PCB" based on the ATtiny10 (which requires only a few nanoamperes in deep sleep mode).

{{< figure src="/images/wakeup-board-schematic.png" class="center-image" alt="Wake-Up Board Schematic" caption="Wake-Up Board Schematic">}}

The sole duty of the ATtiny microcontroller is to awaken every 30 minutes and trigger a MOSFET, thereby supplying power to the Inkplate board for approximately 10 seconds, enabling it to update the image. Due to the ATtiny10 predominantly residing in deep sleep mode and the Inkplate board remaining entirely dormant, a runtime exceeding 6 months can be attained with a 3.3V 2500mAh battery, while ensuring the image is refreshed every half hour.

{{< figure src="/images/wakeup-board-rendering.png" class="center-image" alt="Wake-Up Board 3D Rendering" caption="Wake-Up Board 3D Rendering">}}

For the frame, I aimed for a simple wooden design to amplify the nostalgia. With only a 3D printer available at the time, I experimented with a wood-fiber filament and wood staining.  Apart from the significantly lighter weight of the faux-wood frame, in my opinion, it closely resembles a real wooden frame.

{{< figure src="/images/mindful-picture-frame.jpg" class="center-image" alt="Mindful Picture Frame" caption="The Picture Frame in all its glory (with a picture that was taken 13 years ago)">}}

## The Server Component

To update the image on the digital picture frame, the Inkplate board connects via WiFi to a locally running [Mindfulbytes Server](https://github.com/bbernhard/mindfulbytes) and retrieves the image to display via REST. Mindfulbytes is a plugin-based application I wrote, which collects all locally available digital assets and provides them, along with their associated metadata (e.g., EXIF metadata), via REST. This makes it easy to retrieve either a random image or an image taken on that day via REST and display it on the Inkplate 6.
