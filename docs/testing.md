# Testing and Verification

## Current state

The repository is currently specification-first. No executable C++ or Python baseline is documented yet. Therefore:

- do not report builds, tests, coverage, CAN traffic, or hardware checks as passed;
- first implementation work must add exact commands and CI together with the scaffold;
- documentation review is not a substitute for executable verification.

## Proposed local commands after M1 scaffold

The first C++ scaffold should support commands equivalent to:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build --parallel
ctest --test-dir build --output-on-failure
```

The exact generator, compiler support, warning flags, sanitizers, and dependency setup must be documented when implemented.

## Proposed Python scenario commands after M3

The Python tooling should document an isolated environment and commands equivalent to:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install -e ".[dev]"
pytest
```

Do not add Python packaging until the scenario layer actually requires it.

## Required test categories

### Physical values and validation

- valid nominal values;
- exact minimum and maximum;
- just-inside and just-outside limits;
- NaN, infinity, invalid ranges, and contradictory measurements;
- explicit units and sign conventions;
- conversion overflow and saturation.

### Protection logic

For each protection:

- inactive nominal state;
- threshold entry;
- hysteresis exit;
- debounce duration;
- latching and reset;
- simultaneous faults and priority;
- stale or missing measurement behavior;
- deterministic state transition sequence.

### State-of-charge logic

- initialisation;
- charge and discharge sign convention;
- integration over time;
- saturation at valid bounds;
- invalid current or time step;
- deterministic reference cases;
- documented drift and model limitations.

### CAN protocol

- golden byte vectors;
- encode/decode round trips;
- little- and big-endian behavior as specified;
- signed and unsigned values;
- scale and offset boundaries;
- reserved bits;
- invalid encodings;
- rolling counter and wraparound;
- timeout and stale frames;
- checksum behavior if included;
- unknown frame identifiers;
- malformed frame length.

### Fault campaigns

- sensor stuck-at, bias, drift, dropout, and out-of-range values;
- missing or delayed frames;
- corrupt counters or checksum;
- deterministic replay from a scenario file;
- expected protection and reporting response.

## Safety boundary

Virtual-bus testing does not justify physical CAN or battery testing. Hardware checks require explicit approval, isolated equipment, current and voltage limits, emergency stop, supervision, a rollback plan, and a separate test record.

## CI acceptance for initial implementation

- clean CMake configure and build;
- warnings treated as errors for supported compilers;
- unit tests pass;
- optional sanitizers run in a compatible job;
- no dependency on physical CAN hardware for core CI;
- protocol golden vectors and deterministic scenario tests pass;
- generated documentation and message map are current.

## Baseline status

Until executable files are added, all implementation checks remain **Not implemented**, not passed.
