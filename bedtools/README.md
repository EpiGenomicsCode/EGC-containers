# bedtools 2.31.1 Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with [bedtools](https://bedtools.readthedocs.io/en/latest/) **v2.31.1**, installed via [Bioconda](https://bioconda.github.io/).  
The container includes all bowtie2 command-line tools (e.g., `bedtools intersect`, `bedtools closest`, `bedtools-genomecov`) in the system `PATH`.

---

## Notes
- **Pinned version:** bedtools v2.31.1
- **Location:** bedtools binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build bedtools_2.31.1.sif bedtools_2.31.1.def
```

### Run command

Example command to run bedtools
```
singularity exec bedtools
```
