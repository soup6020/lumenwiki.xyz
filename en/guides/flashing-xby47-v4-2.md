---
title: Flashing the XBY47 v4.2 driver
description: >-
  How to flash the Technoman UI or default firmware onto the 47mm XBY v4.2
  driver
published: true
date: '2026-11-09T01:44:18.575Z'
tags: []
editor: markdown
dateCreated: '2026-11-09T00:00:00.000Z'
---

# Flashing the XBY47 v4.2 driver
This guide covers flashing the 47mm XBY v4.2 driver used in the big [DongDongHai](/manufacturers/dongdonghai) hosts (D6F, D7F, D8, D8DF, F8B). You can install the [Technoman UI](/user-interfaces/technoman-ui) or restore the v4.2 default settings.

> **This only works with the 47mm v4.2 driver. Do not flash any other driver with this software.**
{.is-danger}

*Part of [Guides](/guides).*

## What you need
| Item | Notes | Example |
|---|---|---|
| USB-serial adapter | Any common adapter works. A CH340 adapter costs a few dollars and is fine. | [Adapter used by Technoman](https://www.amazon.com/dp/B0DLGN14T6) (more advanced than a CH340) |
| SOP8 4.4mm pogo-pin probe | Used to touch the programming pads on the driver | [Probe used by Technoman](https://www.amazon.com/dp/B0DPFXQL9Q) |
| Flashing software | Windows program (.exe) | [Google Drive folder](https://drive.google.com/drive/folders/1GcXeJJPlQc7lIDeoQrTkjoAtc5OmHAw3) |

### Using an Arduino as the adapter
An Arduino Nano or Uno (both ATmega328P boards) has also been used successfully as the USB-serial adapter, at both **3.3V** and **5V**:

| Board | USB-to-UART chip |
|---|---|
| Arduino Nano (generic) | CH340G |
| Arduino Uno (generic) | CP2104 |

- Install the latest USB driver for the board's chip (CH340 or CP210x). Both boards needed the newest drivers.
- On at least one board, TX and RX had to be swapped. This is normal for UART. If flashing this way doesn't work, try swapping them.

## Wiring
The driver has four programming pads, marked **V**, **G**, **T** and **R**. Trace which probe pin lands on each pad, then wire the probe to the adapter:

| Driver pad | Adapter pin | Purpose |
|---|---|---|
| V | Power (positive) | Powers the driver |
| G | Ground | Ground |
| T | RX | Driver transmit → adapter receive |
| R | TX | Adapter transmit → driver receive |

TX and RX cross over: the driver's **T** goes to the adapter's **RX**, and **R** goes to **TX**.

Both **3.3V** and **5V** on the V pad have been reported to work (tested with Arduino boards, see above).

## Software
1. Download the software from the [Google Drive folder](https://drive.google.com/drive/folders/1GcXeJJPlQc7lIDeoQrTkjoAtc5OmHAw3).
2. Extract the zip. It is password-protected, and the password is in the file name.
3. The zip contains three files:
   - **Instructions**
   - **v4.2 default settings**: restores the stock firmware settings
   - **New UI**: the [Technoman UI](/user-interfaces/technoman-ui)
4. Rename the file you want to flash so it ends in `.exe`.
5. Run that file. Most of the interface is in Chinese, but the important buttons are in English.

## Flashing
1. Connect the USB-serial adapter to your computer.
2. In the flashing program, click **Start**.
   > Click **Start** *before* the probe touches the pads, or flashing won't work.
   {.is-warning}
3. Touch the probe to the pads on the driver. Ideally **T** and **R** make contact first, before power (**V** and **G**).
4. Wait a few seconds. Flashing is then complete.

Once it's flashed, you can use 7H to switch between the [Technoman UI](/user-interfaces/technoman-ui) and the [XBY original UI](/user-interfaces/xby-original-ui).

## Sources
- Flashing notes from Technoman (November 2026)
- Additional notes from a community member on start order, pad contact order and using Arduino boards (November 2026)
