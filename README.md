# Object Detection BrightSign Model Package (BSMP) Demo using a BA:connected Presentation

This demo BA:con presentation showcases the tech behind the NPU that is enabled in Brightsign players.  This demo shows:

- Full motion video playing as an attract loop
- If a cup is detected in the camera view, a Starbucks video plays
- If a phone is detected in the camera view, a Samsung phone video plays

> **Looking for a complete solution?**
> [**Argus**](https://github.com/brightsign/argus-audience-measurement-extension) is BrightSign's
> reference audience-measurement application: person counting, gaze detection, dwell time,
> entry/exit events, and movement analytics, published over MQTT and Prometheus. This repository
> is a single-purpose example of one piece of that system.
>
> *For production audience analytics rather than a demo presentation, use Argus.*

## Just Use It!

1. ensure you have all the pre-requisites per the [BSMP](https://github.com/brightsign/brightsign-npu-object-extension)
2. copy the contents of the 'sd' folder to an SD card
3. download the BSMP (.bsfw) from the [latest BSMP release](https://github.com/brightsign/brightsign-npu-object-extension/releases/latest) and copy it onto the SD card
4. place the SD card into the player and boot

## Building

To use this you will need to have BrightAuthor:connected (BA:connected) installed.  You can open the presentation in the [preso](./preso/) folder.

Media for this presentation is in the [media](./media) folder.

## Ensure the BSMP is Installed

If your player needs the extension installed, include the [bsfw installation package](https://github.com/brightsign/brightsign-npu-object-extension/releases/latest) on the root of the SD card and it will be automatically installed on the next boot.

This BSMP is released as an ALPHA quality only.

## Licensing

This project is released under the terms of the [Apache 2.0 License](./LICENSE.txt).
