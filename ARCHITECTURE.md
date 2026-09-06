# Current Architecture

## Design status

The architecture is a current design baseline and remains subject to validation through practical testing.

## Core layer

### Loxone

Role:
- central building automation logic
- stable, local and long-lived operation
- handling of essential building functions

### KNX

Role:
- wired switches, push buttons, sensors and actuators
- long-lived field infrastructure
- deterministic local operation

## Integration and visualization layer

### Home Assistant

Role:
- integration of consumer products
- Matter, Thread, Zigbee and WLAN device integration
- dashboards and wall displays
- experimental automation
- monitoring and visualization

Home Assistant is not intended to be the sole dependency for essential building functions.

## Communication principles

Priority order:
1. Ethernet for core components
2. wired field buses such as KNX
3. Thread / Matter / Zigbee for suitable consumer devices
4. WLAN only where wired or low-power alternatives are impractical

The architecture should avoid unnecessary dependency on future WLAN generations for core functionality.

## Failure model

The following must remain available during Home Assistant/server failure:

- basic lighting
- heating
- shading
- essential local control

Consumer functions may fail without affecting building operation.

## Integration boundaries

Interfaces between KNX, Loxone and Home Assistant are intentionally still open. Integration mechanisms will be selected only after sufficient practical validation.

## Visualization

Wall displays are preferred over smartphone dependency for household interaction. Kiosk-style displays and presence-triggered activation are being evaluated.

## Current classification examples

| Function | Layer | Preferred communication |
|---|---|---|
| Lighting | Core | wired |
| Lighting scenes | Core | wired |
| Floor heating | Core | wired |
| Shading | Core | wired |
| Robot mower | Consumer | WLAN/mobile as needed |
| Robot vacuum | Consumer | Home Assistant / vendor integration |
| Wall dashboards | Integration | Ethernet/WLAN depending device |
