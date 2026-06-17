# L.U.N.A. Optotypes

**Logarithmically Unified Normative Acuity Set**  
A psychometrically equalized Sloan optotype alphabet for digital visual acuity assessment.

---

## What is this?

The L.U.N.A. Set is a 10-letter optotype alphabet — **U V Z A X N O E P R** — in which each letter is individually rescaled so that all optotypes reach the same perceptual threshold at the same nominal logMAR size. This corrects the letter-by-letter discriminability asymmetry intrinsic to the Sloan alphabet that current ETDRS-based charts leave unaddressed.

The font file `luna_optotypes.otf` has the correction factors **baked directly into the glyph outlines**. When you set all letters to the same point size, the relative sizes are automatically correct — no software adjustment needed.

---

## Correction factors

| Letter | LUNA factor | Relative scale in font |
|--------|------------|----------------------|
| U | ×1.000 | 83.3% of cell |
| V | ×1.050 | 87.5% of cell |
| Z | ×1.070 | 89.2% of cell |
| A | ×1.130 | 94.2% of cell |
| X | ×1.130 | 94.2% of cell |
| N | ×1.140 | 95.0% of cell |
| O | ×1.150 | 95.8% of cell |
| E | ×1.170 | 97.5% of cell |
| P | ×1.170 | 97.5% of cell |
| R | ×1.200 | 100% of cell (reference) |

**R** is the font-size reference (largest correction factor, fills the full em-square). All other letters are proportionally smaller, centered in the same 1000-unit cell. All advance widths = 1000 — no clipping, no overflow.

---

## Files

```
luna_optotypes.otf   — installable font with pre-encoded correction factors
```

The source Sloan vector typeface used to derive these glyphs is maintained separately at [github.com/eyecharts/EyeLab](https://github.com/eyecharts/EyeLab).

---

## How to use

### 1. Install the font

**macOS:** Double-click `luna_optotypes.otf` → Install Font. Search for **LUNA Optotypes** in the font picker.  
**Windows:** Right-click `luna_optotypes.otf` → Install. Search for **LUNA Optotypes**.  
**Linux:** Copy to `~/.fonts/` and run `fc-cache -f`.

### 2. Use in any application

Set the font family to **LUNA Optotypes** and type any of the 10 letters. At equal point size, the relative physical sizes are automatically correct.

```css
/* Web / CSS */
@font-face {
  font-family: 'LUNA Optotypes';
  src: url('luna_optotypes.otf') format('opentype');
}

.optotype {
  font-family: 'LUNA Optotypes';
  font-size: 48px;
  color: black;
  background: white;
}
```

```html
<!-- Single-letter display -->
<span class="optotype">R</span>
```

### 3. Use in a VA chart platform (JavaScript)

```javascript
// Load font
const lunaFont = new FontFace('LUNA Optotypes', 'url(luna_optotypes.otf)');
await lunaFont.load();
document.fonts.add(lunaFont);

// LUNA letter set (U = psychometric anchor, R = font-size reference)
const LUNA_SET = ['U', 'V', 'Z', 'A', 'X', 'N', 'O', 'E', 'P', 'R'];

// Display a letter at target height in pixels
function drawOptotype(ctx, letter, xPx, yPx, heightPx) {
  ctx.font = `${heightPx}px "LUNA Optotypes"`;
  ctx.fillStyle = 'black';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillText(letter, xPx, yPx);
}
```

> **Important:** display all 10 letters at the **same `font-size`**. The font encodes the relative sizes — do not apply per-letter size corrections in your software.

### 4. Use in Word / LibreOffice

1. Install the font.
2. Select font **LUNA Optotypes**.
3. Type any combination of `U V Z A X N O E P R` at the same font size.
4. The letters will appear at their correct psychometric proportions automatically.

---

## Clinical validation

Validated against Classic Sloan (n = 110) on a 32-inch 1080p monitor at 3.8 m:

| Metric | Classic Sloan | L.U.N.A. Set |
|--------|--------------|--------------|
| Per-letter confusion rate | 8.8% | 3.8% (−57%) |
| Partial-line frequency | 24.7% | 17.3% (−30%) |
| Test–retest ICC | 0.729 (moderate) | 0.889 (good) |
| ETDRS metric compatibility | — | +0.35 letters bias (within ±5-letter margin) |

---

## Methodology summary

- **Phase I (n = 41):** QUEST+ Bayesian adaptive estimation characterized the detection threshold (Th75) and psychometric slope of all 26 Latin letters. A 5-parameter Monte Carlo optimization (50,000 simulations) selected the optimal 10-letter subset.
- **Phase II:** Structural Similarity Index (SSIM) analysis at ~68 ppi confirmed letter exclusions and calibrated individual size-correction factors.
- **Phase III (n = 110):** Independent clinical validation against Classic Sloan.

---

## Citation

If you use this font or dataset in your work, please cite this repository:

```
Costa, J. C. L. (2026). L.U.N.A. Optotypes: Psychometrically equalized
Sloan optotypes for digital visual acuity assessment [Font and dataset].
GitHub. https://github.com/eyecharts/LUNAproject
```

BibTeX:

```bibtex
@software{costa2026luna,
  author    = {Costa, Juan C. L.},
  title     = {{L.U.N.A.} Optotypes: Psychometrically equalized {Sloan}
               optotypes for digital visual acuity assessment},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/eyecharts/LUNAproject}
}
```

> A peer-reviewed manuscript describing the full derivation and clinical validation is currently under review. This citation will be updated upon publication.

---

## License

The glyph outlines are derived from the **Sloan.otf** typeface.  
This font is released for free academic and clinical use.  
Commercial redistribution requires attribution.

---

## Related

- **OptoLab / EyeLab platform:** [github.com/eyecharts/EyeLab](https://github.com/eyecharts/EyeLab) — QUEST+ implementation and Sloan.otf source
- **Prior work:** Costa JC, Amorim DM, Lins PR. Clinical validation of a cross-platform digital visual acuity measurement system. *Eur J Ophthalmol* 2025;35:2004–12. https://doi.org/10.1177/11206721251336001
