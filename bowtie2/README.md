# Bowtie 2.5.4 Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with [Bowtie2](https://github.com/BenLangmead/bowtie2) **v2.5.4**, installed via [Bioconda](https://bioconda.github.io/).  
The container includes all bowtie2 command-line tools (e.g., `bowtie2`, `bowtie2-inspect`, `bowtie2-build`) in the system `PATH`.

---

## Notes
- **Pinned version:** bowtie2 v2.5.4
- **Location:** bowtie2 binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build bowtie2_2.5.4.sif bowtie2_2.5.4.def
```

### Run command

Example command to run bowtie2
```
singularity exec bowtie2
```

Example command to run bowtie2-build (for indexes)
```
singularity exec bowtie2-build
```
