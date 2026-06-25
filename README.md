# purvis-dev2025-crispr-outcomes

Canonical repository for the [`CrispRVariants`](https://bioconductor.org/packages/release/bioc/html/CrispRVariants.html) amplicon-seq pipeline used in the the following manuscript. P0 mouse retinas were electroporated with conventional CRISPR plasmids; FACS-sorted genomic DNA was PCR-amplified across guide sites and sequenced to quantify indel spectra.

**Purvis IJ, Ochoa Olmos OE, Park KU, Kaufman ML, Henry CM, Schaaf C, Clise OJ, Tesdahl CD, Haas A, Brzezinski JA IV.** A robust cis-regulatory network ensures *Otx2* expression during retinal development. *Development* **153**, dev204881 (2026).  
[https://doi.org/10.1242/dev.204881](https://doi.org/10.1242/dev.204881)

---

## Paper scope

Amplicon sequencing of CRISPR-edited retinal cells, analyzed with CrispRVariants. Outcomes are reported in **Table S3**.

| Target | Guides analyzed | Notes |
|--------|-----------------|-------|
| *Otx2* coding | g1, g2 | Positive control |
| DHS2 | g1, g2 | |
| DHS15 | g2 only | g1 amplicon failed |
| Promoter / exon 1A | g2 only | g1 amplicon failed |
| Promoter / exon 1B | g1, g2 | |
| Promoter / exon 1C | g1, g2 | |

In total: **6 target regions**, **10 guide sequences** successfully analyzed (DHS15 g1 and promoter 1A g1 could not be amplified).

---

## Repository contents

This repo holds the analysis pipeline and a subset of the sequencing data from the paper.

| sampleid | prefix | treatment |
|----------|--------|-----------|
| ControlDHS2 | ControlDHS2primers | Control |
| ControlDHS15 | ControlDHS15primers | Control |
| TestDHS15 | TestDHS15primers | Test |

Primary analysis ([`analysis/01-CrispRVariants.qmd`](analysis/01-CrispRVariants.qmd)): TestDHS15 vs ControlDHS15 at the DHS15 locus (both guides; see [`analysis/comparisons.csv`](analysis/comparisons.csv)).

**Guide RNA sequences** (PAM not included):

| Target | Guide | Sequence |
|--------|-------|----------|
| DHS15 | g1 | `GCTGCCCCAGCCTTTCACAA` |
| DHS15 | g2 | `TTTTCTTTTTTATTTAACCG` |
| DHS2 | g1 | `CACCGACCCAGCTCTGGCAGATGGG` |
| DHS2 | g2 | `ATTTTGAACCCCCTACAGAT` |

**Amplicon primers**

DHS15 (437 bp): F `GGTGTGCACCTCACCCGTGTTT` · R `CACATCAAGCTGGAGGGCTGCA`  
DHS2 (638 bp): F `CCGAAGTGCCAGGAGGAAAGGC` · R `ACCAAACCACACCACACCACACC`

---

## Analysis

- Align FASTQ files with `bwa` and `samtools` (mm39)
- Quantify indels with `CrispRVariants`
- Documents: [`analysis/01-CrispRVariants.qmd`](analysis/01-CrispRVariants.qmd), [`analysis/02-CrispRVariants_autoguide.qmd`](analysis/02-CrispRVariants_autoguide.qmd)

### Outputs

- [Mutagenesis report (`01-CrispRVariants.html`)](analysis/outs/01-CrispRVariants/01-CrispRVariants.html)
- [`analysis/variant_plot.pdf`](analysis/variant_plot.pdf)

### Reproducing

```bash
cd analysis
Rscript -e "renv::restore()"
quarto render 01-CrispRVariants.qmd
```

Reference genome files (`ref/mm39.fa`, GENCODE vM37 GTF) are not included; place them in `ref/` before rerunning.

---

## References

- [CrispRVariants user guide](https://www.bioconductor.org/packages/release/bioc/vignettes/CrispRVariants/inst/doc/user_guide.html)
- [CrispRVariants GitHub](https://github.com/markrobinsonuzh/CrispRVariants)
- [CrispRVariants Bioconductor](https://bioconductor.org/packages/release/bioc/html/CrispRVariants.html)
