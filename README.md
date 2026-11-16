# SPECTRA·LAB

A browser-based DWDM network simulator for learning how optical transport networks are built, how they fail, and how a NOC finds the fault.

Everything is in one self-contained `index.html`. There is nothing to install and no server component.

## What it is

A fictional carrier network you can inspect, break and repair:

- **Six metros**: five on the mainland, each a four-site ROADM ring with ten customer sites, and a small island metro reached by a subsea cable.
- **Eight long-haul routes** along highways and rail lines, with amplifier huts, shared-risk points at a river bridge and a tunnel, a second line system on the busiest route, and an express trunk with a regenerator.
- **Layered services**: fiber cables and strand assignments, line systems, wavelengths, customer circuits cross-connected at metro gateways, and an IP core riding on top.
- **Equipment you can open**: every site has a chassis view with shelves, cards and pluggables, plus the power plant in a hut, the meet-me room at a gateway, and the building entrance at a customer site.

The geography, site names, CLLI codes and equipment are invented. Nothing here copies a real vendor's product or a real carrier's network.

## Modes

| Mode | What you do |
| --- | --- |
| **Sandbox** | Break anything and watch what the network does: cut a cable, fail a card, pull a jumper, kill site power. |
| **Drills** | 24 prepared faults with the cause hidden. Read the alarms, find the root cause, declare it, file the incident report. |
| **Live shift** | Faults arrive on their own, several at once. Work the queue against the SLA clock. |
| **Design** | Order a circuit from A to Z, single, diverse or protected, and see how it would be built before provisioning it. |

A guided tutorial, a twelve-chapter manual, a glossary and an instructor answer key are in the **Menu**.

## What you can learn from it

- How a circuit is stitched together from an access wave, gateway cross-connects and long-haul trunks
- Reading fiber assignments, tracing a line system strand by strand, and running an OTDR
- OSNR, margin, modulation reach, Raman, tilt, dispersion and flex grid
- 1+1 protection, optical restoration, OTN rerouting, and what none of them cover
- Why "diverse" routes fail together, and why a protected site can still be single-threaded at the door
- How a failure that takes nothing down can still congest the IP layer
- NOC workflow: scoping, correlating alarms, tickets, escalation, handover

## Requirements

A desktop browser with **WebGPU**. Current Chrome and Edge work. Safari and Firefox depend on version. Without WebGPU the page shows an error message in place of the map.

Target hardware is a mid-range discrete GPU at 1440p, where it holds 60 fps.

## Controls

| Input | Action |
| --- | --- |
| Drag | Pan the map or chassis |
| Wheel / pinch | Zoom |
| Click | Select a site, fiber, card or jumper |
| Double-click a site | Open its chassis |
| Esc | Back to the map, or close the menu |
| Space | Pause / resume |
| F | Show frame rate and worst frame time |

The bottom panel also has a console that takes TL1-style commands. Type `HELP` there for the list.

## Running it locally

Download `index.html` and open it in a WebGPU-capable browser. If the map does not appear when opened straight from disk, serve the folder instead:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000/`.

## Saved data

Options, drill progress and saved sessions are kept in your own browser's local storage. Nothing is sent anywhere, and nothing is shared between visitors.

## How it is built

- Rendered with WebGPU directly; no Three.js, Babylon.js or other engine
- Fully procedural: terrain, icons and text are generated at startup, with no image, font or model files
- No per-frame JavaScript allocations; all GPU buffers are preallocated
- One file, about 235 KB minified (about 93 KB gzipped)

## Limitations

This is a teaching model, not a planning tool. Optical physics is simplified, timings are compressed (a splice that takes hours takes seconds here), the map is not strictly to scale, and submerged repeaters are shown as racks like any other amplifier site.
