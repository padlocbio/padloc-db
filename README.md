<a href="https://github.com/padlocbio/padloc-db/LICENSE" alt="License"><img src="https://img.shields.io/github/license/padlocbio/padloc-db" /></a> <a href="https://github.com/padlocbio/padloc-db/releases" alt="Github release"><img src="https://img.shields.io/github/v/release/padlocbio/padloc-db?label=github%20release" /></a> <a href="https://github.com/padlocbio/padloc-db/commits/master" alt="GitHub commits since latest release"><img src="https://img.shields.io/github/commits-since/padlocbio/padloc-db/latest?sort=semver"></a> <a href="https://github.com/padlocbio/padloc-db/" alt="Last update"><img src="https://img.shields.io/github/last-commit/padlocbio/padloc-db?label=last%20update" /></a> 

# PADLOC-DB

## About

This repo contains the latest version of the HMMs and system models used by [PADLOC](https://github.com/padlocbio/padloc). The latest version of this database can be downloaded by running `padloc --db-update`.

The following document describes each field of `hmm_meta.txt` and `sys_meta.txt`, and how you can use your own HMMs and system models with [PADLOC](https://github.com/padlocbio/padloc).

## Citation

If you use [PADLOC](https://github.com/padlocbio/padloc) or [PADLOC-DB](https://github.com/padlocbio/padloc-db) please cite:

> Payne, L.J., Todeschini, T.C., Wu, Y., Perry, B.J., Ronson, C.W., Fineran, P.C., Nobrega, F.L., Jackson, S.A. (2021) Identification and classification of antiviral defence systems in bacteria and archaea with PADLOC reveals new system types. *Nucleic Acids Research*, **49**, 10868-10878. doi: https://doi.org/10/gzgh

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
| `author`         | Payne LJ, Jackson SA             | Author(s) of the entry. If the HMM is from an external database,    crediting the original author is preferred. If the HMM is from a study where an author was not explicity credited, authorship is attributed to the first author of the study. Multiple authors are separated by ', '. |
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

> Bouchard, J. D., Dion, E., Bissonnette, F. and Moineau, S. (2002) Characterization of the Two-Component Abortive Phage Infection Mechanism AbiT from Lactococcus lactis. *Journal of Bacteriology*, **184**, 6325–6332. doi: [10/btq97w](https://doi.org/10/btq97w)

> Parma, D. H., Snyder, M., Sobolevski, S., Nawroz, M., Brody, E. and Gold, L. (1992) The Rex system of bacteriophage lambda: tolerance and altruistic cell death. *Genes Dev.*, **6**, 497–510. doi: [10/b9xpsb](https://doi.org/10/b9xpsb)

> Jabbar, M. A. and Snyder, L. (1984) Genetic and physiological studies of an Escherichia coli locus that restricts polynucleotide kinase- and RNA ligase-deficient mutants of bacteriophage T4. *Journal of Virology*, **51**, 522–529. doi: [10/gndc4t](https://doi.org/10/gndc4t)

> Cram, D., Ray, A. and Skurray, R. (1984) Molecular analysis of F plasmid pif region specifying abortive infection of T7 phage. *Mol Gen Genet*, **197**, 137–142. doi: [10/fg7s8g](https://doi.org/10/fg7s8g)

> Smith, H. S., Pizer, L. I., Pylkas, L. and Lederberg, S. (1969) Abortive Infection of Shigella dysenteriae P2 by T2 Bacteriophage. *Journal of Virology*, **4**, 162–168. doi: [10/gndc4r](https://doi.org/10/gndc4r)

> Dai, G., Su, P., Allison, G. E., Geller, B. L., Zhu, P., Kim, W. S. and Dunn, N. W. (2001) Molecular Characterization of a New Abortive Infection System (AbiU) from Lactococcus lactisLL51-1. *Applied and Environmental Microbiology*, **67**, 5225–5232. doi: [10/cwbxdg](https://doi.org/10/cwbxdg)

> Lindahl, G., Sironi, G., Bialy, H. and Calendar, R. (1970) Bacteriophage Lambda; Abortive Infection of Bacteria Lysogenic for Phage P2. *PNAS*, **66**, 587–594. doi: [10/fkgq7x](https://doi.org/10/fkgq7x)

> Bergsland, K. J., Kao, C., Yu, Y. T. N., Gulati, R. and Snyder, L. (1990) A site in the T4 bacteriophage major head protein gene that can promote the inhibition of all translation in Escherichia coli. *Journal of Molecular Biology*, **213**, 477–494. doi: [10/fv36tb](https://doi.org/10/fv36tb)

> Durmaz, E. and Klaenhammer, T. R. (2007) Abortive Phage Resistance Mechanism AbiZ Speeds the Lysis Clock To Cause Premature Lysis of Phage-Infected Lactococcus lactis. *Journal of Bacteriology*, **189**, 1417–1425. doi: [10/dnndhw](https://doi.org/10/dnndhw)

> Haaber, J., Moineau, S., Fortier, L. C. and Hammer, K. (2008) AbiV, a Novel Antiphage Abortive Infection Mechanism on the Chromosome of Lactococcus lactis subsp. cremoris MG1363. *Applied and Environmental Microbiology*, **74**, 6528–6537. doi: [10/cnwcq7](https://doi.org/10/cnwcq7)

> Emond, E., Dion, E., Walker, S. A., Vedamuthu, E.R., Kondo, J.K. and Moineau, S. (1998) AbiQ, an Abortive Infection Mechanism fromLactococcus lactis. *Applied and Environmental Microbiology*, **64**, 4748–4756. doi: [10/gndc4p](https://doi.org/10/gndc4p)

> Domingues, S., Chopin, A., Ehrlich, S. D. and Chopin, M. C. (2004) The Lactococcal Abortive Phage Infection System AbiP Prevents both Phage DNA Replication and Temporal Transcription Switch. *Journal of Bacteriology*, **186**, 713–721. doi: [10/bjjwc6](https://doi.org/10/bjjwc6)

> Prevots, F. and Ritzenthaler, P. (1998) Complete Sequence of the New Lactococcal Abortive Phage Resistance Gene abiO. *Journal of Dairy Science*, **81**, 1483–1485. doi: [10/cg69rg](https://doi.org/10/cg69rg)

> Prévots, F., Tolou, S., Delpech, B., Kaghad, M. and Daloyau, M. (1998) Nucleotide sequence and analysis of the new chromosomal abortive infection gene abiN of Lactococcus lactis subsp. cremoris S114. *FEMS Microbiology Letters*, **159**, 331–336. doi: [10/c94sd6](https://doi.org/10/c94sd6)

> Deng, Y. M., Liu, C. Q. and W. Dunn, N. (1999) Genetic organization and functional analysis of a novel phage abortive infection system, AbiL, from Lactococcus lactis. *Journal of Biotechnology*, **67**, 135–149. doi: [10/bwc9k8](https://doi.org/10/bwc9k8)

> Emond, E., Holler, B. J., Boucher, I., Vandenbergh, P. A., Vedamuthu, E. R., Kondo, J. K. and Moineau, S. (1997) Phenotypic and genetic characterization of the bacteriophage abortive infection mechanism AbiK from Lactococcus lactis. *Applied and Environmental Microbiology*, **63**, 1274–1283. doi: [10/gndc4n](https://doi.org/10/gndc4n)

> Deng, Y. M., Harvey, M. L., Liu, C. Q. and Dunn, N. W. (1997) A novel plasmid-encoded phage abortive infection system from Lactococcus lactis biovar. diacetylactis. *FEMS Microbiology Letters*, **146**, 149–154. doi: [10/d24tcq](https://doi.org/10/d24tcq)

> Su, P., Harvey, M., Im, H. J. and Dunn, N. W. (1997) Isolation, cloning and characterisation of the abiI gene from Lactococcus lactis subsp. lactis M138 encoding abortive phage infection. *Journal of Biotechnology*, **54**, 95–104. doi: [10/ckwmpp](https://doi.org/10/ckwmpp)

> Prévots, F., Daloyau, M., Bonin, O., Dumont, X. and Tolou, S. (1996) Cloning and sequencing of the novel abortive infection gene abiH of Lactococcus lactis ssp. lactis biovar. diacetylactis S94. *FEMS Microbiology Letters*, **142**, 295–299. doi: [10/dvjcb5](https://doi.org/10/dvjcb5)

> O’Connor, L., Coffey, A., Daly, C. and Fitzgerald, G. F. (1996) AbiG, a genotypically novel abortive infection mechanism encoded by plasmid pCI750 of Lactococcus lactis subsp. cremoris UC653. *Applied and Environmental Microbiology*, **62**, 3075–3082. doi: [10/gndc4m](https://doi.org/10/gndc4m)

> Garvey, P., Fitzgerald, G. F. and Hill, C. (1995) Cloning and DNA sequence analysis of two abortive infection phage resistance determinants from the lactococcal plasmid pNP40. *Applied and Environmental Microbiology*, **61**, 4321–4328. doi: [10/gndc3x](https://doi.org/10/gndc3x)

> Dy, R. L., Przybilski, R., Semeijn, K., Salmond, G. P. C. and Fineran, P. C. (2014) A widespread bacteriophage abortive infection system functions through a Type IV toxin–antitoxin mechanism. *Nucleic Acids Research*, **42**, 4590–4605. doi: [10/f5zkmw](https://doi.org/10/f5zkmw)

> McLandsborough, L.A., Kolaetis, K. M., Requena, T. and McKay, L. L. (1995) Cloning and characterization of the abortive infection genetic determinant abiD isolated from pBF61 of Lactococcus lactis subsp. lactis KR5. *Applied and Environmental Microbiology*, **61**, 2023–2026. doi: [10/gndc4j](https://doi.org/10/gndc4j)

> Garvey, P., Fitzgerald, G. F. and Hill, C. (1995) Cloning and DNA sequence analysis of two abortive infection phage resistance determinants from the lactococcal plasmid pNP40. *Applied and Environmental Microbiology*, **61**, 4321–4328. doi: [10/gndc3x](https://doi.org/10/gndc3x)

> Anba, J., Bidnenko, E., Hillier, A., Ehrlich, D. and Chopin, M. C. (1995) Characterization of the lactococcal abiD1 gene coding for phage abortive infection. *Journal of Bacteriology*, **177**, 3818–3823. doi: [10/gndc3w](https://doi.org/10/gndc3w)

> Durmaz, E., Higgins, D. L. and Klaenhammer, T. R. (1992) Molecular characterization of a second abortive phage resistance gene present in Lactococcus lactis subsp. lactis ME2. *Journal of Bacteriology*, **174**, 7463–7469. doi: [10/gndc3v](https://doi.org/10/gndc3v)

> Parreira, R., Ehrlich, S. D. and Chopin, M. C. (1996) Dramatic decay of phage transcripts in lactococcal cells carrying the abortive infection determinant AbiB. *Molecular Microbiology*, **19**, 221–230. doi: [10/b835bf](https://doi.org/10/b835bf)

> Cluzel, P. J., Chopin, A., Ehrlich, S. D. and Chopin, M. C. (1991) Phage abortive infection mechanism from Lactococcus lactis subsp. lactis, expression of which is mediated by an Iso-ISS1 element. *Applied and Environmental Microbiology*, **57**, 3547–3551. doi: [10/gndc3t](https://doi.org/10/gndc3t)

> Dinsmore, P. K. and Klaenhammer, T. R. (1994) Phenotypic Consequences of Altering the Copy Number of abiA, a Gene Responsible for Aborting Bacteriophage Infections in Lactococcus lactis. *Applied and Environmental Microbiology*, **60**, 1129–1136. doi: [10/gndc3s](https://doi.org/10/gndc3s)

> Owen, S. V., Wenner, N., Dulberger, C. L., Rodwell, E. V., Bowers-Barnard, A., Quinones-Olvera, N., Rigden, D. J., Rubin, E. J., Garner, E. C., Baym, M., et al. (2021) Prophages encode phage-defense systems with cognate self-immunity. *Cell Host & Microbe*, **29**, 1620-1633 doi: [10/g29b](https://doi.org/10/g29b)

The relevant refences for individual HMMs can be found by inspecting the `hmm_meta.txt` file provided with [PADLOC-DB](https://github.com/padlocbio/padloc-db).

## License

This software and data is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

