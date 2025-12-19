# IGNIS – hub_module_connection Specification
### Version: v0.1  |  Status: Draft

## 0. Normative Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 1. Purpose & Scope

This specification is concerned with the interface between hubs and modules which enables the modularity of IGNIS. This specification is not concerned with the inner workings of hubs and modules. 

## 2. Definitions & Terminology

**Device**  
A self-contained functional unit within the IGNIS ecosystem. A device may include electronics, firmware, and mechanical components and interacts with other devices according to applicable IGNIS specifications.

**Hub**  
A device that acts as the central controller of an IGNIS system. The hub orchestrates game logic, provides environment parameters, manages user interaction, and coordinates communication with attached modules.

**Module**  
A device that implements a single physical puzzle and is designed to be attached to a hub. A module interacts with the hub via the Hub-Module Connection Specification and reports its status as part of the overall game.

**Environment parameters**
A set of random, game-instance–specific values chosen by the hub at the beginning of each game. Environment parameters are physically presented to the player and may be observed and interpreted as part of solving module riddles. Environment parameters have no intrinsic game semantics beyond their concrete values.

**Strikes**
A module MAY issue strikes. The number of strikes are counted globally by the hub. When too many strikes are reached the game is lost. 

**State**
A runtime condition of a module that reflects its current role in the game. A module can only be in one state at a time. The states specified in this document describe the externally observable role of the module within the game procedure and do not need to correspond directly to the internal states used by a module’s implementation.

## 3. Dependencies

Compliance with the following specifications is REQUIRED:
- environment_parameters Specification v0.1

This specification is incomplete without the specifications listed above. 

## 4. Compliance

To comply with this specification follow the requirements defined in "5 Normative Requirements" and all specifications listed in "3 Dependencies".

Recommendations in "6 Recommendations" are non-normative and do not affect compliance. Nevertheless it is recommended to follow them for consistency. 

## 5. Normative Requirements

### 

- Electrical / Power
  - Supply voltage and tolerance
  - Max current per module
  - Connector / Pinout
- Communication / Protocol
  - Physical layer -> CAN
  - Protocol -> Cy4Net
  - Hub ↔ Module services:
    - Module reports solved status
    - Hub provides environment parameters

## 6. Recommendations (Non-Normative)

<!--
Strong suggestions, not requirements. Should encourage consistency. 
-->

## 7. Undefined and Reserved Areas

<!--
What is not defined by the specification? Where is room for future versions of the specification to evolve?
-->

### Mechanical
The mechanical specifications for the module hub connection will follow in future versions of this specification. Preliminarily there are no mechanical constrains. 

## 8. Notes and Rationale

<!--
Explanation of design decisions. Not necessary but can be helpful. 
-->