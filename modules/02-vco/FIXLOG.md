# FIXLOG

This document tracks known issues found in specific PCB revisions and how to correct them.
If you are building from anything other than the latest revision in this repository, review this file before starting your build.

## 🐛 Feb 22, 2026 FIX

**If you ordered the Core board before May 24 2026 you need to apply the following fix manually.** The bug is fixed on the Core boards on May 24, 2026.

#### Affected boards
VCO Core boards, Rev 2 and earlier

#### Sympthoms
- 1V/oct tracking doesn't work.
- The VCO pitch is ceiling at ~70 Hz
- Pitch plateaus and flattens above a certain CV — no further response to increasing CV
- R_BIAS1 trim has no or very little effect on frequency
- TP1 floats at ~1V instead of being servoed to 0V
- U1B output pinned at −10.3V (TL072 negative rail)

#### Assumed reason

The R+O datasheet only characterizes hFE at IC = −10 mA and above, with no minimum specified at low collector currents. The circuit operates Q2 at sub-milliamp currents, where the substituted part has insufficient gain to close the reference current loop that charges the oscillator's cap. U1B saturates against the negative supply rail trying to compensate, leaving Q2's collector current stuck at a fixed (too-low) value regardless of CV input.

#### Fix faulty boards

**TESTED HACK** — Desolder Q2 (SMD component) and hack a 2N3906 on the SDM pads. Be careful to match the emitter/base/collector pins of the 2N3906 properly to the pads of Q2.

**UNTESTED PROPER FIX** — Replace Q2 with ONSEMI version of the same component: MMBT3906LT1G, https://mou.sr/43pMpYO, Mouser Part No: 863-MMBT3906LT1G

#### Solution

**UNTESTED** — The previous BOM specified the generic LCSC part C7420354, which JLCPCB assumed to silently substituted between production batches: batch 1 (Jan 2026) received a working part, while batches 2 and 3 received Zhuhai Hongjiacheng (R+O) MMBT3906 parts under the same C-code.
