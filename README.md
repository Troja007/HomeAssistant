# Home Assistant / Smart Home Project

Repository for the ongoing evaluation and implementation of an autonomous, manufacturer-independent smart home.

The project is intentionally technology-open. Home Assistant is currently used as the integration, visualization and experimentation layer. The target architecture is a hybrid system with a robust wired core and a flexible consumer layer.

## Current target architecture

- **Loxone**: core building automation logic
- **KNX**: wired switches, sensors and actuators for long-lived infrastructure
- **Home Assistant**: integration, visualization, experimentation and consumer-device layer
- **Ethernet**: preferred transport for core components
- **Matter / Thread / Zigbee / WLAN**: consumer-device integration where appropriate

Core functions such as lighting, heating and shading must remain operational even if Home Assistant or consumer integrations fail.

## Project principles

- local and offline operation wherever possible
- no dependency on smartphones or tablets for basic functions
- technology decisions based on practical tests
- avoid vendor lock-in
- long lifecycle for core infrastructure
- consumer components may have shorter replacement cycles
- document decisions and lessons learned to avoid repeating already evaluated approaches

## Repository structure

- [`PROJECT.md`](PROJECT.md) – project goals, methodology and current evaluation scope
- [`ARCHITECTURE.md`](ARCHITECTURE.md) – current architecture and system boundaries
- [`OPEN_TOPICS.md`](OPEN_TOPICS.md) – unresolved design and evaluation topics
- [`projects/`](projects/) – individual implementation/evaluation projects
- `Motion_Lux_Light_on.yaml` – existing Home Assistant blueprint/automation experiment

## Current subprojects

- [Roborock garage](projects/roborock-garage/README.md)
- climate / thermal behaviour evaluation
- whirlpool automation and runtime tracking
- wall display / kiosk concepts
- Matter / Thread / Zigbee interoperability tests

This repository represents the **consolidated project state**, not a raw chat history. Exploratory discussions are reduced to decisions, findings, constraints and open questions that are useful for future implementation work and Codex-based development.
