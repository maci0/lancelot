# Relumea Python 3.15 binding maintenance

This build derives from williballenthin/lancelot commit
`9de1820bf36872175a08987882dc42f6112d2f44` and preserves its Apache-2.0 grants.
The original python-flirt 0.10.2 source archive has SHA256
`f180d7fcdc110cbc5197d27c58fe7cd57adc2eead0a0b562d47ab0b0a85a3b20`.

The maintained distribution is `python-flirt==0.10.2+relumea.1`. Its Rust parser
crate remains `lancelot-flirt==0.10.2`; parser and matching algorithms, signatures,
and binary formats are unchanged. The Python binding selects PyO3 0.30.1 and
explicitly preserves Clone extraction with `#[pyclass(from_py_object)]`, as the
PyO3 migration guide requires. The workspace contains the same two members as
the original Python source archive. Other upstream project components are not
part of this binding build. Existing producer identities remain immutable;
artifacts produced using this binding must record its actual new distribution
version, source identity and native module SHA256.

Build inputs are Cargo.lock, Rust 1.99.1 and maturin 1.15.0 (all published backend
artifact hashes are in build-requirements.txt). Linux production wheels use the
pinned manylinux 2.28 image in Dockerfile.manylinux. Build with no ABI-forward
compatibility environment override. cp315 and cp314 are separate native builds;
free-threaded wheels and a switch to the stable ABI are outside this change.

Validation includes all upstream Python parser/matcher fixtures, the Rust parser
suite, retained-producer parsing in downstream consumers and byte-identical
rebuilds with SOURCE_DATE_EPOCH=1792886400. Source, wheel and native module hashes
are recorded alongside the published assets. Public maintained releases belong
to the user-owned fork; upstream tags are never replaced.
