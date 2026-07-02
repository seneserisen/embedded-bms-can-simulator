# Project Status

- Last updated: 2 July 2026
- Maturity: Planned Portfolio MVP
- Default branch: `main`

## Current repository state

The repository currently contains the project concept and planning material. It does not yet contain a documented executable C++ BMS core, CAN encoder/decoder, Python scenario runner, test suite, or CI implementation.

## Implemented

- high-level project goals;
- planned architecture;
- intended technology and portfolio evidence;
- specification-first governance and verification requirements on the `chore/ai-project-governance` branch.

## Not yet implemented

- battery plant model;
- measurement validation;
- SOC estimator;
- protection state machine;
- CAN signal definitions and encode/decode code;
- virtual bus or SocketCAN adapter;
- Python scenario runner;
- fault campaigns and reports;
- CMake build, unit tests, and CI.

## Highest-priority next tasks

1. Write an architecture decision for the first MVP scope and platform-independent bus boundary.
2. Define physical units, ranges, time base, current sign convention, and synthetic plant assumptions.
3. Define BMS states and protection semantics, including thresholds, hysteresis, debounce, latching, reset, and priority.
4. Define a small original CAN message map with IDs, byte order, bit layout, scale, offset, invalid values, timing, counter, and timeout.
5. Create the minimal C++17/CMake scaffold with pure core logic and tests before adding SocketCAN.

## Primary risks

- generated code inventing engineering requirements;
- accidental use of proprietary DBC or vehicle information;
- ambiguous current sign, units, timing, endianness, or threshold behavior;
- unsafe interpretation of a simulator as a real BMS;
- adding SocketCAN or hardware dependencies before the core is testable;
- claiming ISO 26262, AUTOSAR, hardware, or automotive readiness without evidence;
- overbuilding electrochemical or cloud features before the protection and protocol core works.

## Verification status

| Area | Status |
|---|---|
| Requirements | Partially specified |
| Architecture | High-level plan only |
| C++ build | Not implemented |
| Unit tests | Not implemented |
| CAN golden vectors | Not implemented |
| Python scenarios | Not implemented |
| CI | Not implemented |
| Virtual CAN | Not implemented |
| Physical hardware | Not authorised or validated |

## Status language

Until code and tests exist, describe features as **planned**, not implemented. Virtual simulation must remain separate from physical battery or vehicle validation.
