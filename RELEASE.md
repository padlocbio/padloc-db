# PADLOC-DB release v1.3.0

### About

PADLOC-DB is a curated database of HMMs for prokaryotic antiviral defence system proteins, and models describing the genetic architecture of these systems. These files are used by [PADLOC](https://github.com/leightonpayne/padloc) to locate antiviral defence systems in prokaryotic genomes. They can otherwise be used independently with HMMER and related software.

The latest version of this database is installed when running `padloc --db-update`, specifc versions can be installed using `padloc --db-install <version>`.

### What's new

This release of PADLOC-DB adds BREX, DISARM, pArgonaute, Phosphorothioation systems (DND/PBE/SSP), Pycsar, Viperin, and several other types of defence systems (https://doi.org/10/g29b).

### What's included


```
padloc-db
├── hmm/                        <- Defence protein HMMs.
├── sys/                        <- Defence system models.
├── hmm_meta.txt                <- Metadata for HMMs.
├── sys_meta.txt                <- Metadata for system models.
├── README.md                   <- Information regarding metadata fields.
├── RELEASE.md                  <- This file.
└── LICENSE                     <- Copyright information.
```

### Release record

| Release | Date       | HMMs | Classifications |
| ------- | ---------- | ---- | --------------- |
| v1.3.0  | 13/02/2022 | 2974 | 181             |
| v1.2.0  | 11/11/2021 | 2360 | 126             |
| v1.1.0  | 28/09/2021 | 2223 | 97              |
| v1.0.0  | 05/08/2021 | 915  | 36              |

