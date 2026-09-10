# Roborock Garage

## Status and evidence

Consolidated on 2026-09-10 from the project discussion “HA: Staubsauger Garage” and the repository baseline of 2026-09-06.

This is a design and evaluation baseline. The reviewed material contains no completed garage prototype, measured travel times, selected bill of materials or acceptance-test results. Integration options below were discussed or researched; they are not verified implementations in this installation.

## Goal

Integrate a Roborock robot vacuum with fresh-water connection into a kitchen cabinet. The robot and docking station remain accessible by opening the normal kitchen cabinet front.

A complete horizontal plinth/front panel below the kitchen front is lifted vertically to create the robot exit. The moving panel may include the normal plinth offset and is intended to move as one rigid part.

## Functional sequence

1. Home Assistant triggers opening of the garage front.
2. Linear actuator moves the panel upward.
3. Once the opening movement is complete, Home Assistant starts the required Roborock cleaning program.
4. After the robot returns to the dock, the panel can be lowered again.

Continuous position tracking is not required. The required functional states are essentially:

- open
- closed
- opening triggered
- closing triggered

## Mechanical concept

Current preferred approach:

- one rigid full-width plinth/front panel
- vertical lifting movement
- approximately 300 mm actuator stroke
- linear actuator / electric lifting cylinder with integrated limit switches
- actuator installed behind the kitchen front / inside the cabinet
- separate mechanical guidance for the moving front so the actuator primarily provides lifting force rather than lateral guidance
- sufficient structural rigidity and balanced loading to reduce binding

The cabinet volume is not considered a critical limitation; if required, a complete cabinet can be allocated to the mechanism and docking station.

## Actuator requirements

Current target specification:

- fixed stroke: approximately 300 mm or more
- 12 V or 24 V DC
- integrated end switches
- simple polarity reversal for up/down movement
- no proprietary cloud controller required
- relatively low to medium force; very high-force 6000 N actuators are considered unnecessary and potentially undesirable
- preference for faster movement rather than very slow heavy-duty actuators

Position feedback via potentiometer or Hall sensor is currently not required.

## Control concept

Preferred simplicity:

- local UP/DOWN push buttons are desirable
- Home Assistant should trigger the same electrical commands through relays or a motor controller
- actuator internal limit switches define the physical end positions
- Home Assistant can use known travel time plus a safety margin before starting the Roborock program
- optional external open/closed contacts can later be added for plausibility checking, but are not currently mandatory

### Timing and state interpretation

Without external feedback, open/closed are assumed states derived from commands and elapsed time. A travel-time delay cannot confirm that the panel actually opened if it binds or the drive fails. This distinction is also documented for [ESPHome time-based covers](https://esphome.io/components/cover/time_based/) (reviewed 2026-09-10).

The selected actuator's internal end switches are intended to stop travel; whether they expose a separate status signal depends on the model. The choice of external confirmation remains open. No continuous position measurement is required by the current brief.

Local UP/DOWN operation should remain usable without Home Assistant. Local travel timeout, direction handling and behaviour after power loss still need to be defined and tested with the selected controller.

## Home Assistant integration options evaluated

### ESP32 / ESPHome

A DIY approach discussed using reports of other Home Assistant projects; those reports are not acceptance evidence for this garage:

- ESP32
- ESPHome
- 2-channel relay or H-bridge / polarity-reversal stage
- 12/24 V linear actuator
- optional local buttons and end-state sensors

Advantages:
- fully local
- flexible logic
- native Home Assistant integration
- easy addition of buttons and sensors

### Zigbee relay

A Zigbee relay such as the NOUS B3Z may simplify the smart-home side, but it is currently considered a control layer rather than a guaranteed direct motor controller.

Reason:
A typical two-wire DC linear actuator requires polarity reversal:

- polarity A -> direction 1
- reversed polarity -> direction 2

A generic dual relay does not automatically provide a documented motor/interlock/H-bridge function. Therefore a separate polarity-reversal stage may still be required unless a suitable motor controller with UP/DOWN inputs is selected.

## Suppliers / manufacturers to consider in Austria

Preference is given to suppliers that can support implementation in Austria.

Relevant companies identified so far:

- ELRA Antriebstechnik, Jois / Burgenland
- MEW Maschinenelemente, Dornbirn
- BÖMA, Alberschwende
- KML Linear Motion Technology, Wien
- igus Österreich
- MÄDLER Österreich

German / EU suppliers and Amazon-sourced generic actuators may be used for prototyping if they meet the electrical and mechanical requirements.

## Current design decision

The project currently favors a **simple fixed-stroke linear actuator with integrated end switches** over more complex belt, encoder, Hall-sensor or potentiometer solutions.

The exact actuator, guide mechanism and relay/motor-controller combination are still open and must be selected after final cabinet/front dimensions and weight are known.

## Next implementation step

Measure the cabinet/front geometry and moving mass first, then select the actuator, guides, power supply and controller as a compatible combination. Keep the unresolved component and sensor decisions in [OPEN_TOPICS.md](../../OPEN_TOPICS.md#roborock-garage).

Before marking the concept validated, record observed travel times under load, repeatable movement without binding, both end stops, local button operation without Home Assistant, and restart/timeout behaviour. Define and test the robot start/return sequence and the handling of an obstructed opening before unattended operation. These are pending checks, not completed results.
