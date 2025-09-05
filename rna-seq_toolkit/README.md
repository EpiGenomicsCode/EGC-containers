# RNA-seq Toolkit Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with RNA-seq processing algorithms installed via [Bioconda](https://bioconda.github.io/).
Current included algorithms:
[star](https://github.com/alexdobin/STAR)
[salmon](https://github.com/COMBINE-lab/salmon)
[kallisto](https://github.com/pachterlab/kallisto)
[samtools](https://www.htslib.org/)
[htseq](https://htseq.readthedocs.io/en/latest/)
[subread](https://subread.sourceforge.net/)

The container includes all command-line tools in the system `PATH`.

---

## Notes
- **Pinned version:**
  - star v2.7.11b
  - salmon v1.10.3
  - kallisto v0.51.1
  - samtools v1.21
  - htseq v2.0.9
  - subread v2.1.1
- **Location:** Binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build rna-seq_toolkit.sif rna-seq_toolkit.def
```

### Run command

Example command to run STAR
```
singularity exec rna-seq_toolkit.sif STAR
```

Example command to run STAR alignment with BAM indexing
```
singularity exec rna-seq_toolkit.sif STAR --runThreadN 8 --genomeDir star_index \
     --readFilesIn reads_1.fq reads_2.fq \
     --outSAMtype BAM SortedByCoordinate \
     --outFileNamePrefix sample1_

singularity exec rna-seq_toolkit.sif samtools index sample1_Aligned.sortedByCoord.out.bam
```

Example command to run Gene counting
```
singularity exec rna-seq_toolkit.sif htseq-count -f bam -r pos -s no -t exon -i gene_id sample1_Aligned.sortedByCoord.out.bam annotation.gtf > counts_htseq.txt

singularity exec rna-seq_toolkit.sif featureCounts -T 8 -t exon -g gene_id -a annotation.gtf -o counts_featureCounts.txt sample1_Aligned.sortedByCoord.out.bam
```

Example command to run Alignment-free quantification
```
singularity exec rna-seq_toolkit.sif salmon quant -i transcript_index -l A \
              -1 reads_1.fq -2 reads_2.fq \
              -p 8 -o salmon_quant

singularity exec rna-seq_toolkit.sif kallisto quant -i transcript_index.idx \
               -o kallisto_quant -b 100 \
               reads_1.fq reads_2.fq
```
