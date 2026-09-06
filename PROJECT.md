# Project Goals and Methodology

## Goal

Build an autonomous, flexible and manufacturer-independent smart home without mandatory Internet dependency and without requiring smartphones or tablets for basic operation.

The project is currently in an open evaluation and learning phase. Technologies are tested practically before architectural commitments are made.

## Evaluation scope

Current technologies and systems include:

- Home Assistant
- Loxone
- KNX
- Matter
- Thread
- Zigbee
- Ethernet and WLAN
- consumer IoT products used for acceptance and interoperability testing

## Methodology

The project follows an iterative but controlled learning process.

### Principles

- decisions are based on real tests rather than theoretical assumptions
- previous findings remain the baseline for new evaluations
- avoid repeating already explored ideas without new evidence
- document meaningful changes, observations and conclusions
- remain technology-open until stability and integration quality are proven

## Evaluation criteria

- offline functionality
- stability and latency
- local control and authentication
- interoperability
- maintainability
- resilience and fail-safe behaviour
- usability of dashboards and wall displays
- security
- expected component lifecycle

## Current test environment

- Raspberry Pi 5 running Home Assistant
- SONOFF Zigbee gateway / ZBDongle-E
- Matter and Thread evaluation
- various consumer devices for automation and dashboard testing

## Target lifecycle model

- core infrastructure: approximately 10–20 years
- optional consumer products: approximately 2–5 years

## Functional classification

### Core

Functions that must remain operational even when Home Assistant or Internet connectivity fails:

- lighting
- heating
- shading
- essential building automation

### Consumer / integration layer

Functions that may depend on Home Assistant or vendor devices without affecting essential building operation:

- robot vacuum
- dashboards
- convenience automations
- consumer sensors and devices
- experimental integrations
