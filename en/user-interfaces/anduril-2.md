---
title: Anduril 2
description: Anduril 2, the open-source flashlight firmware and UI by ToyKeeper
published: true
date: '2026-11-09T23:24:45.116Z'
tags:
  - ui
  - anduril
editor: markdown
dateCreated: '2026-11-09T23:30:00.000Z'
---

# Anduril 2
**Anduril 2** is open-source flashlight firmware by ToyKeeper, released under the GPL v3. It is used on many enthusiast lights, including Emisar, Noctigon, Fireflies, Sofirn and Wurkkos models, and on hobbyist drivers such as INeedMoreLumens' [DongDongHai](/manufacturers/dongdonghai#drivers) drivers.

It has two interfaces:
- **Simple UI:** the default. It limits the brightness range and hides advanced features, so the light is safe to lend to someone.
- **Advanced UI:** everything else, including strobes, configuration menus and aux LED settings.

*Part of [User interfaces](/user-interfaces). See [Notation](/user-interfaces#notation) for what 1C and 1H mean.*

> Many features depend on the light's hardware and firmware version, and default values vary between lights. The [official manual](https://github.com/ToyKeeper/anduril/blob/trunk/docs/anduril-manual.md) by ToyKeeper should be the go-to for reference, but manufacturers may override certain behaviour.
{.is-info}

## Diagram
![Anduril 2 UI diagram](/images/user-interfaces/anduril-2-diagram.png)

*[Anduril 2 UI diagram](https://github.com/dirtydancing/anduril-tikz-diagram) by dirtydancing, for Anduril 2 release 2026-10-26, licensed under the [GPL v3](https://github.com/dirtydancing/anduril-tikz-diagram/blob/main/LICENSE). The source and a printable PDF are on the [releases page](https://github.com/dirtydancing/anduril-tikz-diagram/releases).*

## Quick start
| Action | Function |
|---|---|
| 1C | On / off |
| 1H | Ramp brightness up. Release and hold again within 1 second to ramp down. |
| 2C | Jump to the highest level |
| 4C | Lock / unlock |

The light blinks once when power is connected.

## Simple UI
Simple UI is on by default and is turned back on by every factory reset.

| Mode | Action | Function |
|---|---|---|
| Off | 1C | On at memorized level |
| Off | 1H | On at floor, keep holding to ramp up |
| Off | 2C | On at ceiling |
| Off | 2H | Momentary ceiling |
| Off | 3C | Battery check (blinks once, then turns off) |
| Off | 4C | Lockout |
| Off | 10H | Switch to Advanced UI |
| Off | 15C or more | Version check |
| On | 1C | Off |
| On | 1H | Ramp up (or down if released less than 1 second ago) |
| On | 2H | Ramp down |
| On | 2C | Go to / from the ceiling |
| On | 4C | Lockout |

Simple UI defaults: floor 20/150, ceiling 120/150, 5 steps, no turbo. These are set in the Simple UI config menu (see [Configuration menus](#configuration-menus)).

Since 2024-08, strobes and mood modes are blocked in Simple UI. Some lights have an **Extended Simple UI**, at the manufacturer's request, which adds ramp style toggle (3C), sunset timer (5H) and aux LED pattern and colour (7C / 7H).

### Switching UI
- **Simple → Advanced:** 10H from off
- **Advanced → Simple:** 10C from off
- **Which UI am I in?** 3C from off. Simple UI blinks the battery voltage once, Advanced UI repeats it.

## Advanced UI
### From off
| Action | Function |
|---|---|
| 1C | On at memorized level |
| 1H | On at floor, keep holding to ramp up |
| 2C | On at ceiling |
| 2H | Momentary turbo (off on release) |
| 3C | Blinky & utility modes (starts at battery check) |
| 3H | Strobe & mood modes (last used) |
| 4C | Lockout |
| 5C | Momentary mode |
| 6C | Tactical mode |
| 7C | Next aux LED pattern |
| 7H | Next aux LED colour |
| 8H | Aux LED brightness (some lights) |
| 9H | Misc config menu (some lights) |
| 10C | Switch to Simple UI |
| 10H | Simple UI config menu |
| 13H | Factory reset (some lights) |
| 15C or more | Version check |

### While on (ramp)
| Action | Function |
|---|---|
| 1C | Off |
| 1H | Ramp up (or down if released less than 1 second ago, or already at ceiling) |
| 2H | Ramp down |
| 2C | Go to / from ceiling or turbo (see turbo style) |
| 3C | Toggle smooth / stepped ramp. On multi-channel lights, next channel mode instead. |
| 3H | Momentary turbo, or tint ramp on lights with tint control |
| 4H | Momentary turbo when 3H is tint ramp |
| 4C | Lockout |
| 5C | Momentary mode |
| 5H | Sunset timer: each blink adds 5 minutes |
| 6C | Toggle smooth / stepped ramp, when 3C is used for channel modes |
| 7H | Ramp config menu |
| 9H | Channel mode config (multi-channel lights) |
| 10C | Save manual memory (brightness and channel mode) |
| 10H | Ramp extras config menu |

### Brightness memory
1C from off turns on at the memorized level. There are three memory types:
- **Automatic:** the last level you ramped to. Shortcut levels (turbo, 2C ceiling, 1H floor) aren't remembered.
- **Manual:** a fixed level saved with 10C while on.
- **Hybrid:** automatic if the light was only off briefly, manual if it was off longer than a timer (0 to about 140 minutes).

These are set in the ramp extras menu.

### Sunset timer
Set the brightness, then 5H while on. The light blinks once per second, and each blink adds 5 minutes. It slowly dims to the lowest level and turns off when the time runs out. In candle mode it stays steady until the last minute, then dims out.

## Lockout
Enter lockout with 4C from off or while on. It prevents accidental activation in a pocket or bag.

| Action | Function |
|---|---|
| 1C / 1H | Momentary moon (lowest floor) |
| 2C / 2H | Momentary low (highest floor, or the manual memory level if set) |
| 3C | Unlock, stay off |
| 3H | Next channel mode (multi-channel lights) |
| 4C | Unlock and turn on at memorized level |
| 4H | Unlock and turn on at floor |
| 5C | Unlock and turn on at ceiling |
| 7C | Next aux LED pattern |
| 7H | Next aux LED colour |
| 10H | Auto-lock config |

**Auto-lock** locks the light automatically after it has been off for a set time. In the config, click once per minute. 0 clicks turns it off, which is the default.

## Blinky & utility modes
3C from off. In any of these, 1C turns the light off and 2C goes to the next mode.

| Mode | Notes |
|---|---|
| Battery check | Blinks the voltage: whole volts, pause, tenths, pause, hundredths. A very quick blink means zero. 4.2V is full, about 3.0V is empty. |
| Temperature check | Blinks the temperature in °C (lights with a sensor) |
| Beacon | A short pulse at the memorized level. Hold the button to set the interval: it blinks once per second while held. |
| SOS | Three short, three long, three short (if enabled) |

**Battery check extras:**
- 2H: toggle powerbank mode, which charges another device over USB-C (some lights, not a standard feature)
- 3C: choose which LEDs blink the numbers (multi-channel lights, notably this *includes* aux colours)
- 7H: voltage config menu

**Battery check resolution** depends on firmware date:

| Firmware | Resolution |
|---|---|
| 2026-09 or later | 0.01V |
| 2024-04 or later | 0.02V |
| 2023-12 or later | 0.025V |
| Older | 0.1V |

## Strobe & mood modes
3H from off. Opens the last-used mode.

| Mode | Notes |
|---|---|
| Candle | Flickering candle. 5H adds a sunset timer. |
| Bike flasher | Steady medium light with a brighter stutter once per second |
| Party strobe | Motion-freezing strobe |
| Tactical strobe | Disorienting strobe. Gets hot. |
| Police strobe | On some lights with 2 or more colours, generally red/blue aux |
| Lightning storm | Random flashes |

| Action | Function |
|---|---|
| 1C | Off |
| 2C | Next mode |
| 4C | Previous mode |
| 1H | Brighter (candle, bike) or faster (strobes) |
| 2H | Dimmer or slower |
| 5C | Momentary mode with the current strobe |

## Momentary mode
5C from off, while on, or in a strobe mode. The light is only on while the button is held, at the memorized level or with the current strobe.

> The only way to leave momentary mode is to **disconnect power** by loosening the tailcap or battery tube.
{.is-warning}

## Tactical mode
6C from off. 6C again exits.

| Action | Default |
|---|---|
| 1H | Slot 1: high |
| 2H | Slot 2: low |
| 3H | Slot 3: strobe |

All three are momentary. To change a slot, 7H in tactical mode, then click once per brightness level (1–150; hold adds 10). 0 means the last-used strobe, 151 the party strobe, 152 the tactical strobe, and 153 and up the other strobes in order.

## Aux LEDs
Many Anduril lights have aux LEDs (small LEDs around the main emitter) or a lit button. These can be configured from off or from lockout. The settings for off and lockout are separate.

- **7C:** next pattern: off, low, high, blinking. Lights with an aux control chip add breathing patterns.
- **7H:** next colour. Hold and release on the colour you want.
- **8H:** aux brightness (2026+ firmware with an aux control chip). Set the pattern to low or high first.

**Colour order:** red, yellow, green, cyan, blue, purple, white, disco (fast random), rainbow (cycling), voltage.

**Voltage colours:** in voltage mode, the colour shows the battery level:

| Colour | Voltage |
|---|---|
| Red | 2.9V |
| Yellow | 3.3V |
| Green | 3.5V |
| Cyan | 3.7V |
| Blue | 3.9V |
| Purple | 4.1V |

**Post-off voltage display (POVD):** on lights with RGB aux LEDs, the aux LEDs show the battery voltage colour for a few seconds (4 by default) after the light turns off.

> This section does not currently cover non-standard aux offerings such as tri-aux, available from certain retailers like JLHawaii808, or custom aux boards made by theoboegod
{.is-info}

## Configuration menus
In a config menu, the light blinks once for each setting. Release the button after the blink for the setting you want to change, then click the number of times for the value. When entering a value, 1H counts as 10 clicks.

### Ramp config (7H while on)
Smooth and stepped ramps have separate settings. Set the ramp style first, then enter the menu.

| # | Smooth ramp | Stepped ramp |
|---|---|---|
| 1 | Floor: click n times for level n of 150 (default 1) | Floor (default 20) |
| 2 | Ceiling: click n times for level 151 − n (default 120) | Ceiling (default 120) |
| 3 | Ramp speed: 1 = fastest (about 2.5s), 4 = slowest (about 10s) | Number of steps: 1–150 (default 7) |

### Simple UI config (10H from off, in Advanced UI)
1. Floor (default 20/150)
2. Ceiling (default 120/150)
3. Number of steps (default 5)
4. Turbo style (default 0: no turbo)

### Ramp extras (10H while on)
1. **Disable manual memory:** any value goes back to automatic memory.
2. **Manual memory timer:** n clicks = n minutes, 0 = off. Non-zero gives hybrid memory.
3. **Ramp after moon:** 0 = 1H from off ramps up, 1 = stays at floor.
4. **Advanced UI turbo style:** 0 = ceiling only, no turbo. 1 = 2C goes to turbo (Anduril 1 style). 2 = 2C goes to ceiling, or to turbo if you're already at the ceiling (Anduril 2 style).
5. **Smooth steps:** 0 = off, 1 = fade between steps.

### Voltage config (7H in battery check)
1. **Voltage correction:** 20 clicks = no change. Each click above or below shifts by 0.01V (19 = −0.01V, 21 = +0.01V).
2. **POVD timeout:** seconds, 0 = off (default 4).
3. **Aux low ramp level:** button LEDs turn on low at this level and above.
4. **Aux high ramp level:** button LEDs turn on high at this level and above.
5. **Aux while on:** 0 = none, 1 = single-colour aux, 2 = RGB aux, 3 = both.

### Thermal config (7H in temperature check)
1. **Calibrate:** click once per °C of the current room temperature.
2. **Temperature limit:** click n times for 30 + n °C. Default 45°C, max 70°C.

> Lights often arrive with miscalibrated thermal settings, it is a good idea to set the current room temperature after receiving a new Anduril light.
{.is-warning}

### Misc config (9H from off, some lights)
1. Tint ramp style (multi-channel lights): 0 = smooth, 1 = middle tint only, 2 = extreme tints only, 3+ = stepped with that many steps
2. Jump start level: a brief pulse when turning on from off, for emitters that struggle to start at low levels (1–150)

## Channel modes (multi-channel lights)
Lights with more than one set of emitters, such as two colour temperatures, have channel modes.
- **3C while on:** next channel mode. Smooth / stepped toggle moves to 6C.
- **3H while on:** tint ramp, if the channel mode supports it.
- **9H while on:** turn channel modes on or off. Release at the blink for the mode number, then click once to enable or wait to disable.

A typical dual-channel light has: channel 1, channel 2, 50/50 blend, tint ramp and auto-tint.

## Protection
- **Thermal regulation:** brightness is adjusted gradually to stay under the temperature limit.
- **Low-voltage protection:** brightness steps down when the battery is low, and the light turns off at 2.8V.

## Version check
15C or more from off. On firmware from 2023-12 or later, the light blinks a code in the form `MODEL-YYYY-MM-DD`. `MODEL` is a 4-digit number made of a brand ID and a product ID, and the date is the firmware release. The model number must match when reflashing.

A date of 1969-07-20 means the firmware builder probably made a mistake.

## Factory reset
Resets all settings and turns Simple UI back on.
- **Any light:** loosen the tailcap, hold the button, tighten the tailcap and keep holding for about 4 seconds.
- **Some lights:** 13H from off and keep holding for about 4 seconds.

The light flickers while getting brighter, then flashes to full power. Release before full power to cancel.

## Sources
- [Anduril User Manual](https://github.com/ToyKeeper/anduril/blob/trunk/docs/anduril-manual.md) by ToyKeeper
- [Anduril 2 UI diagram](https://github.com/dirtydancing/anduril-tikz-diagram) by dirtydancing
- [Anduril source code](https://github.com/ToyKeeper/anduril)
