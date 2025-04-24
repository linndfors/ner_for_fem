# ner_for_fem


Structure of the notebooks in the [src directory](src/):

TODO: split by sections

- [Gender Swapping](src/gender_swapper.ipynb) — the main notebook that extracts sentences containing `JOB` entities, uses an LLM to perform gender swapping, prepares a dataset for annotation, and updates annotation files to account for offset shifts. The outcome is a modified dataset with gender-marked, swapped sentences.

- [Filtering Non-Gender-Marked Sentences](src/remove_not_swapped_sentence_from_the_text.ipynb) — a helper notebook that filters the new dataset to retain only gender-swapped sentences, avoiding duplication of other entities. Corresponding annotation files are updated accordingly.

- [Match Original and Swapped Sentences](src/match_swapped_dataset_with_original_by_sentences.ipynb) — matches each modified sentence with its original counterpart to create a parallel dataset while preserving label and filename metadata.

- [Script for Creating Meta Files](src/creating_meta_files.ipynb) — this script matches gender-swapped sentences with their original counterparts by using filenames and entity labels extracted from annotation files. The result is a meta file containing index mappings for each sentence in the `.txt` files.

- [Script for Creating Dataset for LLM](src/create_parallel_dataset_for_llm.ipynb) — this notebook constructs a dataset by merging parallel sentences with gendered word pairs extracted from a dictionary (via GenderGid). The data is then formatted to match the requirements for fine-tuning the LLM (Aya-101), with appropriate instruction-style prompts. Two input types are supported: full sentences and individual word pairs. These are mixed so the input column contains both masculine and feminine examples. Finally, the dataset is split into training and testing sets (80/20).

- [Script to Classify Gender of Entities](src/gender_classification_for_entities.ipynb) — this notebook classifies `JOB` entities into gender categories (female, male, common) by lemmatizing terms using the Stanza and pymorphy libraries, followed by dictionary-based classification using gendered word pairs from GenderGid. A section is also included for classifying `PERS` entities using a dataset of Ukrainian names (note: some names may not reflect common real-world usage, so caution is advised).    

- [Metrics Calculation](src/metrics.ipynb) — a notebook for computing various evaluation metrics, including additional experiments that are not covered in the previously mentioned notebooks.

- [Util folder](./src/util) — contains additional scripts for data inspection, minor filtering, and experimental analysis.


Structure of the [data directory](data)