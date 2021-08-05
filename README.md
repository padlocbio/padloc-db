<a href="https://github.com/padlocbio/padloc-db/LICENSE" alt="License"><img src="https://img.shields.io/github/license/padlocbio/padloc-db" /></a> <a href="https://github.com/leightonpayne/padloc-db/" alt="Last Update"><img src="https://img.shields.io/github/last-commit/padlocbio/padloc-db?label=last%20update" /></a> <a href="https://github.com/padlocbio/padloc-db/releases" alt="Release"><img src="https://img.shields.io/github/v/release/padlocbio/padloc-db" /></a> 
# PADLOC-DB

## About

This repo contains the latest version of the HMMs and system models used by [PADLOC](https://github.com/padlocbio/padloc). This database is downloaded and compiled automatically when [PADLOC](https://github.com/padlocbio/padloc) is installed via conda. Otherwise, it can be installed by running `padloc --db-update`.

The following document describes each field of `hmm_meta.txt` and `sys_meta.txt`, and how you can use your own HMMs and system models with [PADLOC](https://github.com/padlocbio/padloc).

## Citation

Manuscript in preparation.

## System models

System models are written using YAML syntax:

```yaml
---
maximum_separation: 4       <- Number of unrelated genes allowed to separate each component.
minimum_core: 4             <- Number of core genes that need to be present.
minimum_total: 5            <- Number of total genes that need to be present.
core_genes:                 <- Genes that are generally considered essential.
  - GenA
  - GenB
  - GenC
  - GenD
optional_genes:             <- Genes that are not always present.
  - GenX
  - GenY
prohibited_genes:           <- Genes that cannot be present.
  - GenZ
...
```

## HMM metadata (hmm_meta.txt)

#### Compulsory fields

These fields must be filled out for use with [PADLOC](https://github.com/leightonpayne/padloc).

| Field                       | Example          | Description                                                  |
| --------------------------- | ---------------- | ------------------------------------------------------------ |
| `hmm.accession`             | PDLC00001        | A unique identifier for each padlocDB HMM.                   |
| `hmm.name`                  | GajA_6           | Another unique identifier for each HMM. If the HMM is from an external database, the original ID from that database is preferred. |
| `hmm.description`           | Predicted ATPase | A one line description of the HMM e.g. describing protein function or domains. |
| `protein.name`              | PemK\|MazF       | The name of the protein that the HMM represents. Multiple protein names are separated by '\|'. Capitalisation of the first letter is preferred. These are the names that are referenced in the system models. |
| `e.value.threshold`         | 1e-05            | The minimum E-value allowed when reporting hits.             |
| `hmm.coverage.threshold`    | 0.3              | The proportion of the HMM that must contribute to the HMM/target alignment when reporting hits. |
| `target.coverage.threshold` | 0.3              | The proportion of the target that must contribute to the HMM/target alignment when reporting hits. |
| `comment`                   | NA               | Other information that is relevant. This may include comments from the original database where applicable. |

####  Optional fields

These fields are for reference only, and are not strictly required by [PADLOC](https://github.com/leightonpayne/padloc).

| Field            | Example                          | Description                                                  |
| ---------------- | -------------------------------- | ------------------------------------------------------------ |
| `secondary.name` | CRISPR-accessory                 | A secondary identifier that can be referred to in the system definition for groups of proteins rather than individual protein names |
| `system`         | DISARM, RESTRICTION MODIFICATION | The category of defence system to which the HMM belongs. Multiple system names are separated by ', '. The full system name is used where reasonable. |
| `author`         | Payne LJ, Jackson SA             | Author(s) of the entry. If the HMM is from an external database,     crediting the original author is preferred. If the HMM is from a study where an author was not explicity credited, authorship is attributed to the first author of the study. Multiple authors are separated by ', '. |
| `hmm.nseq`       | 49                               | The number of sequences that contribute to the HMM.          |
| `hmm.length`     | 120                              | The length of the the HMM.                                   |
| `literature.ref` | 10/f2wkj3                        | The DOI for the literature that implies that the members of the HMM belong to the protein/defence system. Multiple references are separated by ', '. |
| `database.ref`   | PFAM; PF06527                    | Reference to the original accession of the alignment/HMM if it was taken from an external database, e.g. PFAM, COG, etc. Includes the name of the database name and the identifier separated by '; '. |

## System metadata (sys_meta.txt)

#### Compulsory fields

| Field       | Example         | Description                                                  |
| ----------- | --------------- | ------------------------------------------------------------ |
| `yaml.name` | druantia_type_I | The exact name of the yaml file that corresponds with the system type (without the `.yaml` extension) |
| `search`    | T               | Set to `TRUE` or `FALSE` (or `T` / `F`) to determine whether the system is searched or not. |
| `comment`   | NA              | Other information that is relevant.                          |

#### Optional fields

| Field         | Example  | Description                |
| ------------- | -------- | -------------------------- |
| `system.name` | Druantia | The name of the system     |
| `type`        | type I   | The subtype of the system. |

## Adding to the database

Additional HMMs and system models can be added directly to your copy of this database, or a separate database can be set up in the same way as this one.

Additional HMMs can be added to the `hmm/` directory, `hmm_meta.txt` also needs to be updated to include metadata for the new HMMs. When using with [PADLOC](https://github.com/leightonpayne/padloc), these HMMs need to be concatenated into a single file in the `hmm/` directory called `padlocdb.hmm`.

Additional system models can be added to the `sys/` directory, `sys_meta.txt` should also be updated to include metadata for the new models.

