# qevedo

[![CI](https://github.com/qevedo/qevedo/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/qevedo/qevedo/actions/workflows/ci.yml)

The Qevedo quantum toolkit in one install:

```bash
pip install qevedo            # or qevedo[numpy] for NumPy state vectors
```

| Package | Import | What it is |
|---|---|---|
| [`qevedo-compiler`](https://github.com/qevedo/qcc) | `qevedo.compiler` | QCC, a technology-agnostic quantum circuit compiler (and the `qcc` command) |
| [`qevedo-simulator`](https://github.com/qevedo/qevedo-simulator) | `qevedo.simulator` | qvd, a fast simulator: AVX2 state vector, stabilizer, MPS and near-Clifford backends |
| [`openqasm`](https://github.com/qevedo/openqasm) | `openqasm` | OpenQASM 2 and 3 parser and checker, used by the compiler |

Each can also be installed on its own. `qevedo` itself has no code: it
depends on the compiler and the simulator, which share the `qevedo`
namespace.

## Compile, then simulate

```python
from qevedo.compiler import compile_source, emit_qasm
from qevedo.simulator import run

program = """
OPENQASM 3.0;
include "stdgates.inc";
qubit[3] q;
bit[3] c;
h q[0];
cx q[0], q[1];
ccx q[0], q[1], q[2];
c = measure q;
"""

compiled = compile_source(program)   # lowered to the device's native gates
result = run(emit_qasm(compiled), shots=1000)
print(result.counts, result.backend)
```

## Releases

Pushing a tag `vX.Y.Z` that matches `pyproject.toml` builds the package and
publishes it to PyPI through trusted publishing
(`.github/workflows/release.yml`).

## License

MIT. Copyright [Qevedo](https://qevedo.com).
