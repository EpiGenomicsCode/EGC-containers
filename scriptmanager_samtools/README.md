## Singularity container `scriptmanager_samtools`

This repository contains a Singularity/Apptainer definition file for building a portable container with samtools and scriptmanager installed from source on a minimal os (`bitnami/minideb:latest`).

Current included algorithms:
- [samtools=1.21](https://www.htslib.org/)
- [scriptmanager=0.15](https://github.com/CEGRcode/scriptmanager) (default-jre)

---
Future changes:
- Reduce storage footprint: once binaries are compiled, could remove samtools and htslib source
---

We built a Singularity container with both ScriptManager (and Java) and [samtools](https://www.htslib.org/) for running the HTCondor jobs (plus unzip for unpackaging YEP downloads). Read more about using containers on OSG [here](https://portal.osg-htc.org/documentation/htc_workloads/using_software/containers/).

### Build Command

```
# Built on https://cloud.sylabs.io/ cause I was running into memory limits building on ROAR
# try the following line if you want to command line build but be warned that it hasn't been confirmed to work
#singularity build scriptmanager_samtools.sif scriptmanager_samtools.def
```

### Run command

Example command to run samtools
```
singularity exec scriptmanager_samtools.sif samtools index INPUT.bam
```

Example command to run scriptmanager
```
singularity exec scriptmanager_samtools.sif scriptmanager coordinate-manipulation expand-bed INPUT.bed -c 1000 -o OUTPUT_1000bp.bed
```
