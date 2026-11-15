# Pedigree Collapse — Why You Do Not Have 2ⁿ Ancestors

An interactive D3.js lab refuting the "2ⁿ different ancestors" fallacy for
endogamous populations, with Jewish population history (founder bottlenecks,
endogamy, consanguinity) as the worked example.

## Run

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

No build step, no data leaves the browser. Everything is in `index.html`
(D3.js v7 + KaTeX via CDN).

## The model

- **Ancestral slots** (Ahnentafel places): \(S_g = 2^g\) — this is all the viral video counts.
- **Distinct ancestors** — occupancy ("birthday problem") expectation, drawing
  slots with replacement from the effective breeding pool \(N_e(g)\):
  \(\mathbb{E}[A_g] = N_e(g)\left[1-(1-1/N_e(g))^{S_g}\right] \approx N_e(g)(1-e^{-S_g/N_e(g)})\)
- **Pedigree collapse**: \(C_g = 1 - A_g/S_g\); **multiplicity**: \(m_g = S_g/A_g\)
  (average number of Ahnentafel slots one distinct ancestor occupies).
- **Population trajectory** \(N_e(g)\): log-linear through present size →
  founder bottleneck \(N_f\) at generation \(g_b\) → older ancestral size.
  All sizes are *effective* size \(N_e\), not census \(N_c\) (\(N_e/N_c \approx 0.1\!-\!0.3\)).
- **Endogamy** shrinks the mating pool: \(N_e^{mate} = N_e[(1-e) + e\,s]\),
  with endogamy rate \(e\) and subgroup share \(s\).
- **Inbreeding**: Wright's \(F\) accumulated by drift,
  \(F_g = 1-\prod_k (1-\tfrac{1}{2N_e^{mate}(k)})\), blended with a consanguinity
  term from the share \(\alpha\) of close-kin unions. Benchmarks: offspring of
  first cousins \(F=1/16\), second cousins \(F=1/64\) (Wright's path method).
- **Saturation**: collapse takes over at \(g^* = \log_2 N_e\); beyond it, deeper
  generations add *paths* to existing ancestors, not new ancestors (cf. the
  identical ancestors point, Rohde–Olson–Chang 2004).

## What's interactive

- 6 scenario presets (large outbred control → Ashkenazi bottleneck, Sephardic
  post-1492, isolated shtetl, small isolated community) plus a dashed
  comparison overlay.
- Sliders for \(N_e\), founder size \(N_f\), bottleneck timing \(g_b\), older
  \(N_e\), endogamy \(e\), subgroup share \(s\), consanguineous unions \(\alpha\),
  generation time, and pedigree depth \(G\).
- Charts: distinct vs. slots (log),
  collapse & multiplicity, \(N_e(g)\) trajectory, cumulative \(F_g\), and a
  stochastic 7-generation pedigree where colour = one real person, so
  duplicated ancestors are visible. Full generation-by-generation table.

## Caveats

Random mating within the (shrunken) pool, discrete generations, no geography
or reproductive skew — outputs are orders of magnitude and mechanisms, not a
personal family tree. Genealogical ancestors ≠ genetic ancestors: beyond
~7–10 generations many true ancestors contribute no DNA segments to you.

## Main papers

Why 2^g fails — MRCA & identical ancestors point:
- Chang, J.T. (1999). *Adv. Appl. Prob.* 31(4):1002–1026. [doi:10.1017/S0001867800009587](https://doi.org/10.1017/S0001867800009587) — MRCA ~ log₂N, IAP ≈ 1.77·log₂N.
- Rohde, Olson & Chang (2004). *Nature* 431(7008):562–566. [doi:10.1038/nature02842](https://doi.org/10.1038/nature02842)

Coefficients — F, kinship, coalescent, genetic ancestors:
- Wright, S. (1922). *Am. Nat.* 56(645):330–338. [doi:10.1086/279872](https://doi.org/10.1086/279872)
- Kingman, J.F.C. (1982). *Stoch. Proc. Appl.* 13(3):235–248. [doi:10.1016/0304-4149(82)90011-4](https://doi.org/10.1016/0304-4149(82)90011-4)
- Donnelly, K.P. (1983). *Theor. Popul. Biol.* 23(1):34–63. [doi:10.1016/0040-5809(83)90004-7](https://doi.org/10.1016/0040-5809(83)90004-7)

Jewish demographic history — bottlenecks, endogamy, IBD:
- Carmi, S. et al. (2014). *Nat. Commun.* 5:4835. [doi:10.1038/ncomms5835](https://doi.org/10.1038/ncomms5835) — AJ bottleneck ≈350 (250–420), 25–32 gen ago.
- Palamara, P.F. et al. (2012). *Am. J. Hum. Genet.* 91(5):809–822. [doi:10.1016/j.ajhg.2012.08.030](https://doi.org/10.1016/j.ajhg.2012.08.030) — Nₑ(g) from IBD lengths.
- Waldman, S. et al. (2022). *Cell* 185(25):4703–4716.e16. [doi:10.1016/j.cell.2022.11.002](https://doi.org/10.1016/j.cell.2022.11.002) — medieval Erfurt aDNA.
- Xue, J. et al. (2017). *PLoS Genet.* 13(4):e1006644. [doi:10.1371/journal.pgen.1006644](https://doi.org/10.1371/journal.pgen.1006644)
- Atzmon, G. et al. (2010). *Am. J. Hum. Genet.* 86(6):850–859. [doi:10.1016/j.ajhg.2010.04.015](https://doi.org/10.1016/j.ajhg.2010.04.015)
- Behar, D.M. et al. (2010). *Nature* 466(7303):238–242. [doi:10.1038/nature09103](https://doi.org/10.1038/nature09103)
- Slatkin, M. (2004). *Am. J. Hum. Genet.* 75(2):282–293. [doi:10.1086/423146](https://doi.org/10.1086/423146)

Preset numbers are rounded teaching values synthesised from these — tune them.
