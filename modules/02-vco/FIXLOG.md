# FIXLOG

This document tracks known issues found in specific PCB revisions and how to correct them.
If you are building from anything other than the latest revision in this repository, review this file before starting your build.

## 🐛 May 24, 2026 FIX

**If you ordered the Core board before May 24 2026 you need to apply the following fix manually.** The fix is being verified on the Core boards onwards May 24, 2026.

#### Affected boards
VCO Core boards, Rev 3 and earlier

#### Sympthoms
- 1V/oct tracking doesn't work.
- The VCO pitch is ceiling at ~70 Hz
- Pitch plateaus and flattens above a certain CV — no further response to increasing CV
- R_BIAS1 trim has no or very little effect on frequency
- TP1 floats at ~1V instead of being servoed to 0V
- U1B output pinned at −10.3V (TL072 negative rail)

#### Reason

For Q2, pin numbering was incorrectly following 2N3906 (TO-92, EBC) instead of MMBT3906 (SOT-23, BEC). Previous production used the SMD MMBT3906 with traces routed to the wrong pads, leaving the transistor operating in reverse-active mode. This barely worked with some manufacturer's parts and failed entirely with others, producing a uniform pitch ceiling at ~70 Hz across all affected units.

#### Fix faulty boards

**TESTED THT HACK** — Desolder Q2 (SMD component) and hack a 2N3906 on the SDM pads. Make sure to match the emitter/base/collector pins of the 2N3906 properly to the pads of Q2.

**⚠️ UNTESTED SMD HACK** — Desolder Q2 and resolder in a "deadbug" position so that the actual pins match the footprint.

#### Board fix

**⚠️ UNTESTED** — The board was fixed on May 24, 2026 but verification is in progress.
