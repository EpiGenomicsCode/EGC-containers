# Aligner Toolkit Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with most common NGS-aligners installed via [Bioconda](https://bioconda.github.io/).
Current included algorithms:
[bowtie2](https://github.com/BenLangmead/bowtie2)
[bwa](https://github.com/lh3/bwa)
[minimap2](https://github.com/lh3/minimap2)
[star](https://github.com/alexdobin/STAR)
[samtools](https://www.htslib.org/)

The container includes all command-line tools in the system `PATH`.

---

## Notes
- **Pinned version:**
  - bowtie2 v2.5.4
  - bwa v0.7.18
  - minimap2 v2.28
  - star v2.7.11b
  - samtools v1.21
- **Location:** Binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build aligner_toolkit.sif aligner_toolkit.def
```

### Run command

Example command to run bowtie2
```
singularity exec aligner_toolkit.sif bowtie2
```

Example command to run bwa
```
singularity exec aligner_toolkit.sif bwa
```

Example command to run minimap2
```
singularity exec aligner_toolkit.sif minimap2
```

Example command to run STAR
```
singularity exec aligner_toolkit.sif STAR
```

Example command to run samtools
```
singularity exec aligner_toolkit.sif samtools
```

Example command to run bowtie2 piping directly into samtools (call container multiple times)
```
singularity exec aligner_toolkit.sif \
    bowtie2 -x ref/genome_index -1 reads_1.fq -2 reads_2.fq \
    | singularity exec aligner_toolkit.sif samtools view -bS - \
    | singularity exec aligner_toolkit.sif samtools sort -o aligned.sorted.bam
```

Example command to run bowtie2 piping directly into samtools (call container once)
```
singularity shell aligner_toolkit.sif
bowtie2 -x ref/genome_index -1 reads_1.fq -2 reads_2.fq \
  | samtools view -bS - \
  | samtools sort -o aligned.sorted.bam
samtools index aligned.sorted.bam
exit
```
