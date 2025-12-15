# IGNIS – environment_parameters Specification
### Version: v0.1  |  Status: Draft

## 0. Normative Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## 1. Purpose & Scope

This specification defines the set of environment parameters used within the IGNIS ecosystem, including their meaning, valid ranges, and lifecycle.

This specification does not define how environment parameters are transported or encoded, nor how modules implement parameter-dependent behavior.

## 2. Definitions & Terminology

**Device**  
A self-contained functional unit within the IGNIS ecosystem. A device may include electronics, firmware, and mechanical components and interacts with other devices according to applicable IGNIS specifications.

**Hub**  
A device that acts as the central controller of an IGNIS system. The hub orchestrates game logic, provides environment parameters, manages user interaction, and coordinates communication with attached modules.

**Module**  
A device that implements a single physical puzzle and is designed to be attached to a hub. A module interacts with the hub via the Hub-Module Connection Specification and reports its status as part of the overall game.

**Environment parameters**
A set of parameters that are exposed to the player and which can be changed by the hub. At the beginning of each game, the hub chooses a random value for each parameter. This mechanic should enable modules to change their correct solution depending on the environment parameters and therefore make the game replayable. 

**Strikes**
A module MAY issue strikes. The number of strikes are counted globally by the hub. When too many strikes are reached the game is lost. 

**State**
A runtime condition of a module that reflects its current role in the game. A module can only be in one state at a time. The states specified in this document describe the externally observable role of the module within the game procedure and do not need to correspond directly to the internal states used by a module’s implementation.

## 3. Dependencies

This specification is independent and does not rely on any other IGNIS specifications.

## 4. Compliance

To comply with this specification follow the requirements defined in "5 Normative Requirements" and all specifications listed in "3 Dependencies".

Recommendations in "6 Recommendations" are non-normative and do not affect compliance. Nevertheless it is recommended to follow them for consistency. 

## 5. Normative Requirements

### Parameter model

Each environment parameter is defined by the following properties:

- **Parameter ID**  
  A unique numerical identifier in the range **0–100**. Parameter IDs uniquely identify an environment parameter within the IGNIS ecosystem.

- **Length**  
  The number of data bytes associated with the parameter. The length MUST be at least 1 byte and MUST NOT exceed *N* bytes. 

- **Encoding**  
  A definition of how the parameter’s bytes are to be interpreted.

- **Physical Meaning**  
  A description of what the parameter represents in the context of the game and how they should be physically represented.

### Parameter definitions:

#### Serial number

**Parameter ID:** 0  
**Length:** 16  
**Encoding:** 
```
  0   1   2   ...  14  15  
+---+---+---+-   -+---+---+
|N01|N02|N03| ... |N15|N16|
+---+---+---+-   -+---+---+

[Nxx] Character of the serial number: 0 .. 255 (ASCII) 
```
**Physical Meaning:**  
A size 16 string of arbitrary ASCII characters.

## 6. Recommendations (Non-Normative)

## 7. Undefined and Reserved Areas

## 8. Notes and Rationale