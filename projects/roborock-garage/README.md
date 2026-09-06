# Roborock Garage

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

## Home Assistant integration options evaluated

### ESP32 / ESPHome

A proven DIY approach found in multiple Home Assistant projects:

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
