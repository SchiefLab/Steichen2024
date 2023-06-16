# Steichen2023

This is the public code and data repository for Steichen et al. 2023.

## Data

There are both local and remote datasets in this repository.

### Local datasets

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
| B23         | Not used                                                                                                                            |
| IgG.1       | Not used                                                                                                                            |
