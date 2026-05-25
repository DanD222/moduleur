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

**OPTION 1** — Desolder Q2 and rotate 180 deg and solder the collector pin (#3) to TP2 (Hi-Frequency test point, which is apparently the collector of Q2), with a short piece of wire. For this fix you might want to buy a few MMBT3906 if the legs of the original accidentally break during desoldering: https://mou.sr/43pMpYO / Mouser Part no: 863-MMBT3906LT1G. TESTED, works.

<img width="1753" height="1361" alt="q2fix-option1" src="https://github.com/user-attachments/assets/a276a65d-875f-4533-b705-0ef0cd4f6cd3" />


---

**OPTION 2** — Desolder Q2 (SMD) and solder a 2N3906 THT component to the SMD pads and the Hi-Freq test point. TESTED, works

<img width="1753" height="1375" alt="q2fix-option2" src="https://github.com/user-attachments/assets/23350349-0c3a-4167-87a6-543c61b5847c" />

Both works the same, there's no preferred way so just do which seems easier and better for you.



#### Board fix

**⚠️ UNTESTED** — The board was fixed on May 24, 2026 but verification is in progress.
