# PADLOC-DB release v2.0.0

### About

PADLOC-DB is a curated database of profile Hidden Markov Models (HMMs) and Covariance Models (CMs) for prokaryotic antiviral defence system proteins and ncRNAs, and models describing the genetic architecture of these systems. These files are used by [PADLOC](https://github.com/leightonpayne/padloc) to locate antiviral defence systems in prokaryotic genomes. The HMMs and CMs can otherwise be used independently with HMMER, Infernal and related software.

The latest version of this database is installed when running `padloc --db-update`, specifc versions can be installed using `padloc --db-install <version>`.

### What's new

This release of PADLOC-DB adds many new systems from [Millman et al., 2022](https://doi.org/10/gsdp9b) (HMMs from [DefenseFinder](https://doi.org/10/kx68)), the systems from [Vassalo et al., 2022](https://doi.org/10/gqwkdp), the Juk system from [Li et al., 2022](https://doi.org/10/kwzv), the Ddm system from [Jaskólska et al., 2022](https://doi.org/10/hrkn), the HNH (PcaRCII) system from [Birkholz et al., 2022](https://doi.org/10/kw2b), the MADS system from [Maestri et al., 2023](https://doi.org/10/ktmx), several new Hma-embedded candidate systems (HECs) (Payne, unpublished), and hundreds of other phage defence candidates (PDCs) (Payne, unpublished).

The covariance models used by the PADLOC web server for retron ncRNA detection have also been included. Instructions for using these CMs with PADLOC can be found in the [PADLOC repo](https://github.com/padlocbio/padloc).

Due to re-formating of the system models and metadata tables, this database is only compatible with PADLOC version 2.X.X, and not PADLOC version 1.X.X. Make sure you are using the updated version of PADLOC with this database.

### What's included

```
padloc-db
├── hmm/                        <- Defence system protein HMMs.
├── cm/                         <- Defence system RNA CMs.
├── sys/                        <- Defence system models.
├── hmm_meta.txt                <- Metadata for HMMs.
├── cm_meta.txt                 <- Metadata for CMs.
├── sys_meta.txt                <- Metadata for system models.
├── system_info.md              <- Formatted table of system/reference information.
├── README.md                   <- Information regarding metadata fields.
├── RELEASE.md                  <- This file.
└── LICENSE                     <- Copyright information.
```

### Release record

| Release | Date       | HMMs | CMs | Classifications |
| ------- | ---------- | ---- | --- | --------------- |
| v2.0.0  | 03/08/2023 | 5027 | 21  | 385             |
| v1.4.0  | 23/04/2022 | 3824 | 0   | 210             |
| v1.3.0  | 14/02/2022 | 2974 | 0   | 181             |
| v1.2.0  | 11/11/2021 | 2360 | 0   | 126             |
| v1.1.0  | 28/09/2021 | 2223 | 0   | 97              |
| v1.0.0  | 05/08/2021 | 915  | 0   | 36              |
