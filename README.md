
# fast-antx

Fast implementation of the antx text annotation tool. Transfer annotations from one text to another using regex patterns and an optimized diff algorithm.

## Installation

Requires Python 3.8+

### From GitHub

```bash
pip install "git+https://github.com/OpenPecha/fast-antx.git"
```

### From source

```bash
git clone https://github.com/OpenPecha/fast-antx.git
cd fast-antx
# optional but recommended
python -m venv .venv && source .venv/bin/activate
pip install -e .
```

For development:

```bash
pip install -e ".[dev]"
pre-commit install
pytest
```

## Usage

Basic example with custom patterns:

```python
from fast_antx.core import transfer

source = "[1a]Hello\n[1a.1]World"
target = "Hello\nWorld"
patterns = [
    ["pages", r"(\[\d+[ab]\])"],
    ["lines", r"(\[\d+\.\d\])"],
]

# output: "txt" | "yaml" | "diff"
annotated = transfer(source, patterns, target, "txt")
print(annotated)
```

Using built-in HFML tag patterns:

```python
from fast_antx.core import transfer
from fast_antx.ann_patterns import HFML_ANN_PATTERN

layer = "<...>"  # text containing HFML-like tags
base = "..."     # target text to receive transferred annotations

result = transfer(layer, HFML_ANN_PATTERN, base, "txt")
```

Notes:
- On first use, a small `node-dmp-cli` binary is downloaded automatically to `~/.antx/bin/` to speed up diff computation.
- See `tests/` for more examples (e.g., `tests/test_annotation_transfer.py`).

## Contributing

Contributions are welcome!
- Open an issue for bugs or feature requests.
- Fork the repo and create a feature branch.
- Set up dev environment: `pip install -e ".[dev]"` then `pre-commit install`.
- Run tests with `pytest` and include tests for new features.
- Submit a pull request to `main`.

## License (MIT)

This project is licensed under the MIT License. See the `LICENSE` file for details.
