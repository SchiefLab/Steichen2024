# Steichen2023

This is the public code and data repository for Steichen et al. 2023.

## Data

There are both local and remote datasets in this repository.

### Local datasets

---

These are datasets in this repository. They are stored in the `data/` directory.

1. [`data/all_processed_combined.csv.gz`](data/all_processed_combined.csv.gz) is the processed 10X dataset with paired heavy and light chains as well as the single cell sort paired data from Sanger sequencing. In addition to having all [AIRR compliant fields](https://docs.airr-community.org/en/stable/datarep/rearrangements.html#fields), this dataset contains the following:

| Field       | Description                                                                                                                         |
| :---------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| sequence_id | A unique ID describing the sequence, takes the form: `<animal id>_<weeks post>_<tissue>_<sequencing method>_<index_number>_<probe>` |
| barcode     | The barcode from the 10X GEM                                                                                                        |
| NHP         | The NHP animal ID                                                                                                                   |
| weeks_post  | Weeks post vaccination. 3,4,7,10,13 or 710 (weeks 7 or 10)                                                                          |
| tissue      | GC or MBC                                                                                                                           |
| seq_method  | Sequencing Method, 10X or Sanger                                                                                                    |
| prime_boost | Sequence isolated after prime or boost or was a control (MD39)                                                                      |
| probe       | Probe population of this sequence [Env+, Env-, Env++KO-]                                                                            |
| KO.         | How many counts of the barcode labeled KO probe                                                                                     |
| well_id     | Well ID for the single cell sort                                                                                                    |
| IgG         | The ELISA signal for IgG                                                                                                            |
| N332-GT5 WT | The ELISA signal for GT5                                                                                                            |
| N332-GT5 KO | The ELISA signal for the KO                                                                                                         |
| B23         | The boosting reagent ELISA                                                                                                          |
| IgG.1       | The boolean measure for if it is an IgG                                                                                             |

2. [`data/all_processed_combined_personalized.csv.gz`](data/all_processed_combined_personalized.csv.gz) is the same as `data/all_processed_combined.csv.gz` but with the sequences personalized to the IGHD3-43 allele haplotypes found in [data/genotypes.xlsx](data/genotype.xlsx). The haplotypes are:

   a. `IGHD3-43*01/IGHD3-43*01`

   b. `IGHD3-43*01/IGHD3-43*01_S8240`

   c. `IGHD3-43*01_S8240/IGHD3-43*01_S8240`

### Remote datasets

---

These are datasets that are too large to store in this repository. They are stored in the an AWS S3 bucket.

**74 Macaque naive BCR sequences found in this study**

a. Annotated in feather format and tar zipped [here](https://macaquenaive.s3.us-west-2.amazonaws.com/annotated_feather.tgz). This data does not contain the animal IDs but contains the SRA number.

b. Annotated in parquet format and tar zipped [here](https://macaquenaive.s3.us-west-2.amazonaws.com/parquet.tgz). This data has the animal IDs and after its uncompressed it can be used in AWS EMR.

## Notebooks

We also are adding local notebooks and EMR notebooks that were used in this study.

### Local Notebooks

[Personalize Seqs.ipynb](local_notebooks/Personalize%20Seqs.ipynb) reads in all 10X data from [data/all_processed_combined.feather](data/all_processed_combined.feather) and reannotates the sequences based on the IGHD3-43 allele haplotypes found in [data/genotypes.xlsx](data/genotype.xlsx)

[Process Seqs.ipynb](local_notebooks/Process%20Seqs.ipynb) reads in all 10X and single-cell sorting paired and personalized sequences from [data/all_processed_combined_personalized.feather](data/all_processed_combined_personalized.feather) and adds the following fields:

1. Add closest human ortholog to the V and J genes
2. Add the HCDR3 and LCDR3 length
3. Annotate sequences with BG18 type I criteria.
4. Annotate sequences with BG18 type I criteria with alternative D3-41 reading frame.
5. Assign precursor definitions
6. Run mutational analysis
7. Run clustering on BG18 sequences using the criteria from the paper.

### EMR Notebooks

[BG18 human precursors](emr_notebooks/BG18%20human%20precursor%202023.ipynb) searched for human BG18-like precursors and calculate their frequencies on NGS datasets of 1.1 billion human BCR heavy chain sequences from 14 human donors that were previously described (Briney et al., 2019; Steichen et al., 2019; Willis et al., 2023).

[BG18 macaque precursors](emr_notebooks/BG18%20macaque%20precursor%202023.ipynb) searched for rhesus macaque BG18-like precursors and calculate their frequencies on 154 datasets of 95.4 million macaque BCR sequences from 60 macaques.
