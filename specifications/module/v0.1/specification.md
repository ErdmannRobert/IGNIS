DRAFT!!!

- Status LED
  - RGB LED
  - Shows status
    - Not solved -> Off
    - Solved -> Green
    - Strike -> Red flash 
    - Continuos task -> Yellow 


# IGNIS – module Specification
Version: v0.1
Status: Draft

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

## 3. Dependencies

Compliance with the following specifications is REQUIRED:
- hub_module_connection Specification v0.1

## 4. Compliance

<!--
What does it mean to comply with this spec? 
-->

To comply with this specification, all requirements defined in "5 Normative Requirements" MUST be satisfied.

Recommendations in "6 Recommendations" SHOULD be followed, nevertheless they are non-normative and do not affect compliance.

## 5. Normative Requirements

<!--
This is the core of the spec. These rules must be followed to comply with the specification. 

Subsections of this section are optional and may be omitted or extended.
-->

### 5.1 Electronics  

#### 5.1.1 Visual indicator

A module MUST provide a **visual indicator** that can be changed in color. 

### 5.2 Protocol  

### 5.3 Mechanical  

### 5.4 Behavioral  

#### 5.4.1 Visual indicator

The **visual indicator** MUST convey the module’s current state using
the following color semantics:

- **Unsolved state**  
  The indicator MUST be **inactive** (off) or black.

- **Solved state**  
  The indicator MUST display **green**.

- **Strike**  
  At the Event of a strike the indicator MUST display **red** for three seconds.
  This MUST override the color of the current module state.   

- **Continuous task**  
  The indicator MUST display **yellow**.

## 6. Recommendations (Non-Normative)

<!--
Strong suggestions, not requirements. Should encourage consistency. 
-->

## 7. Undefined and Reserved Areas

<!--
What is not defined by the specification? Where is room for future versions of the specification to evolve?
-->

## 8. Notes and Rationale

<!--
Explanation of design decisions. Not necessary but can be helpful. 
-->