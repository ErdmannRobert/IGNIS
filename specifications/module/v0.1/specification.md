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
A set of parameters that are exposed to the player and which can be changed by the hub. At the beginning of each game, the hub chooses a random value for each parameter. This mechanic should enable modules to change there correct solution depending on the environment parameters and therefore make the game replayable. 

**Strikes**
Strikes can be issued when players make a mistake. When to many strikes are reached the game is lost. 

## 3. Dependencies

Compliance with the following specifications is REQUIRED:
- hub_module_connection Specification v0.1

## 4. Compliance

To comply with this specification, all requirements defined in "5 Normative Requirements" MUST be satisfied.

Recommendations in "6 Recommendations" SHOULD be followed, nevertheless they are non-normative and do not affect compliance.

## 5. Normative Requirements

### Startup
A module MUST start of in a **idle state** as soon as it is supplied with power. When the hub notifies a module of the game start it MUST transition to the **unsolved state** or **continuous state** depending on its riddle mode. When the hub notifies a module of the game end it MUST transition back to its **idle state**.

### Environment parameters
The default values for **environment parameters** is not defined. 

A module MUST store values of **environment parameters** when informed about them by the hub while in the **idle state**.

A module MUST NOT store values of **environment parameters** when informed about them by the hub while not in the **idle state**. 

### Riddle Modes

While the game is running a module MUST be in one of two **riddle modes**:
1. **Solvable**
   In this mode a module starts of in the **unsolved state**. There MUST be a specific set of player actions that transitions the module into the **solved state**. When the module is in *solvable* mode there MAY be player actions that result in the module issuing a strike. The correct solution for a module in *solvable* mode SHOULD depend on the hub environment parameters. 
2. **Continuous**
   When a module is in this mode it is in the **continuous state** and MUST NOT be able to transition to a solved state. In this mode a module MUST require a specific set of player action, to be prevented of issuing a strike. Modules in this mode can not be solved, they have to be dealt with continuously to prevent strikes. The actions needed to prevent a strike in *continuous" mode SHOULD depend on the hub environment parameters. 

The riddle mode MAY be dependent on the hub environment parameters. 

### Visual indicator

A module MUST provide a **visual indicator** that can be changed in color. 

The **visual indicator** MUST be located visible to the player. 

The **visual indicator** MUST convey the module’s current state using
the following color semantics:

- **Unsolved state**  
  The indicator MUST be **inactive** (off) or black.

- **Solved state**  
  The indicator MUST display **green**.

- **Strike event**  
  At the Event of a strike the indicator MUST display **red** for three seconds.
  This MUST override the color of the current module state.   

- **Continuous state**  
  The indicator MUST display **yellow**.

## 6. Recommendations (Non-Normative)

## 7. Undefined and Reserved Areas

## 8. Notes and Rationale