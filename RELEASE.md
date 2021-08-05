# PADLOC-DB release v1.0.0

### About

PADLOC-DB is a curated database of HMMs for prokaryotic antiviral defence system proteins, and models describing the genetic architecture of these systems. These files are used by [PADLOC](https://github.com/leightonpayne/padloc) to locate antiviral defence systems in prokaryotic genomes. They can otherwise be used independently with HMMER and related software.

The latest version of this database is installed when running `padloc --db-update`, specifc versions can be installed using `padloc --db-install <version>`.

### What's new

This is the first release of PADLOC-DB. It contains HMMs and system models for CBASS and Doron/deity defence systems (i.e. Druantia, Gabija, Hachiman, Kiwa, Lamassu, Septu, Shedu, Thoeris, Wadjet and Zorya). It also contains HMMs and models for several new types of Doron defence systems we've discovered (manuscript in preparation).

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
| 1.0.0   | 05/08/2021 | 915  | 36              |

