# IGNIS – module Specification
### Version: v0.1  |  Status: Draft

## 0. Normative Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## 1. Purpose & Scope

This specification defines the required characteristics and behavior of IGNIS modules. A module is a device that implements a physical riddle and is designed to be mounted onto a hub.

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
- hub_module_connection Specification v0.1
  - Defines how modules and hubs physically and logically communicate, including message formats, transport mechanisms, and electrical interfaces.
- environment_parameters Specification v0.1
  - Defines the set of environment parameters, their meaning, and their valid ranges.

This specification is incomplete without the specifications listed above. 

## 4. Compliance

To comply with this specification follow the requirements defined in "5 Normative Requirements" and all specifications listed in "3 Dependencies".

Recommendations in "6 Recommendations" are non-normative and do not affect compliance. Nevertheless it is recommended to follow them for consistency. 

## 5. Normative Requirements

### Startup
A module MUST enter the **idle state** immediately after being supplied with power. When the hub notifies a module of the game start it MUST transition to the **unsolved state** or **continuous state** depending on its riddle mode. When the hub notifies a module of the game end it MUST transition back to its **idle state**.

### Environment parameters

Environment parameters are provided to modules by the hub via the Hub-Module Connection Specification and are defined by the Environment Parameters Specification.

A module MAY also provide its own environment parameters for the same purpose as the environment parameters provided by the hub. These internal environment parameters MUST only be used by the module that provides them. 

A module MUST store values of **static environment parameters** when informed about them by the hub while in the **idle state**.

A module MUST NOT store values of **static environment parameters** when informed about them by the hub while not in the **idle state**. 

A module MAY ask for values of **dynamic environment parameters** at any point while not in the **idle state**.

A module MUST tolerate environment parameters it does not recognize. 

A module MUST tolerate not receiving environment parameters it expects or receiving unexpected values of environment parameters. 

No default values for **environment parameters** are defined by this specification. 

### Riddle Modes

While the game is running a module MUST be in one of two **riddle modes**:
1. **Solvable**
   In this mode a module starts off in the **unsolved state**. There MUST be a specific set of player actions that transitions the module into the **solved state**. When the module is in *solvable* mode there MAY be player actions that result in the module issuing a strike. The correct solution for a module in *solvable* mode SHOULD depend on the hub environment parameters. 
2. **Continuous**
   When a module is in this mode it is in the **continuous state** and MUST NOT be able to transition to a solved state. In this mode a module MUST require a specific set of player actions to prevent the module from issuing a strike.  Modules in this mode cannot be solved, they have to be dealt with continuously to prevent strikes. The actions needed to prevent a strike in *continuous* mode SHOULD depend on the hub environment parameters. 

The riddle mode MAY be dependent on the hub environment parameters. 

### Visual indicator

A module MUST provide a **visual indicator** that can be changed in color. 

The **visual indicator** MUST be located visible to the player. 

The **visual indicator** MUST convey the module’s current state using
the following color semantics:

- **Idle state**  
  The indicator MUST be **blue**.

- **Unsolved state**  
  The indicator MUST be **purple**.

- **Solved state**  
  The indicator MUST display **green**.

- **Strike event**  
  At the event of a strike the indicator MUST display **red** for three seconds.
  This MUST override the color of the current module state.   

- **Continuous state**  
  The indicator MUST display **yellow**.

## 6. Recommendations (Non-Normative)

The **visual indicator** MAY be implemented as a RGB LED. 

## 7. Undefined and Reserved Areas

## 8. Notes and Rationale