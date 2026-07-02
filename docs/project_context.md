# Project Context

## Identity

- Project: Embedded BMS and CAN Simulator
- Owner: Sadik Enes Erisen
- Maturity: Planned Portfolio MVP
- Intended stack: C++17, CMake, virtual CAN abstraction, optional SocketCAN adapter, Python scenario tooling, automated tests
- Repository visibility: Public

## Purpose

Create a hardware-independent simulator that demonstrates embedded software structure, battery signal processing, protection-state logic, CAN protocol implementation, fault injection, deterministic scenario execution, and engineering verification.

The project must use synthetic or public specifications and must not imply compatibility with a proprietary vehicle, battery pack, DBC, or production BMS.

## Proposed system boundaries

```text
Synthetic battery plant
        |
        v
Measurement and validation layer
        |
        +--> SOC estimator
        |
        +--> Protection state machine
                  |
                  v
          CAN signal model
                  |
          +-------+-------+
          |               |
     Virtual bus      SocketCAN adapter
          |
          v
Python scenario runner and reports
```

## Planned functional scope

- simulated cell voltages, pack current, temperatures, and state of charge;
- over-voltage, under-voltage, over-temperature, and over-current detection;
- explicit hysteresis, debounce, latching, reset, and fault-priority behavior;
- documented BMS operating states;
- periodic CAN frame encoding and decoding;
- documented signal map, byte order, scaling, ranges, invalid values, counters, timeout, and checksum policy;
- sensor and communication fault injection;
- deterministic Python-driven scenarios and reports;
- C++ unit tests and CI.

## Milestone order

### M0 — Specification

- define units, ranges, timing, state machine, protection semantics, and CAN message map;
- define acceptance tests and non-goals;
- record design decisions.

### M1 — Pure C++ core

- typed physical values or clearly centralised conversions;
- deterministic battery plant and measurement validation;
- protection state machine;
- no operating-system or CAN dependency in core logic.

### M2 — Protocol layer

- encode/decode library with fixed-width types;
- round-trip and golden-vector tests;
- counters, timeout, invalid value, and checksum behavior.

### M3 — Scenario and bus layer

- platform-independent virtual bus;
- Python scenario runner;
- reports and fault campaigns;
- optional SocketCAN adapter separated from core logic.

### M4 — Portfolio demonstration

- reproducible scenarios;
- architecture and message-map documentation;
- CI evidence;
- clear limitations and no hardware claims.

## Core invariants

1. Plant truth, measured values, estimated values, protection state, and transmitted signals remain separate.
2. Units, ranges, sign conventions, sample periods, and byte order are explicit.
3. Protection transitions are deterministic and testable.
4. Invalid or stale inputs lead to documented safe behavior.
5. Protocol encode/decode operations are bounded and validated.
6. No proprietary thresholds, DBC content, or vehicle data is used.
7. Simulation evidence is not hardware or functional-safety evidence.

## Non-goals for the first MVP

- real battery or vehicle connection;
- contactor or charger control;
- electrochemical cell modelling;
- production SOC/SOH accuracy;
- AUTOSAR integration;
- ISO 26262 compliance;
- real-time guarantees;
- proprietary DBC compatibility;
- cloud dashboards or mobile applications.

## Definition of done for the first MVP

- [ ] Requirements, units, state machine, thresholds, and CAN map are documented.
- [ ] Pure core logic builds without SocketCAN.
- [ ] Protection boundaries, hysteresis, debounce, latching, reset, and priority are tested.
- [ ] CAN encode/decode has golden vectors and round-trip tests.
- [ ] Fault and stale-data scenarios are deterministic.
- [ ] Python scenarios produce reproducible reports.
- [ ] CI builds and tests the supported platforms.
- [ ] No proprietary information or unsupported safety claim is present.
- [ ] Enes can explain the architecture, protocol, state transitions, tests, and limitations.
