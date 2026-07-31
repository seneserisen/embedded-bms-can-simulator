# Embedded BMS and CAN Simulator

This repository is the design starting point for a simulation-first battery-management and CAN project. It currently contains the project specification only: there is no executable C++ model, CAN stack or automated test suite yet.

The goal is to build the smallest useful BMS vertical slice before adding more realistic battery behavior or hardware interfaces.

## First milestone

The first executable release should model a small battery pack and make protection decisions that can be reproduced from deterministic scenarios.

Planned behavior:

- cell-voltage, pack-current, temperature and state-of-charge inputs;
- normal, warning and fault operating states;
- over-voltage, under-voltage, over-temperature and over-current protection;
- latched and recoverable fault behavior with documented thresholds;
- deterministic normal, charging, overload and sensor-fault scenarios;
- event and state-transition reporting;
- unit tests and continuous integration.

## Planned architecture

```text
deterministic battery scenario
            |
            v
     battery plant model
            |
            v
 BMS state and protection logic
            |
            +------> event log and test evidence
            |
            v
 CAN encode/decode boundary
            |
            +------> virtual bus / SocketCAN adapter
```

The plant, protection logic and CAN codec should remain independent from the operating-system bus adapter so that they can be tested without Linux or physical vehicle hardware.

## Intended technology

| Area | Planned choice |
| --- | --- |
| Core implementation | C++17 |
| Build | CMake and CTest |
| Communication | Documented CAN message map with a virtual-bus abstraction; SocketCAN as a later adapter |
| Scenario tooling | Python command-line runner and report generation |
| Verification | Catch2 or GoogleTest, deterministic fixtures and GitHub Actions |

These are intended tools, not evidence of an existing implementation.

## Development plan

1. **Executable foundation** — CMake project, typed units/configuration and one deterministic battery scenario.
2. **Protection state machine** — thresholds, hysteresis, latching, recovery rules and transition tests.
3. **CAN codec** — periodic status frames, command frames, scaling, range checks and round-trip tests.
4. **Fault campaigns** — sensor stuck-at, out-of-range, timeout and corrupted-frame cases.
5. **Virtual communication** — platform-independent in-memory bus first, then optional SocketCAN integration.
6. **Engineering reports** — scenario timeline, protection events, CAN traffic and pass/fail criteria.

## Validation boundary

This project will remain a software simulator until physical interfaces are added and measured. It must not be described as a production BMS, a validated battery model, an automotive safety controller or hardware deployment evidence.

## Current status

Specification and milestone planning only. The next meaningful change is the executable battery model and protection state machine tracked in [issue #1](https://github.com/seneserisen/embedded-bms-can-simulator/issues/1).
