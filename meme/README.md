# MEME Suite 5.5.8 Singularity Container

This repository contains two Singularity/Apptainer definition file for building a portable container with the [MEME Suite](http://meme-suite.org/) **v5.5.8**, installed either via [Bioconda](https://bioconda.github.io/) or building directly from source.

The container includes all MEME command-line tools (e.g., `meme`, `meme-chip`, `fimo`) in the system `PATH`.

---

## Notes
- **Pinned version:** MEME Suite v5.5.8
- **Location:** MEME binaries linked into `/usr/local/bin`
- **Source:** Building with source is required for multi-core MEME support (MPI)

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build meme-suite_5.5.8.sif meme-suite_5.5.8.def
```

##### If MPI support is needed
```
singularity build meme-suite_5.5.8_MPI.sif meme-suite_5.5.8_MPI.def
```

### Run command

Example command to run MEME
```
singularity exec meme-suite_5.5.8.sif meme
```

Example command to run MEME-ChIP
```
singularity exec meme-suite_5.5.8.sif meme-chip
```

Example command to run FIMO
```
singularity exec meme-suite_5.5.8.sif fimo
```

Example command to run MEME with multi-core (e.g., 2) support
```
singularity exec meme-suite_5.5.8_MPI.sif meme -p 2 --oversubscribe
```
 - Note that ``--oversubscribe`` is a Apptainer container command (**NOT** part of the MEME-suite) to force the usage of multiple cores
