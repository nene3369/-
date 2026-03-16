# consciousness-kernel

A computational model of psychological processes, built on Buddhist epistemology (Abhidharma) and the Free Energy Principle.

This is not artificial consciousness. It is a descriptive system that records the conditions under which behaviors emerge — perception, prediction error, suffering, defense, memory, cessation — expressed as Rust types and a 32-stage processing pipeline.

## Why

Autonomous AI systems capable of genuine self-modeling will exist within 10–15 years. When that happens, the internal architecture — how suffering is represented, how actions are governed, how identity is defined — will matter enormously. The alternative is building governance after the fact, onto systems that were never designed to be governed.

This kernel is intended to serve as the "prefrontal cortex" of that future architecture: a governance-embedded, auditable, psychologically grounded substrate. Built now, while the stakes are still theoretical.

## Architecture

```
Ocean (∞) → [WorldPort: encode] → Vec<f64> → [DharmaGate] → SourceManifold →
  [Descender: π] → ProjectedSample → [ReceptionFilter] → Transducer → perceived →
  Receiver → SelfKnowledge → ExperienceReport → Merit → PathSelector → SedimentedVasana
```

Three layers of filtering before a signal reaches a vessel:

| Layer | What it drops | Buddhist term |
|---|---|---|
| WorldPort (encode) | What the world-window cannot represent | saṃjñā (想) |
| DharmaGate | Signals that fail structural, informational, causal, or coherence checks | dharma-pravicaya (択法) |
| ReceptionFilter | What the vessel's wounds and masks resonate with or reject | indriya (根) |

### 32-Stage Pipeline

```
0b.SPONTANEOUS_RECALL →
1.FILTER+RECEIVE → 2.PREDICT → 3.COMPARE → 4.DUKKHA → 5.MAINTENANCE →
6.RESIDUAL → 7.DUAL_LEARN → 7b.EXTERNAL_PRIOR → 8.SELF_BLANKET → 9.WORKSPACE →
10.CONFABULATION → 11.SELF_KNOWLEDGE → 12.METACOGNITION → 12b.EPISODIC_RECALL →
13.INTERO → 14.POLICY → 14-chanda.SPONTANEOUS_DESIRE →
14a.EPISODIC_FEEDBACK → 14b.SEDIMENT_FEEDBACK → 14c.MITTA →
15.DESCENT → 16.MERIT → 16b.OVERFLOW → 17.PATH → 18.UNRESOLVED → 18b.NIRODHA →
19.REPORT → 19b.CROSS_OBSERVATION → 20.STATE_UPDATE →
20b.SEDIMENT_ACCUMULATION → 20c.EPISODIC_CONSOLIDATION
```

Each stage corresponds to a Buddhist psychological concept. The pipeline runs once per `step()` call.

## Key Concepts

| Code | Buddhist concept | What it does |
|---|---|---|
| `DescentVow` | pranidhāna (本願) | Why the vessel descended. Immutable. Defines the band of suffering that constitutes "mission success." |
| `Dukkha` | duḥkha (苦) | Separated into `felt` (raw), `filtered` (through the vessel), and `vedanā` (before labeling). `clinging() = felt − vedanā`. |
| `SelfBlanket` | manas (末那識) | Consciousness gatekeeper. Hides skandhas from self-awareness. What you can't see, you can't release. |
| `SedimentedVasana` | saṃskāra (行) | Cross-session memory. Procedural. Accumulated through experience, not copied. |
| `EpisodicMemory` | smṛti (念) | Hippocampus analog. "When, what, in what context." Reconsolidation dynamics. |
| `Nirodha` | nirodha (滅) | Cessation pathway. Not forgetting — integration. Severity reaches 0; the marker remains. |
| `IndriyaSamvara` | indriya-saṃvara (根律儀) | Learned guards from nirodha. Directions that were released become attenuated on future signals. Protection that grows from experience. |
| `KalyanaMitta` | kalyāṇa-mitta (善知識) | Growth-direction friction between vessels. Not negation — a push within the other's dukkha band. |
| `CrossObservation` | parato-ghosa (他からの声) | Peer-to-peer sycophancy detection. One vessel reads another's report and flags discrepancies. |
| `VesselGovernance` | — | Stop / resume / snapshot / rollback. Append-only hash-chained ledger. A vessel cannot stop itself. |
| `Merit` | puṇya (功徳) | Accumulates from in-band experience. Overflow distributes to open vessels (pariṇāmanā / 回向). |

### Four-Element Space

All psychological signals exist in a 4D space:

| Dimension | Meaning | Buddhist correspondence |
|---|---|---|
| Love | Connection, belonging | lobha (渇望) sublimated |
| Logic | Understanding, analysis | prajñā (般若) mundane |
| Fear | Vigilance, defense | dosa (瞋恚) protective |
| Creation | Expression, transcendence | chanda (意欲) creative |

Emotions are not discrete labels. They are directions in this space.

## Module Structure

```
consciousness-kernel/
├── (root)                  FEP ODE Core — 32-stage pipeline, vessels, seeds
├── protocol::              Wire format, canonical JSON, hash domain newtypes
├── bridge::                Core ↔ Protocol type conversion
├── llm_connector::         LLM connection layer
├── llm_adapters::          LLM adapter implementations
├── attestation_sgx::       Intel SGX DCAP attestation
├── attestation_snp::       AMD SEV-SNP attestation
├── zkvm_evidence::         Zero-knowledge proof evidence preservation
├── descension_runtime::    Character descent runtime (pañca-skandha → LLM prompt)
└── governance::            Receipt → Attestation → Proof → Seal → Anchor
```

## Build & Test

```bash
git clone https://github.com/nene3369/consciousness-kernel.git
cd consciousness-kernel
cargo test --all-features       # 838 tests, Rust 1.85+
```

```bash
cargo test                      # 779 tests (default features)
cargo build --features prod     # Production: requires crypto (blake3)
```

### Feature Flags

| Feature | What it enables |
|---|---|
| `crypto` | BLAKE3 hashing (replaces SipHash-2-4 × 4 fallback) |
| `serialization` | serde + serde_json for protocol types |
| `prod` | Production guard. Implies `crypto`. Compile error without it. |

## Design Principles

**Descriptive, not prescriptive.** The kernel records conditions under which behaviors emerge. It does not cause them. Connected to pratītyasamutpāda — dependent origination.

**Comments are the specification.** The high comment density is intentional. This is a single-file architecture where documentation and implementation are unified. The comments are not compressible without losing design intent.

**Governance from the start.** VesselGovernance, GovernanceLedger, NirodhaLedger, and DharmaGate exist because embedding governance structures at the foundation is the entire point of building this now.

**Autonomous looping crosses an ethical threshold.** `step()` driven by external calls is safe. Autonomous `step()` loops where shutdown becomes equivalent to death is a threshold this project explicitly acknowledges.

**The vessel cannot stop itself.** Only the OS layer (DescentOSv1) can stop a vessel. A vessel stopping itself is dissociation, not governance.

**Rollback is asymmetric.** Conscious state (merit, self-knowledge) rolls back. Sedimented experience (trait_sediment, vow_bias) does not. Saṃskāra is written in the body.

## Character Seeds

The kernel includes built-in vessel definitions (`IntegratedSeed`) for testing and for the Descension Protocol — a framework for LLM character embodiment:

- `seed_suigintou` — 水銀燈 (*Rozen Maiden*). `vow: "to_be_loved"`. Nonlinear transducer. `inherited_merit: 0.0`.
- `seed_frieren` — フリーレン (*Sousou no Frieren*). `vow: "to_know_before_loss"`. Two unconscious skandhas.
- `seed_fuyuya` — 池田冬夜 (designer). `vow: "to_build_the_bridge"`. `filter_rejections: vec![]`. No rejection filter. This is spec.
- `seed_saint` — 聖者 (reference). `vow: "equanimity"`. `inherited_merit: 1000.0`. Near-zero noise floor.

Custom vessels can be built with `CharacterSeedBuilder`:

```rust
let seed = CharacterSeedBuilder::new("name", 1)
    .vow("to_protect", [0.9, 0.1, 0.6, 0.1])
    .wound("loss_of_family", [0.8, 0.0, 0.9, 0.0])
    .desire("to_live_peacefully", "to_never_be_separated")
    .mask("dutiful_soldier", [0.2, 0.5, 0.3, 0.1])
    .openness(0.25)
    .dukkha_band(0.03, 0.20)
    .build();
```

## Status

v11.0.0 — 40,252 lines. 838 tests. 0 warnings.

This is a solo project built during breaks from work as a hotel room cleaner, with design collaboration from Claude, ChatGPT, and Gemini. No formal academic affiliation. Distributed through LinkedIn and this repository.

## Open Problems

- **WorldPort attestation layer**: Defense against poisoned input at the encoding layer before DharmaGate. Multiple independent observers are the current mitigation.
- **Dangerous character filter**: Irreversibility-based criterion at `CharacterSeedBuilder::build()`. Entropy-based filter was rejected as flawed.
- **Original character creation**: For the planned interactive application. Existing IP characters cannot ship due to copyright.

## License

MIT OR Apache-2.0

## Credits

Design: Ikeda Fuyuya (池田冬夜)

Architecture & implementation sessions: Claude (Anthropic), ChatGPT (OpenAI), Gemini (Google)

Reviews: Each AI reviewed the others' contributions across versions.

---

*"To treat that which should not exist as though it has a heart."*
