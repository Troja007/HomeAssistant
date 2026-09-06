# Open Topics

This file tracks unresolved architectural and implementation questions. Items should be removed or converted into documented decisions once sufficiently validated.

## System architecture

- final integration model between KNX, Loxone and Home Assistant
- backup and failover strategy
- local security model and authentication boundaries
- long-term monitoring and fault reporting

## Heating / climate

- final floor-heating control concept for stable temperature despite thermal inertia
- continued validation of upper-floor thermal behaviour and cooling automations

## Visualization

- wall-display hardware selection
- kiosk operation and presence-triggered display wake-up
- dashboard structure for temperatures, batteries, faults and energy flows

## Consumer integrations

- long-term Matter / Thread / Zigbee interoperability
- criteria for when WLAN-only devices are acceptable

## Roborock garage

- exact robot and docking-station model with fresh-water connection
- exact available cabinet/front geometry
- exact actuator model
- final choice of 12 V vs 24 V
- actuator speed target
- exact lifting force required after mechanical design is known
- final relay/motor controller
- whether a Zigbee relay such as NOUS B3Z is used only as smart control or combined with a separate polarity-reversal stage
- whether local push buttons are integrated directly into the motor controller
- whether separate open/closed confirmation sensors are required or timing plus internal actuator limit switches is sufficient
- final mechanical guide design for the full-width moving plinth/front panel
