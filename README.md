# Embedded BMS and CAN Simulator

A planned C/C++ portfolio project for simulating battery-management logic and CAN communication without requiring proprietary vehicle hardware.

## Project goals

- Simulate cell voltages, pack current, temperature, and state of charge
- Implement over-voltage, under-voltage, over-temperature, and over-current protection
- Encode and decode periodic CAN frames using a documented message map
- Inject sensor and communication faults for verification
- Provide a Python test client for automated scenario execution
- Build and test the project in GitHub Actions

## Planned architecture

```text
Battery plant model
        |
        v
BMS state estimator + protection logic
        |
        v
CAN message encoder / decoder
        |
        +--> SocketCAN or virtual bus
        |
        +--> Python scenario runner and reports
```

## Planned technology

- C++17
- CMake
- SocketCAN or a platform-independent virtual CAN abstraction
- DBC-style signal definitions
- Python test tooling
- GoogleTest or Catch2
- GitHub Actions

## Intended evidence

The finished repository will demonstrate embedded software structure, state estimation, fault handling, communication protocols, automated tests, and engineering documentation.

## Status

Project specification and milestone planning are in progress. Implementation will begin after the industrial-quality anomaly-monitor project reaches its first stable release.

## Author

Sadik Enes Erisen — M.Sc. Autonomy Technologies, FAU Erlangen-Nürnberg; B.Sc. Electrical and Electronics Engineering.
