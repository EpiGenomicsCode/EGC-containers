# deepTools 3.5.6 Singularity Container

This repository contains a Singularity/Apptainer definition file for building a portable container with [deepTools](https://deeptools.readthedocs.io/en/latest/) **v3.5.6**, installed via [Bioconda](https://bioconda.github.io/).  
The container includes all deepTools command-line tools (e.g., `bamCoverage`, `bamCompare`, `computeMatrix`, `plotHeatmap`, `plotProfile`) in the system `PATH`.

---

## Notes
- **Pinned version:** deepTools v3.5.6
- **Location:** deepTools binaries linked into `/usr/local/bin`

---

## Building the Container

### Prerequisites
- Singularity CE ≥ 3.6 **or** Apptainer ≥ 1.1
- Internet access for downloading Miniconda and Bioconda packages

### Build Command
```
singularity build deeptools_3.5.6.sif deeptools_3.5.6.def
```

### Run command

Example command to run deepTools
```
singularity exec deepTools
```

Example command to generate bigWig files for midpoint-based assays (e.g., ATAC-seq, Histone ChIP, MNase-seq)
```
singularity exec deepTools_3.5.6.sif bamCoverage -b input.bam  -o output.bw --outFileFormat 'bigwig' --binSize 1 --minMappingQuality '1' --centerReads --normalizeUsing CPM > logs/file.logs
```

Example command to generate stranded bigWig files for high-resolution (5' Read 1) assays (e.g., ChIP-exo, PRO-cap)
```
singularity exec deepTools_3.5.6.sif bamCoverage -b input.bam -o output_forward.bw --outFileFormat 'bigwig' --binSize 1 --minMappingQuality '1' --samFlagInclude 64 --samFlagExclude 16 --Offset 1 --smoothLength 10 --normalizeUsing CPM > logs/file.logs
singularity exec deepTools_3.5.6.sif bamCoverage -b input.bam -o output_reverse.bw --outFileFormat 'bigwig' --binSize 1 --minMappingQuality '1' --samFlagInclude 80 --Offset 1 --smoothLength 10 --normalizeUsing CPM > logs/file.logs
```
