# PS1 — Honesty Through Two-Way Verification

**Zhengjun He** · Duke Kunshan University
COMSCI/ECON 206 Computational Microeconomics · Autumn 2026 Session 1
Instructor: Prof. Luyao Zhang · Workshop 6

## The research question

Free generation makes both a deliverable and the documentation meant to vouch for it
nearly costless, while independent verification stays expensive. When anyone can
fabricate the evidence, the question is not what to disclose but **which mechanisms
make honest disclosure an equilibrium**.

The proposal identifies two mechanisms that act as substitutes:

```
    delta + pF  >  25
```

- **`pF`** — the expected fine, paid only by a detected fake
- **`delta`** — a market premium, paid only for a verifiable trace file
- **`25`** — the fake's cost advantage under the calibrated payoff law

A premium of 25 removes the need to fine at all. A premium of 15 halves the required
spot-check rate from 0.50 to 0.20.

## Contents

| Path | What it is |
|---|---|
| `main.tex` | Paper identity, metadata, Figure 1 and the teaser caption |
| `sections/proposal.tex` | Five numbered main sections, 2056 statement, Open Science Statement, SDG 4 statement |
| `appendices/supporting.tex` | Author Notes, references, Appendices A–E |
| `references.bib` | 12 cited works |
| `figures/ps1_teaser.drawio` | **Figure 1, editable master** (draw.io / diagrams.net) |
| `figures/ps1_teaser.pdf` | Figure 1, vector PDF used by LaTeX |
| `colab/trace_or_fake_psweep.ipynb` | **Colab notebook** — re-derives the payoff table, runs the fine sweep and the premium sweep |
| `colab/notebook_output.txt` | Verified run output (also reproduced in Appendix A) |
| `preview.pdf` | Compiled paper (2 main pages + supporting pages) |

## Reproducing the result

The notebook needs no API key, no paid service and no third-party package — Python 3
standard library only.

1. Open `colab/trace_or_fake_psweep.ipynb` in [Google Colab](https://colab.research.google.com).
2. Choose **Runtime → Run all**.
3. The notebook prints the payoff table, runs six checks (all pass), and reports:

```
Best response with no rules: C_fake       <- the market failure
Threshold p* = 0.5000  (fine F = 50.0)
Fake's advantage over honest+verified, at p = 0: +25.0
Combined threshold:  delta + p*F  >  25
  delta= 0 -> p* = 0.5000 at F=50
  delta=15 -> p* = 0.2000 at F=50
  delta=25 -> p* = 0.0000: no enforcement needed
```

## Two corrections recorded in the paper

Both were found by running the notebook, and both are documented in Appendix B.

**1. Sign error.** The first payoff law summed a cost index, a benefit index and a
stability index. Cost and benefit have opposite sign conventions, so summing them
scored honesty as better on *both* and made the fake worse on both. The spot-check
sweep then returned `p* = 0`: faking was never attractive, so **the rule question
could not be posed at all.** The corrected law enters cost negatively.

**2. Honesty was a cost, not an asset.** After fixing the sign, honest and faked
traces still earned the same base benefit, so honesty won only by avoiding a penalty —
a tax, not a signal. Reading Mäkimattila, Shang & Shirakawa (ACM EC 2025), where a
sender's *choice* among offered tests is itself informative, prompted adding the
premium `delta`. The proposal can now show that honesty wins **because it is worth
more**, not merely because cheating is punished.

## Interactive demo

A browser-run simulator of the same decision: https://huggingface.co/spaces/Peterhe123/Trust

The Space is static client-side HTML/CSS/JavaScript with no backend, database, API key
or paid service. It shares one payoff law with the notebook, so the two cannot disagree.

## Build

```
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

Or upload the repository to Overleaf, set the main document to `main.tex` and the
compiler to **pdfLaTeX**.

## AI-use disclosure

All substantive work — the research question, the payoff law, the strategy matrix, both
corrections to that law, the threshold `delta + pF > 25`, the computational checks, the
game, the notebook and the argument of the paper — is the author's own. Every source was
read and every number re-derived by the author, who played the game and ran the checker.

A generative AI assistant (DeepSeek, `deepseek-v4-flash`, 6 September 2026) was used
only for LaTeX typesetting and layout, and for brainstorming possible literature to look
up. It did not devise the model, run any computation, or write the argument. All
literature it suggested was independently located and verified before citation. Initial
reasoning and handwritten reflection are Human-Only. Full disclosure is in Appendix A.1
of the paper.

## License and reuse

`acmart.cls` and `ACM-Reference-Format.bst` are the ACM Master Article Template
(LaTeX Project Public License). Where third-party specifications are referenced — the
SLSA specification, CKAN — their own licences apply and are credited in the paper.
