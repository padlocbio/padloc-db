<a href="https://github.com/padlocbio/padloc-db/LICENSE" alt="License">
	<img src="https://img.shields.io/github/license/padlocbio/padloc-db" />
</a>

<a href="https://github.com/padlocbio/padloc-db/releases" alt="Github release">
	<img src="https://img.shields.io/github/v/release/padlocbio/padloc-db?label=github%20release" />
</a>

<a href="https://github.com/padlocbio/padloc-db/commits/master" alt="GitHub commits since latest release">
	<img src="https://img.shields.io/github/commits-since/padlocbio/padloc-db/latest?sort=semver">
</a>

<a href="https://github.com/padlocbio/padloc-db/" alt="Last update">
	<img src="https://img.shields.io/github/last-commit/padlocbio/padloc-db?label=last%20update" />
</a>

<a href="https://doi.org/10/gzgh" alt="Citations">
	<img src="https://citations.njzjz.win/10.1093/nar/gkab883">
</a>

# PADLOC-DB

> [!IMPORTANT]
> [PADLOC](https://github.com/padlocbio/padloc) `>v2.0.0` is only compatible with [PADLOC-DB](https://github.com/padlocbio/padloc-db) `>v2.0.0` and vice-versa. After you update PADLOC, make sure to update your database by running: `padloc --db-update`.

## About

This repo contains the HMMs and system models used by [PADLOC](https://github.com/padlocbio/padloc). The latest version of this database can be downloaded by running `padloc --db-update`.

## Citation

If you use [PADLOC](https://github.com/padlocbio/padloc) or [PADLOC-DB](https://github.com/padlocbio/padloc-db) please cite:

> Payne, L.J., Todeschini, T.C., Wu, Y., Perry, B.J., Ronson, C.W., Fineran, P.C., Nobrega, F.L., Jackson, S.A. (2021) Identification and classification of antiviral defence systems in bacteria and archaea with PADLOC reveals new system types. *Nucleic Acids Research*, **49**, 10868-10878. doi: https://doi.org/10/gzgh

The HMMs and system models in [PADLOC-DB](https://github.com/padlocbio/padloc-db) were built and curated using the data and conclusions from many different sources, we encourage you to also give credit to these groups by reading their work and citing them where appropriate. References to relevant literature can be found in [`system_info.md`](https://github.com/padlocbio/padloc-db/blob/master/system_info.md).

## System models (`sys/*.yaml`)

System models are written using YAML syntax:

```yaml
force_strand: FALSE    # <- Specifies whether all system components should be on the same strand
maximum_separation: 4  # <- Number of unrelated genes allowed to separate each component
minimum_core: 4        # <- Number of core genes that need to be present
minimum_total: 5       # <- Number of total genes that need to be present
core_genes:            # <- Genes that are generally considered essential
  - GenA
  - GenB
  - GenC
  - GenD
secondary_genes:       # <- Genes that are not always present, but still contribute to minimum_total
  - GenX
neutral_genes:         # <- Genes that are not always present, and do not contribute to minimum_total
  - GenY
prohibited_genes:      # <- Genes that cannot be present
  - GenZ
```

## HMM metadata (`hmm_meta.txt`)

| Field                       | Example                | Description |
| --------------------------- | ---------------------- | ----------- |
| `hmm.accession`             | `PDLC00001`            | A unique identifier for each PADLOC-DB HMM. This should be consistent with the filename and `ACC` field of the HMM. |
| `hmm.name`                  | `GajA_6`               | Another unique identifier for each HMM. If the HMM is from an external database, the original ID from that database is preferred. This should be consistent with the `NAME` field of the HMM. |
| `hmm.description`           | `Predicted ATPase`     | A one line description of the HMM e.g. describing protein function or domains. This should be consistent with the `DESC` field of the HMM. |
| `protein.name`              | `PemK\|MazF`           | The name of the protein that the HMM represents. Multiple protein names are separated by a pipe (`\|`). Capitalisation of the first letter is preferred. These are the names that are referenced in the system models. |
| `secondary.name`            | `cas_effector`         | A secondary identifier that can be references in the system definition for groups of proteins rather than individual protein names. |
| `author`                    | `Payne LJ, Jackson SA` | Author(s) of the entry. If the HMM is from an external database, crediting the original author is preferred. If the HMM is from a study where an author was not explicity credited, authorship is attributed to the first author of the study. Multiple authors are separated by a comma (`, `). |
| `e.value.threshold`         | `1e-05`                | The minimum domain iE-value allowed when reporting hits. |
| `hmm.coverage.threshold`    | `0.3`                  | The proportion of the HMM that must contribute to the HMM/target alignment when reporting hits. |
| `target.coverage.threshold` | `0.3`                  | The proportion of the target that must contribute to the HMM/target alignment when reporting hits. |
| `literature.ref`            | `10/f2wkj3`            | The DOI for the literature that implies that the HMM or underlying protein sequences belong to a particular protein family or defence system.  Multiple references are separated by a comma (`, `). DOIs can be resolved at [doi.org](https://www.doi.org/). |
| `database.ref`              | `PFAM; PF06527`        | Reference to the original accession of the alignment/HMM if it was taken from an external database, e.g. PFAM, COG, etc. Includes the name of the database and the identifier separated by a semicolon (`; `). |
| `comment`                   | `NA`                   | Other relevant information. This may include comments from the original database where applicable. |

## System metadata (`sys_meta.txt`)

| Field         | Example             | Description |
| ------------- | ------------------- | ----------- |
| `system`      | `Druantia Type I`   | The human-readable name for the system. |
| `yaml.name`   | `druantia_type_I`   | The exact name of the yaml file that corresponds with the system type (without the `.yaml` extension). |
| `search`      | `TRUE`              | Set to `TRUE` or `FALSE` to determine whether the system is searched or not. |
| `comment`     | `NA`                | Other relevant information. |
| `references`  | `payne2021:10/gzgh` | References to relevant literature that describe the system in the form `surnameYEAR:DOI`. Multiple references are separated by a semicolon (`;`). DOIs can be resolved at [doi.org](https://www.doi.org/). |
| `group`       | `DMS`               | Arbitrary system groups used for dividing data on the PADLOC web server. |
| `fill`        | `#F1F1D1`           | Arbitrary HEX code used for colouring genes on the PADLOC web server. |
| `stroke`      | `#CACA56`           | Arbitrary HEX code used for colouring genes on the PADLOC web server. |

## Adding to the database

Additional HMMs and system models can be added directly to your copy of this database, or a separate database can be set up in the same way as this one.

Additional HMMs can be added to the `hmm/` directory, `hmm_meta.txt` also needs to be updated to include metadata for the new HMMs. When using with [PADLOC](https://github.com/leightonpayne/padloc), these HMMs need to be concatenated into a single file in the `hmm/` directory called `padlocdb.hmm`. This is done automatically when downloading the database using `padloc --db-update` or `padloc --db-install`.

Additional system models can be added to the `sys/` directory, `sys_meta.txt` should also be updated to include metadata for the new models.

## License

This software and data is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

