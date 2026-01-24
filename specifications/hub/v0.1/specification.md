# IGNIS – hub Specification
### Version: v0.1  |  Status: Draft

## 0. Normative Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## 1. Purpose & Scope

This specification defines the required characteristics and behavior of IGNIS hubs. A hub is a device that executes the central game logic, hosts the environment parameters and can be expanded by IGNIS modules. 

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

### Program flow

On startup a hub MUST enter **Init**.

#### Init

- The countdown time MUST be reset to the maximum time available to solve the riddles.
- The strike counter MUST be reset to zero strikes. 
- The values for all *Static* environment parameters MUST be chosen in compliance to the value ranges specified in the *environment_parameters* specification.  
- Power MUST be supplied to modules as specified in the hub_module_connection specification. 
- The values for all *Static* environment parameters MUST be communicated to the modules a specified in the hub_module_connection specification.
- MUST Transition to **Running**

#### Running 

- Value of countdown time is reduced by one every second. 
- Communication with modules as required by the hub_module_connection specification is maintained.
- Strike count is updated when notified of new strike. 
- MUST Transition to **Solved** if all modules report being solved as specified in the hub_module_connection specification.
- MUST Transition to **Failed** if strike counter reaches at least 3 strikes or value of countdown timer reaches 0. 
- MUST transition to **Init** when reset button is pressed. 
- SHOULD Transition to **Error** if unexpected event arises. 

#### Solved 

- Power MUST NOT be supplied to modules as specified in the hub_module_connection specification. 
- MUST transition to **Init** when reset button is pressed. 

#### Failed 

- Power MUST NOT be supplied to modules as specified in the hub_module_connection specification. 
- MUST transition to **Init** when reset button is pressed. 

#### Error 

- Power MUST NOT be supplied to modules as specified in the hub_module_connection specification. 
- MUST transition to **Init** when reset button is pressed. 

### IO

#### Reset button

A hub MUST include a button labeled as *RESET*.

#### State indicator 

A hub MUST include a visual representation of the current state described in **Program flow**. 

#### Buzzer

A hub MUST include a BUZZER which MUST be controllable in pitch. 

#### Environment parameters

For each environment parameter in the *environment_parameters* specification, a hub MUST implement the parameter in compliance to its specified **physical representation** and the state of this representation MUST always be alined with the specified **semantical meaning** of the parameter.

### Module connection

A hub MUST provide connections for IGNIS modules. These connections MUST comply with the *hub_module_connection* specification. 

## 6. Recommendations (Non-Normative)

## 7. Undefined and Reserved Areas

The maximal number of module connections is not defined but may be defined in a future version of this specification. 

The usage of the BUZZER will be defined in a future version of this specification. 

The kind of power supply for IGNIS hubs is not defined but may be defined in future versions of this specification. A hub MAY have a internal battery or MAY rely on a external power source. 

The maximum time available to solve the riddles will be specified in future versions of this specification. It will not exceed 3599 seconds. 

## 8. Notes and Rationale
