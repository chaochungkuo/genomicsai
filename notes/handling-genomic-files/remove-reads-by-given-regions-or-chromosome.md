# Remove reads by given regions or chromosome

In some cases, we would like to filter the BAM files by removing certain reads, such as:

* **Filter ChIP-Seq or ATAC-Seq reads by the defined blacked list.** Filtering reads from ChIP-seq or ATAC-seq data using a blacklist is important to remove reads that are likely to be derived from non-specific binding or technical artifacts. These non-specific reads can arise from repetitive genomic regions, such as satellite DNA, centromeres, telomeres, and transposable elements, as well as from PCR or sequencing adapters. These reads can lead to false-positive signals and reduce the quality of downstream analysis results. By filtering out these reads using a blacklist, we can improve the accuracy and specificity of peak calling and other downstream analyses.
* **Filter reads by removing mitochondrial chromosome.** We need to remove reads mapping to mitochondrial chromosome in DNA sequencing data such as ChIP-seq or ATAC-seq because mitochondrial DNA (mtDNA) is abundant in cells and can cause contamination in the sequencing data. The mitochondrial genome is circular and can form concatemers, which makes it difficult to properly map reads to the correct location. In addition, the level of mtDNA can vary among different cell types or experimental conditions, which can introduce biases in downstream analysis if not properly accounted for. Therefore, removing reads mapping to mitochondrial genome can improve the quality and accuracy of downstream analysis.

The scripts for the above tasks can be done by:

* Filtering BAM files by given regions (blacked list).
  * [bedtools intersect](https://bedtools.readthedocs.io/en/latest/content/tools/intersect.html) with -abam and -v
* Filtering BAM files by given chromatin (chrM).
  * The principle is the same: Get the list of all chromatins; Get non-MT list; Extract the reads on those non-MT chromatin; Save as BAM.
  * Bedtools can also work if you define a BED file for MT regions (just one line).

```bash
for i in *.bam; do 
non_chrM_list=$(samtools view -H $i | grep chr | cut -f2 | sed 's/SN://g' | grep -v chrM) 
samtools view -b $i $non_chrM_list -o [outfilename.bam]
done
```
