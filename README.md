# Steichen2023

This is the public code and data repository for Steichen et al. 2023.

## Data

There are both local and remote datasets in this repository.

### Local datasets

---

These are datasets in this repository. They are stored in the `data/` directory.

1. [`data/all_processed_combined.feather`](data/all_processed_combined.feather) is the processed 10X dataset with paired heavy and light chains as well as the single cell sort paired data from Sanger sequencing. In addition to having all [AIRR compliant fields](https://docs.airr-community.org/en/stable/datarep/rearrangements.html#fields), this dataset contains the following:

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

### Remote datasets

---

These are datasets that are too large to store in this repository. They are stored in the an AWS S3 bucket.

**74 Macaque naive BCR sequences found in this study**

a. Annotated in feather format and tar zipped [here](https://macaquenaive.s3.us-west-2.amazonaws.com/annotated_feather.tgz). This data does not contain the animal IDs but contains the SRA number.

b. Annotated in parquet format and tar zipped [here](https://macaquenaive.s3.us-west-2.amazonaws.com/parquet.tgz). This data has the animal IDs and after its uncompressed it can be used in AWS EMR.

## Notebooks

We also are adding local notebooks and EMR notebooks that can be run on the 74 macaque naive sequences.

### Local Notebooks

[Notebooks/Process Seqs.ipynb](Notebooks/Process%20Seqs.ipynb) reads in all 10X and single-cell sorting paired sequences from [data/all_processed_combined.feather](data/all_processed_combined.feather) and adds the following fields:

1. Add closest human ortholog to the V and J genes
2. Add the HCDR3 and LCDR3 length
3. Annotate sequences with the BG18 type I criteria.
4. Annotate sequences with the BG18 type I alternative criteria.
5. Assign precursor definitions
6. Run mutational analysis
7. Run clustering on BG18 sequences using the criteria from the paper.

### EMR Notebooks
