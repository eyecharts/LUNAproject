# L.U.N.A. Optotypes

**Logarithmically Unified Normative Acuity Set**  
A psychometrically equalized Sloan optotype alphabet for digital visual acuity assessment.

LUNA correction factors pre-encoded in the font file.
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

**U** is the psychometric anchor (lowest correction factor). **R** is the font-size reference (largest glyph, fills the full em-square). All letters share the same 1000-unit advance width and fit within the 1000×1000 UPM bounding box — no clipping, no overflow.

---

## Files

```
luna_optotypes.otf   — installable font with pre-encoded correction factors
```

The source Sloan vector typeface used to derive these glyphs is maintained separately at [github.com/eyecharts/EyeLab](https://github.com/eyecharts/EyeLab).

---

## How to use

### 1. Install the font

**macOS:** Double-click `luna_optotypes.otf` → Install Font.  
**Windows:** Right-click `luna_optotypes.otf` → Install.  
**Linux:** Copy to `~/.fonts/` and run `fc-cache -f`.

### 2. Use in any application

Set the font family to **L.U.N.A. Optotypes** and type any of the 10 letters.  
At equal point size, the relative physical dimensions are automatically correct.

```css
/* Web / CSS */
@font-face {
  font-family: 'LUNAOptotypes';
  src: url('luna_optotypes.otf') format('opentype');
}

.optotype {
  font-family: 'LUNAOptotypes';
  font-size: 48px;   /* all 10 letters will render at correct relative sizes */
  color: black;
  background: white;
}
```

```html
<!-- Example: single-letter display -->
<span class="optotype">R</span>
```

### 3. Use in a VA chart platform (JavaScript)

```javascript
// Load font
const lunaFont = new FontFace('LUNAOptotypes', 'url(luna_optotypes.otf)');
await lunaFont.load();
document.fonts.add(lunaFont);

// LUNA letter set in order (U = psychometric anchor)
const LUNA_SET = ['U', 'V', 'Z', 'A', 'X', 'N', 'O', 'E', 'P', 'R'];

// Display a letter at 0.0 logMAR on a canvas
function drawOptotype(ctx, letter, xPx, yPx, heightPx) {
  ctx.font = `${heightPx}px LUNAOptotypes`;
  ctx.fillStyle = 'black';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillText(letter, xPx, yPx);
}
```

> **Important:** all 10 letters must be displayed at the **same `font-size`**. The font encodes the relative sizes — do not apply per-letter size corrections in your software.

### 4. Use in Word / LibreOffice

1. Install the font.
2. Select font **L.U.N.A. Optotypes**.
3. Type any combination of `U V Z A X N O E P R` at the same font size.
4. The letters will appear at their correct psychometric proportions automatically.

---

## Clinical validation

The L.U.N.A. Set was validated against Classic Sloan (n = 110) on a 32-inch 1080p monitor at 3.8 m:

| Metric | Classic Sloan | L.U.N.A. Set |
|--------|--------------|--------------|
| Per-letter confusion rate | 8.8% | 3.8% (−57%) |
| Partial-line frequency | 24.7% | 17.3% (−30%) |
| Test–retest ICC | 0.729 (moderate) | 0.889 (good) |
| ETDRS metric compatibility | — | +0.35 letters bias (within ±5-letter margin) |

---

## Methodology

Letter selection and calibration involved three phases:

- **Phase I (n = 41):** QUEST+ Bayesian adaptive estimation characterized the detection threshold (Th75) and psychometric slope of all 26 Latin letters. A 5-parameter Monte Carlo optimization (50,000 simulations) selected the optimal 10-letter subset.
- **Phase II:** Structural Similarity Index (SSIM) analysis at ~68 ppi confirmed letter exclusions and calibrated individual size-correction factors.
- **Phase III (n = 110):** Independent clinical validation against Classic Sloan.

Full methodology and results are described in the associated publication (see Citation below).

---

## Citation

If you use this font in research or clinical tools, please cite:

> Costa JCL, Nascimento RBM, Martins EMA, Ricarte AJ, Mangueira PKCA, Bezerra HL.  
> **The L.U.N.A. Set: A Psychometrically Equalized Optotype Alphabet for Visual Acuity Assessment — Derivation and Clinical Validation.**  
> *European Journal of Ophthalmology*, 2026. *(in press)*

---

## License

The glyph outlines are derived from the **Sloan.otf** typeface.  
This font is released for free academic and clinical use.  
Commercial redistribution requires attribution.

---

## Related

- **OptoLab / EyeLab platform:** [github.com/eyecharts/EyeLab](https://github.com/eyecharts/EyeLab) — QUEST+ implementation and Sloan.otf source
- **Prior publication:** Costa JC, Amorim DM, Lins PR. Clinical validation of a cross-platform digital visual acuity measurement system. *Eur J Ophthalmol* 2025;35:2004–12. https://doi.org/10.1177/11206721251336001
