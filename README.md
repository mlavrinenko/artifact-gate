# artifact-gate

[![CI](https://github.com/mlavrinenko/artifact-gate/actions/workflows/ci.yml/badge.svg)](https://github.com/mlavrinenko/artifact-gate/actions/workflows/ci.yml)
[![crates.io](https://img.shields.io/crates/v/artifact-gate.svg)](https://crates.io/crates/artifact-gate)
[![License: MIT](https://img.shields.io/crates/l/artifact-gate.svg)](LICENSE-MIT)

Plane-agnostic structural rule engine: match a node tree against require/forbid/order/allow path rules, emit diagnostics

## Install

```bash
cargo add artifact-gate
```

## Usage

```rust
use artifact_gate::{Node, Matcher, Rule, Action, run_rules};

let roots = vec![Node {
    kind: "heading".to_owned(),
    text: "Summary".to_owned(),
    line: 1,
    children: vec![],
}];
let rule = Rule::path(vec![Matcher::exact("Summary")], Action::Require)
    .expect("non-empty path");
assert!(run_rules(&roots, &[rule]).is_empty());
```

## Development

Prerequisites: [Nix](https://nixos.org/) with flakes enabled.

```bash
direnv allow         # or: nix develop

just check           # fmt + clippy + tests + file-size + drift check
just build
just test
just cover           # code coverage (70% minimum)
just fmt             # format code
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for coding conventions.

## License

MIT
