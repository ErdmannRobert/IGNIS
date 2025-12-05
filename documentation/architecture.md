# IGNIS - Architecture

IGNIS is inspired by Keep Talking and Nobody Explodes, but implemented as a **physical modular puzzle bomb** featuring **interchangeable riddle modules** connected by a central hub device.

This is a high-level document that outlines the conceptual architecture of the IGNIS ecosystem.
Implementation details and formal definitions are provided in `specifications/`.

## 0 Overview

IGNIS is a modular ecosystem composed of multiple devices that interoperate through standardized specifications.
Each device can include several engineering domains, which evolve and are versioned independently.

## 1 Design Principles

### 1.1 Modularity

IGNIS is a fully modular system because:
- Riddles can be changed individually
- The ecosystem is open for contributions of new modules
- Modules can be rearranged to change difficulty or length
- Individual modules can be repaired or replaced
- Clear Separation of concerns

### 1.2 Replayability

The goal of IGNIS is to create a puzzle that can be played over and over again. This is realized by changing the correct riddle solution dependent on *environment parameters* provided by the hub, that change every round.

### 1.3 Extensibility

IGNIS is designed to allow expansion by anyone. The interoperation between devices is clearly specified. If a new IGNIS device is created according to the specifications it should work in the entire ecosystem. 

## 2 Core Concepts 

### 2.1 Devices

A device is any self-contained functional unit within IGNIS.
There are two types of devices:
- Hubs — the main body that orchestrates game logic
- Modules — swappable puzzle units that attach to a hub

All devices communicate using a shared bus and a common communication protocol defined in the specifications.

#### 2.1.1 Hubs

The hub is the central controller within IGNIS.
Each system contains exactly one hub, which provides:
- Game orchestration
  - Game logic
  - Timer / strike / failure handling
  - etc.
- User interface elements
  - Countdown display
  - Status indicators
  - Reset / start controls
  - etc.
- **Environment parameters**
  - Randomized values generated at the beginning of each game round.
  - Ensure replayability.
  - The solution to every module should depend on them.
  - Example: Serial number

*Currently the only hub in development is hub_heavy, but the project is open to different hub designs, as long as they comply with the specifications.*

#### 2.1.2 Modules

A module is a physical riddle that can be mounted onto a hub.
Modules typically contain:
- input mechanisms (buttons, switches, encoders, touch sensors …)
- feedback / output elements (LEDs, displays, buzzers)
- embedded control logic
A module:
- Queries the hub for environment parameters
- Executes its own internal puzzle logic
- Reports when solved to the hub

### 2.2 Domains

IGNIS development is divided into independent domains, each versioned separately:
- electronics -> PCB design, schematics
- firmware    -> Embedded logic, device protocol implementation
- mechanical  -> CAD models, enclosures, structural elements
- manual      -> Player-facing Puzzle solving instructions and riddle explanations. 

A change in one domain does not imply a change in the others unless compatibility is affected.

### 2.3 Specifications

Specifications are cross-device contracts that define how devices interoperate.
They guarantee that modules and hubs remain compatible even when independently developed or updated.
This includes:
- Mechanical form factors
- Electrical connections and pin assignments
- Firmware communication protocols

Specifications must not contain implementation details or anything related to an individual device. 

They should also specify which areas are undefined and they should leave room for future expansion where reasonable (for example unused pins).

Formal specification documents are located in `specifications/`.

## 3 Gameplay

When a game is started, a countdown timer begins. The goal of the game is to solve all riddles before the timer expires in order to successfully diffuse the bomb. 

Players are divided into two roles:

- **Diffusers**  
  Players who physically interact with the IGNIS device and its modules.

- **Instructors**  
  Players who have access to the manual and provide guidance to the diffusers without directly interacting with the device.

The two groups should only be able to communicate through speech, and should not be allowed to show the manual or bomb to members of the other group. 

### 3.2 Loose Conditions

There are two ways to lose a game of IGNIS:

1. **Timeout**  
   If the countdown timer reaches zero, the game is immediately lost.

2. **Strike Accumulation**

#### 3.2.1 Strikes

A module MAY trigger a strike when a player makes an incorrect action according to the module’s puzzle logic.

Strikes are accumulated system-wide and managed by the hub.

For each collected strike the countdown timer speed increases.

If a total of **three strikes** is reached, the game is immediately lost. 

### 3.1 Win Conditions

To win the game (diffusing the bomb), the diffusers have to get all riddles to there solved state before the time runs out or they hit 3 strikes. 