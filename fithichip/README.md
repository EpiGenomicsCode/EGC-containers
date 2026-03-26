# FitHiChIP (v11.0) Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with [FitHiChIP](https://ay-lab.github.io/FitHiChIP/html/index.html) **v 11.0**.

The dependency collection is large and spans several languages and libraries so the install was kind of a pain, even when using conda. Luckily, this container **should** make things easier (I'm so very sorry if it doesn't).

The container includes all dependency command-line tools (e.g., `HiC-Pro`, `bowtie2`, `samtools`, `bedtools`, `macs2`, the number of python/R packages, etc.) in the system `PATH` if you would like to try to double dip for the other genomics tools (can't guarantee it will work as you expect). Everything was hard versioned as much as possible for future-proofing reasons.

Related links:
- FitHiChIP docs: https://ay-lab.github.io/FitHiChIP/html/index.html
- FitHiChIP Github: https://github.com/ay-lab/FitHiChIP
- HiC-Pro docs: https://nservant.github.io/HiC-Pro/
- HiC-Pro Github: https://github.com/nservant/HiC-Pro

---

## Notes

- **Pinned version:** bedtools v2.31.1
- **Location:** bedtools binaries linked into `/usr/local/bin`
- FitHiChIP performance notes on the tool itself:
    - the tool itself is a massive memory hog for the first few minutes (Olivia's data reached +50GB on hg38) and then drops down to near-zero for the rest of the hours of runtime
    - allow for a long run time so run it in the background or detachable session
    - at some point, we might consider actually making some PRs to fix some easy performance improvements that would have a massive impact on runtime

---

## Building the Container

### Prerequisites

- Container was tested on Apptainer version `1.4.5-3.el8`
- Internet access for downloading Miniconda and Bioconda packages (speeds up build and is more robust to updates)


### Build Command

- Size of built `.sif` is ~1.4G
- Allow for ~20min minutes to build on [Sylabs](https://sylabs.io/singularity/)

```
singularity build fithichip.sif fithichip.def
```

### Run command

The absolute path input is important because FitHiChIP needs to execute from within its directory in the image and it is unclear what the path from the image directory to the local system `.config` file would look like. Absolute paths are usually safer.

Example command to run:

```
singularity run fithichip.sif /absolute/path/to/config.txt
```

Read more about the config file on the FitHiChIP documentation: https://ay-lab.github.io/FitHiChIP/html/usage/configuration.html

### Test command

This will also report version info and tool paths/locations within the image:

```
singularity test fithichip.sif
```

### Help command

The help will also report key details like tool locations and example commands:

```
singularity run-help fithichip.sif
```
