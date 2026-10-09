# Task 3 for RStudio / Quarto

Open `task3.qmd` in RStudio and click **Render**. Keep `references.bib`,
`task3_reanalyse.R` and the `data` folder beside the QMD. Rendering uses R,
Quarto and knitr; no Python, VCF parser package or internet access is required.
If necessary, run `install.packages("knitr")` once in RStudio.

## Add the chapter to your existing book

Copy the supplied files into the existing project. In the existing
`_quarto.yml`, add `task3.qmd` directly after `Task2.qmd` under `book: chapters:`.
Keep the existing introduction, summary, Task 1 and Task 2 entries unchanged.
For example, the relevant part becomes:

```yaml
book:
  chapters:
    - index.qmd
    - intro.qmd
    - summary.qmd
    - Task1.qmd
    - Task2.qmd
    - task3.qmd
    - references.qmd
```

Use your actual chapter filenames. Do not replace the whole existing
`_quarto.yml` with this snippet.

Merge the new BibTeX entries into your existing bibliography, checking for
matching keys. Alternatively, rename the supplied file to `task3-references.bib`
and include both bibliographies in the project configuration:

```yaml
bibliography:
  - your-existing-references.bib
  - task3-references.bib
```

If references are configured globally, remove the `bibliography:` line from
the chapter YAML. If your book already has a central references chapter,
remove the final `## References` section and its `#refs` div from `task3.qmd`.
The in-text citations remain. Do not replace an existing bibliography without
merging it: Tasks 1 and 2 may already cite other entries.

## What is preserved and corrected

The objective, approach/findings/discussion/conclusion structure, OAS2, both
guide names, seven sample IDs, the original SNP and most of the original
argument are preserved. Necessary changes are:

- The variant changes the PAM from AGG to AGA. Protospacer mismatches stay at four.
- Three carriers retain one reference haplotype; only NA19462 has two ALT copies.
- Guide availability is reported as not assessed. OAS2 is on chromosome 12,
  outside the original chromosome 1/2 analysis.
- Conclusions refer only to the reference-predicted sites actually assessed.
- CRISPRi is discussed as transcriptional regulation, without claims of DNA cutting.
- The original plot and placeholder references are removed.
- Tables, genotype interpretation and sequence comparisons are generated in R.

The original report contained no actual references. The bibliography therefore
contains verified sources supporting the revised statements, rather than a
claim about which publications the original author read. It includes the QUT
Lecture 6 and Task 2/3 slides supplied with this conversation. Their dates and
individual authors were not given, so these fields have not been invented.

## Evidence and remaining work before submission

`data/Task3_variant_hits.csv` is an unchanged copy of the supplied carrier
export. Its original `Risk` column is intentionally ignored. The site snapshot
contains the exact sequence pair and all seven genotypes displayed in the
original HTML notebook. It does not supply the full CRISPOR table or replace
the original VCFs. The counts for the original chr1/chr2 scan are reported
from that original output; they are not an independently repeated raw scan.

To repeat that scan, supply the original CRISPOR table and VCFs, verify their
assembly and coordinate convention, and run the disabled reproduction chunk
in RStudio. The supplementary R function checks strand orientation and REF
agreement and flags complex variants instead of inventing scores. It returns
all per-haplotype overlaps and chromosome coverage. The default assembly
argument in the function is FALSE; set it to TRUE only after checking the
source metadata. The QMD example assumes 1-based-inclusive coordinates only
after that convention has been confirmed.

For the outstanding on-target question, obtain the exact GRCh38 coordinates,
strand and target-plus-PAM sequences for 200forw and 248forw from Task 2,
together with chromosome 12 variant data for the same seven individuals.
Reconstruct both target haplotypes and check the protospacer match and PAM.
Absence from a variant-only VCF is evidence only within its reliable coverage;
missing calls must not be interpreted as reference calls.

A personalised genome or variant-aware search is needed to discover new
variant-created off-targets. Adding a limitations paragraph alone does not
perform this search or resolve target availability, and full marks cannot
be guaranteed with the current missing inputs.

## Verification performed

The snapshot was checked against the displayed notebook result and the
carrier CSV. Both sequence comparisons were independently recalculated:
4 protospacer mismatches before and after, AGG to AGA, three heterozygotes,
one ALT homozygote and three reference homozygotes. BibTeX citation keys
and formatting were checked using Pandoc's citation processor.

R and Quarto are not installed in the authoring environment. The R chunks
and the optional raw-data audit have therefore not been executed here, and
an actual Quarto render must be checked in RStudio. Raw-data results cannot
be verified without the original input files.
