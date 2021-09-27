# PADLOC-DB release v1.1.0

### About

PADLOC-DB is a curated database of HMMs for prokaryotic antiviral defence system proteins, and models describing the genetic architecture of these systems. These files are used by [PADLOC](https://github.com/leightonpayne/padloc) to locate antiviral defence systems in prokaryotic genomes. They can otherwise be used independently with HMMER and related software.

The latest version of this database is installed when running `padloc --db-update`, specifc versions can be installed using `padloc --db-install <version>`.

### What's new

This is the second release of PADLOC-DB. It greatly expands upon the previous release through the addition of HMMs and system models for 27 CRISPR-Cas subtypes and 26 diverse types of defence systems from [Gao et al., 2020](https://doi.org/10/gpsx). One HMM was deprecated (see [hmm/deprecated/notes.txt](https://github.com/padlocbio/padloc-db/tree/master/hmm/deprecated/notes.txt)).

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
| v1.1.0  | 27/09/2021 | 2223 | 97              |
| v1.0.0  | 05/08/2021 | 915  | 36              |

