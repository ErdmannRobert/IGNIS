# !!! THIS IS NOT A SPECIFICATION !!!  

## The only purpose of this specification is to act as a template for other specifications. Other parts of the project MUST NOT comply with it. 

# IGNIS – <Spec Name> Specification
### Version: <vX.Y>  |  Status: Draft / Stable / Deprecated

## 0. Normative Language

<!--
Specify the meaning of terms used in this specification 
-->

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.


## 1. Purpose & Scope

<!--
Describe what this specification defines and what is explicitly out of scope.
-->

## 2. Definitions & Terminology

<!--
Define any terms used in this spec that could be ambiguous.
-->

**Device**  
A self-contained functional unit within the IGNIS ecosystem. A device
may include electronics, firmware, and mechanical components and
interacts with other devices according to applicable IGNIS specifications.

**Hub**  
A device that acts as the central controller of an IGNIS system. The hub
orchestrates game logic, provides environment parameters, manages user
interaction, and coordinates communication with attached modules.

**Module**  
A device that implements a single physical puzzle and is designed to be
attached to a hub. A module interacts with the hub via the
Hub-Module Connection Specification and reports its status as part of the
overall game.

## 3. Dependencies

<!--
List other specifications this spec relies on.
Avoid circular dependencies.

This specification is independent and does not rely on any other IGNIS specifications.

Compliance with the following specifications is REQUIRED:
- hub_module_connection Specification v0.1
-->


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

### Electronics  

<!--
Connector type, pinout, etc.
-->

### Protocol  

<!--
Communication protocol, services, etc. 
-->

### Mechanical  

<!--
Dimensions, etc.
-->

### Behavioral  

<!--
Game logic, behavior of in/out devices, etc.
-->

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