---
title: Technoman UI
description: Technoman's custom UI for XBY flashlight drivers
published: true
date: '2026-11-08T23:00:00.000Z'
tags: ui, xby
editor: markdown
dateCreated: '2026-11-08T23:00:00.000Z'
---

# Technoman UI
A custom UI for XBY drivers, which are commonly fitted to [DongDongHai](/manufacturers/dongdonghai) hosts. It replaces the [XBY original UI](/user-interfaces/xby-original-ui). On drivers that have both, **7H** switches between them.

Drivers reported to ship with it include the **XBY47 v4.20** (50A buck + 350A FET) and the **XBY32 v4.25EX** (18A buck + 170A FET). See [DongDongHai drivers](/manufacturers/dongdonghai#drivers). To install it on an XBY47 v4.2, see [Flashing the XBY47 v4.2 driver](/guides/flashing-xby47-v4-2).

*Part of [User interfaces](/user-interfaces). See [Notation](/user-interfaces#notation) for what 1C and 1H mean.*

## Controls
Rows marked **changed** or **new** differ from the [XBY original UI](/user-interfaces/xby-original-ui).

| Action | Function | |
|---|---|---|
| 1H (1 second) | Regular moon | **new** |
| 1H (3 seconds) | Lower moon (has some flicker) | **changed** |
| 1C | On / off | |
| 2C | Turbo | |
| 3C | Battery check | **changed** |
| 3H | Strobe | **new** |
| 4C | Lockout | **changed** |
| 5C | Momentary mode (power cycle to exit) | |
| 6C | Toggle between ramping and stepped mode | **changed** |
| 7C | Toggle the power button light on / off | |
| 7H | Switch between the old and new UI | **new** |
| 8C | Enable / disable the fan (the button aux LED blinks to confirm) | |
| 9C | Force the fan to full power | |
| 10C | Charger voltage display | |
| 11C | Enable the powerbank function (wait for the blue indicator) | |
| 12C | Temperature display | |
| 13C | Disable automatic sleep mode | |
| 14C | Cycle buck-only modes (see below) | **new** |
| 15C | Toggle thermal regulation on / off | |
| 18C | Restore factory defaults | |
| 20C | Button aux brightness | |

### Comparison with the original UI
| Function | Original UI | Technoman UI |
|---|---|---|
| Lockout | 1H (3 seconds) | 4C |
| Moon | — | 1H (1 second) regular, 1H (3 seconds) lower |
| Battery check | 6C | 3C |
| Strobe | 4C | 3H |
| Ramping / stepped toggle | 3C | 6C |
| Buck-only modes | — | 14C |
| Switch UI | — | 7H |

## Buck-only modes
Some emitters can't handle the full current of the FET (direct-drive) turbo. For those builds, 14C limits turbo to the buck circuit. Each 14C moves to the next option, and the main LED shows which one is set:

| Press | Turbo limit | Confirmation |
|---|---|---|
| First 14C | 35A buck | The light ramps from level 1 up to the 35A turbo level, then turns off |
| Second 14C | 40A buck | The light ramps from level 1 up to the 40A turbo level, flashes twice, then turns off |
| Third 14C | 45A buck | The light ramps from level 1 up to the 45A turbo level, flashes rapidly five times, then turns off |
| Fourth 14C | FET (direct drive) | The light flashes three times at level 1 to show the original 350A direct-drive mode is restored |

> These current levels are for the 350A-FET XBY47 driver. The BLF thread lists 23 / 28.75 / 34.5A buck turbo levels for the XBY32 v4.25EX.
{.is-info}

## Sources
- UI notes from Technoman (November 2026)
- [The Unofficial DongDongHai (DDH) info thread](https://budgetlightforum.com/t/the-unofficial-dongdonghai-ddh-info-thread-and-the-dongers-lounge/232549) on BudgetLightForum
