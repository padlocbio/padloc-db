<a href="https://github.com/padlocbio/padloc-db/LICENSE" alt="License"><img src="https://img.shields.io/github/license/padlocbio/padloc-db" /></a> <a href="https://github.com/padlocbio/padloc-db/releases" alt="Github release"><img src="https://img.shields.io/github/v/release/padlocbio/padloc-db?label=github%20release" /></a> <a href="https://github.com/padlocbio/padloc-db/commits/master" alt="GitHub commits since latest release"><img src="https://img.shields.io/github/commits-since/padlocbio/padloc-db/latest?sort=semver"></a> <a href="https://github.com/padlocbio/padloc-db/" alt="Last update"><img src="https://img.shields.io/github/last-commit/padlocbio/padloc-db?label=last%20update" /></a> 

# PADLOC-DB

## About

This repo contains the latest version of the HMMs and system models used by [PADLOC](https://github.com/padlocbio/padloc). The latest version of this database can be downloaded by running `padloc --db-update`.

The following document describes each field of `hmm_meta.txt` and `sys_meta.txt`, and how you can use your own HMMs and system models with [PADLOC](https://github.com/padlocbio/padloc).

## Citation

If you use [PADLOC](https://github.com/padlocbio/padloc) or [PADLOC-DB](https://github.com/padlocbio/padloc-db) please cite:

> Payne, L.J., Todeschini, T.C., Wu, Y., Perry, B.J., Ronson, C.W., Fineran, P.C., Nobrega, F.L., Jackson, S.A. (2021) Identification and classification of antiviral defence systems in bacteria and archaea with PADLOC reveals new system types. *Nucleic Acids Res*, **X**, XXXX-XXXX. doi: [10/gzgh](https://doi.org/10/gzgh)

The HMMs in [PADLOC-DB](https://github.com/padlocbio/padloc-db) were built/curated using data from various sources, we encourage you to also give credit to these groups by [citing them too](#References).

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
| `literature.ref` | 10/f2wkj3                        | The DOI for the literature that implies that the HMM or underlying proteins belong to the protein/defence system.  Multiple references are separated by ', '. DOIs can be resolved at [doi.org](https://www.doi.org/). |
| `database.ref`   | PFAM; PF06527                    | Reference to the original accession of the alignment/HMM if it was taken from an external database, e.g. PFAM, COG, etc. Includes the name of the database and the identifier separated by '; '. |

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

## References

The HMMs in [PADLOC-DB](https://github.com/padlocbio/padloc-db) were built/curated using data from various sources, we encourage you to also give credit to these groups by citing them too:

> Doron, S., Melamed, S., Ofir, G., Leavitt, A., Lopatina, A., Keren, M., Amitai, G. and Sorek, R. (2018) Systematic discovery of antiphage defense systems in the microbial pangenome. *Science*, **359**, eaar4120. doi: [10/ggqhzm](https://doi.org/10/ggqhzm)

> Millman, A., Melamed, S., Amitai, G. and Sorek, R. (2020) Diversity and classification of cyclic-oligonucleotide-based anti-phage signalling systems. *Nature Microbiology*, **5**, 1608–1615. doi: [10/gg84nk](https://doi.org/10/gg84nk)

> Couvin, D., Bernheim, A., Toffano-Nioche, C., Touchon, M., Michalik, J., Néron, B., Rocha, E. P. C., Vergnaud, G., Gautheret, D. and Pourcel, C. (2018) CRISPRCasFinder, an update of CRISRFinder, includes a portable version, enhanced performance and integrates search for Cas proteins. *Nucleic Acids Res*, **46**, W246–W251. doi: [10/ggdjdf](https://doi.org/10/ggdjdf)

> Makarova, K. S., Wolf, Y. I., Iranzo, J., Shmakov, S. A., Alkhnbashi, O. S., Brouns, S. J. J., Charpentier, E., Cheng, D., Haft, D. H., Horvath, P., et al. (2020) Evolutionary classification of CRISPR–Cas systems: a burst of class 2 and derived variants. *Nat Rev Microbiol*, **18**, 67–83. doi: [10/ggkfgj](https://doi.org/10/ggkfgj)

> Shah, S. A., Alkhnbashi, O. S., Behler, J., Han, W., She, Q., Hess, W. R., Garrett, R. A. and Backofen, R. (2019) Comprehensive search for accessory proteins encoded with archaeal and bacterial type III CRISPR-cas gene cassettes reveals 39 new cas gene families. *RNA Biology*, **16**, 530–542. doi: [10/ggqv9p](https://doi.org/10/ggqv9p)

> Shmakov, S. A., Makarova, K. S., Wolf, Y. I., Severinov, K. V. and Koonin, E. V. (2018) Systematic prediction of genes functionally linked to CRISPR-Cas systems by gene neighborhood analysis. *PNAS*, **115**, E5307–E5316. doi: [10/gdpqwq](https://doi.org/10/gdpqwq)

> Russel, J., Pinilla-Redondo, R., Mayo-Muñoz, D., Shah, S. A. and Sørensen, S. J. (2020) CRISPRCasTyper: Automated Identification, Annotation, and Classification of CRISPR-Cas Loci. *The CRISPR Journal*, **3**, 462–469. doi: [10/gshm](https://doi.org/10/gshm)

> Gao, L., Altae-Tran, H., Böhning, F., Makarova, K. S., Segel, M., Schmid-Burgk, J. L., Koob, J., Wolf, Y. I., Koonin, E. V. and Zhang, F. (2020) Diverse enzymatic activities mediate antiviral immunity in prokaryotes. *Science*, **369**, 1077–1084. doi: [10/gpsx](https://doi.org/10/gpsx)

> Makarova, K. S., Timinskas, A., Wolf, Y. I., Gussow, A. B., Siksnys, V., Venclovas, Č. and Koonin, E. V. (2020) Evolutionary and functional classification of the CARF domain superfamily, key sensors in prokaryotic antivirus defense. *Nucleic Acids Res*, **48**, 8828–8847. doi: [10/gg7qx6](https://doi.org/10/gg7qx6)

The relevant refences for individual HMMs can be found by inspecting the `hmm_meta.txt` file provided with [PADLOC-DB](https://github.com/padlocbio/padloc-db).

## License

This software and data is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

