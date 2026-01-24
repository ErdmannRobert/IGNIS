# IGNIS – environment_parameters Specification
### Version: v0.1  |  Status: Draft

## 0. Normative Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## 1. Purpose & Scope

This specification defines the set of environment parameters used within the IGNIS ecosystem.

This specification does not define how environment parameters are transported or encoded, nor how modules implement parameter-dependent behavior.

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

This specification is independent and does not rely on any other IGNIS specifications.

## 4. Compliance

To comply with this specification follow the requirements defined in "5 Normative Requirements" and all specifications listed in "3 Dependencies".

Recommendations in "6 Recommendations" are non-normative and do not affect compliance. Nevertheless it is recommended to follow them for consistency. 

## 5. Normative Requirements

### Parameter model

Each environment parameter is defined by the following properties:

- **Parameter ID**  
  A unique numerical identifier in the range **0–100**. Parameter IDs uniquely identify an environment parameter within the IGNIS ecosystem.

- **Type**
  - Static:  Values of static parameters MUST NOT change after the start of a game instance.
  - Dynamic: Values of dynamic parameters MAY change at any time during a game instance. The value of a dynamic parameter MUST NOT be inferred by its previous value. 

- **Length**  
  The number of data bytes in the range **0-64** associated with the parameter.

- **Encoding**  
  A definition of how the parameter’s bytes are to be interpreted.

- **Physical Representation**  
  Instructions for a physical representation of the parameter’s value. 

- **Semantical Meaning**  
  Specification on how the value of the parameter is connected to other game mechanics. 
  This section is only included if the parameter has an inherent meaning in the game context. 
  

### Parameter definitions:

#### Serial number

**Parameter ID:** 0  
**Type** Static  
**Length:** 16  
**Encoding:** 
```
  0   1   2   ...  14  15  
+---+---+---+-   -+---+---+
|N01|N02|N03| ... |N15|N16|
+---+---+---+-   -+---+---+

[Nxx] Character nr. xx of the serial number: 0x20 .. 0x7E (printable ASCII)
```
**Physical Representation:**  
The serial number MUST be displayed as its ASCII representation in one 16 character string. It MUST be labeled as "serial number".  

**Semantical Meaning**  
Specifies the semantical meaning in the game play, if the parameter has a meaning. 

---

#### Indicators

**Parameter ID:** 1
**Type** Static  
**Length:** 4
**Encoding:** 
```
  0   1   2   3  
+---+---+---+---+
|IC1|IC2|IC3|IC4|
+---+---+---+---+

[ICx] State of indicator nr. x: 0 .. 1 (off/on)
```
**Physical Representation:**  
The four indicators MUST be located together. Each indicator MUST resemble a *off* state when its respective value is *0* and a *on* state when it is *1*. The indicators MUST be labeled as follows:  
Indicator nr. 1: "BOOT"  
Indicator nr. 2: "VGA"  
Indicator nr. 3: "DRAM"  
Indicator nr. 4: "CPU"  

---

#### Batteries

**Parameter ID:** 2
**Type** Static  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|BAT|
+---+

[BAT] Battery configuration index: 0 .. 3
```
**Physical Representation:**  
The number and type of batteries MUST be clearly inferable. They MAY be represented as physical battery cell types, but MAY also be represented symbolically.

The value of the *batteries* parameter is mapped as follows:  
Battery configuration 0: Empty / no batteries  
Battery configuration 1: 1x AA  
Battery configuration 2: 2x AA  
Battery configuration 3: 1x 9V  

---

#### Port

**Parameter ID:** 3
**Type** Static  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|PRT|
+---+

[PRT] Port index: 0 .. 5
```
**Physical Representation:**  
For the *port* parameter one of the ports described below should be visible. 
The type of port MUST be clearly inferable. The ports MAY be represented as the actual connector of seat type but they MAY also be represented differently as long as it clearly identifiable. 

The value of the *ports* parameter is mapped as follows:  
Port index 0: USB A  
Port index 1: USB B  
Port index 2: HDMI  
Port index 3: TosLink  
Port index 4: RJ-45  
Port index 5: PS/2  

The ports MUST NOT be labeled with there corresponding names. The port type MUST only be inferable by the shape of the port representation. 

---

#### Batch

**Parameter ID:** 4
**Type** Static  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|BTC|
+---+

[BTC] : 0 .. 255
```
**Physical Representation:**  
MUST be displayed in hexadecimal format from 0x00 to 0xFF. MUST be labeled as "Batch nr.".

--- 

#### Mood

**Parameter ID:** 5  
**Type** Static  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|MOD|
+---+

[MOD] Mood index: 0 .. 6
```
**Physical Representation:**  
The mood must be represented by a visual indicator that maps a mood to a color as follows:  
GRRRRRR!!: red  
grrr: orange  
happy: yellow  
relaxed: green  
calm: cyan  
already on the seventh energy drink after working for 3 days strait but pretending to be fine to stop everyone from asking me if I am fine: blue  
romantic: purple  

The color maps to the mood index as follows:  
red: 0  
orange: 1  
yellow: 2  
green: 3  
cyan: 4  
blue: 5  
purple: 6  

---

#### Strikes

**Parameter ID:** 50
**Type** Dynamic  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|SKN|
+---+

[SKN] : 0 .. 3 (uint8)
```
**Physical Representation:**  
MUST be displayed in a way that the numerical amount of strikes can be inferred. MUST be labeled as "strikes". 

**Semantical Meaning**  
The global number of strikes received so far during this round. 

---

#### Time

**Parameter ID:** 51
**Type** Dynamic  
**Length:** 2
**Encoding:** 
```
  0   1  
+---+---+
|SEC|MIN|
+---+---+

[SEC] Seconds remaining: 0 .. 59 (uint8)
[MIN] Minutes remaining: 0 .. 59 (uint8)
```
**Physical Representation:**  
A numerical display recognizable as a clock from which the exact number of MIN and SEC MUST be inferable. 

**Semantical Meaning**  
Time left on the hub countdown timer. 

This specification does not imply that the value of the *time* parameter is tied to an physical time and that it will follow predictable patterns. Therefore it MUST NOT be assumed that the current value of the *time* parameter can be inferred from a previous one. 

---

#### Modules

**Parameter ID:** 52
**Type** Dynamic  
**Length:** 5
**Encoding:** 
```
  0   1   2   3   4  
+---+---+---+---+---+
|ALL|MSV|MCO|SVD|NSV|
+---+---+---+---+---+

[ALL] Total number of active modules: 0 .. 255
[MSV] Number of modules in *solvable mode*: 0 .. 255
[MCO] Number of modules in *continuous mode*: 0 .. 255
[SVD] Number of solved modules: 0 .. 255
[NSV] Number of unsolved modules: 0 .. 255
```
**Physical Representation:**  
The riddle modules connected to the hub. 

**Semantical Meaning**  
The amount of modules in the states specified above. 

It MUST NOT be assumed that any value of the five fields above can be inferred from any other fields, all five values MUST be treated as independent. 

---

#### Orientation

**Parameter ID:** 53
**Type** Dynamic  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|ORI|
+---+

[ORI] Orientation index: 0 .. 2
```
**Physical Representation:**  
It MUST be clearly labeled which side is considered up. 

**Semantical Meaning**  
The orientation index represents the physical rotation of the bomb as follows:  
Orientation index 0: Right side up  
Orientation index 1: Right side down  
Orientation index 2: Sideways  

--- 

#### Difficulty

**Parameter ID:** 54  
**Type** Dynamic  
**Length:** 1
**Encoding:** 
```
  0  
+---+
|DIF|
+---+

[DIF] : 1 .. 3 (uint8)
```
**Physical Representation:**  
A difficulty selection input labeled as *DIFFICULTY*, with three selectable options labeled as *1*, *2*, *3*.

**Semantical Meaning**  
The selected game difficulty level selected by the player. *1* ~ easy 

## 6. Recommendations (Non-Normative)

## 7. Undefined and Reserved Areas

## 8. Notes and Rationale