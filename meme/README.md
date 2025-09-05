# MEME Suite 5.5.8 Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with the [MEME Suite](http://meme-suite.org/) **v5.5.8**, installed via [Bioconda](https://bioconda.github.io/).  
The container includes all MEME command-line tools (e.g., `meme`, `meme-chip`, `fimo`) in the system `PATH`.

---

## Notes
- **Pinned version:** MEME Suite v5.5.8
- **Location:** MEME binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build meme-suite_5.5.8.sif meme-suite_5.5.8.def
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
