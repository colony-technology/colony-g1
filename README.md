# colony g1

public circom circuit fixtures for [colony.technology](https://colony.technology).

```text
COLONY G1
──────────────────────────────────────────────────────────────

18 colony fixtures  ──►  circom 2.x  ──►  speedrunpapi@0.7.6
                                              │
                                              ├─ Certified (exit 0)
                                              └─ Broken    (exit 2)
```

## status

status, 10 november 2026: this corpus was originally published with earlier speedrunpapi builds that matched source patterns instead of analysing the compiled constraint system. the timing comparison under `replay22/` measured that pattern lookup against a solver and is withdrawn.

the fixtures themselves are sound test material with known ground truth. [speedrunpapi 0.7.6](https://github.com/colony-technology/speedrunpapi) compiles each circuit with circom, analyses the r1cs for output determinism, and returns the exact verdict below for all 18 fixtures with an independently replayable derivation or two checked witnesses.

`speedrunpapi@0.3.2` commands and files under `replay22/` stay only as an archive of what was originally published.

## run

requires circom 2.x and node.js 20+.

```bash
git clone https://github.com/colony-technology/colony-g1.git
cd colony-g1
npx --yes speedrunpapi@0.7.6 scan carry/modsum_safe_n4.circom -l lib/circomlib/circuits
```

exit codes: `0` when `Certified`, `2` when `Broken` (including deliberate negative fixtures).

## fixtures

```text
circuit                          verdict     file
───────────────────────────────────────────────────────────────────────────────────────
modsum_safe_n4                   Certified   carry/modsum_safe_n4.circom
modsum_safe_n8                   Certified   carry/modsum_safe_n8.circom
modsum_safe_n16                  Certified   carry/modsum_safe_n16.circom
modsum3_safe_n4                  Certified   carry/modsum3_safe_n4.circom
full_adder_bits                  Certified   carry/full_adder_bits.circom
shared_input_parallel_m3_w8      Certified   carry/shared_input_parallel_m3_w8.circom
cascade3_safe_n4                 Certified   carry/cascade3_safe_n4.circom
limb_add_safe_n4_k2              Certified   limb/limb_add_safe_n4_k2.circom
limb_add_safe_n4_k4              Certified   limb/limb_add_safe_n4_k4.circom
limb_add_safe_n8_k4              Certified   limb/limb_add_safe_n8_k4.circom
u4_add_safe_k8                   Certified   bitvm_model/u4_add_safe_k8.circom
full_adder_no_bit_checks         Certified   buggy/full_adder_no_bit_checks.circom
modsum_no_bitify_n4              Broken      buggy/modsum_no_bitify_n4.circom
modsum_carry_not_bit_n4          Broken      buggy/modsum_carry_not_bit_n4.circom
limb_add_missing_range_n4_k2     Broken      buggy/limb_add_missing_range_n4_k2.circom
u4_add_buggy_k8                  Broken      bitvm_model/u4_add_buggy_k8.circom
shared_input_no_bitify_m3_w8     Broken      buggy/shared_input_no_bitify_m3_w8.circom
cascade3_no_bitify_n4            Broken      buggy/cascade3_no_bitify_n4.circom
```

## upstream

the 18 circuits use standard relative circom includes. required `lib/circomlib/` files are vendored with their original upstream notices and licenses from `0KIMS/circomlib`, separate from the original colony fixtures.

the four additional g1 cases (`test_bigadd_15.circom`, `test_bigadd_23.circom`, `BinSum@binsum.circom`, and circomlib sha-256 compression) are pinned under `replay22/upstream/`. see [replay22/README.md](replay22/README.md), [colony.technology/leaderboard](https://colony.technology/leaderboard), and [colony.technology/checker](https://colony.technology/checker).
