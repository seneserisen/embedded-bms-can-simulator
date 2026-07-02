# Embedded BMS and CAN Simulator — Copilot Instructions

- Treat the repository as specification-first and currently planned, not as an implemented or validated BMS.
- Read `AGENTS.md`, `docs/project_context.md`, `docs/testing.md`, and `docs/project_status.md` before substantial work.
- Do not let generated code invent thresholds, hysteresis, debounce, state transitions, CAN IDs, bit layouts, scaling, timeouts, counters, checksums, or compliance claims.
- Keep battery plant, measured signals, estimated state, protection logic, protocol encoding, bus adapters, and Python test tooling separated.
- Use explicit units, fixed-width protocol types, deterministic behavior, validated bounds, and documented byte order.
- Add boundary, hysteresis, stale-data, fault, counter-wrap, encode/decode round-trip, invalid-frame, and deterministic-replay tests.
- Do not connect to real batteries, vehicles, or physical CAN hardware without explicit owner approval.
- Do not use proprietary DBC or vehicle information.
- Report planned, implemented, tested, and hardware-validated status separately.
- Never invent build results, bus traces, hardware evidence, or ISO 26262/AUTOSAR compliance.
