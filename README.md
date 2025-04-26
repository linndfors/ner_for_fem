# Gender-swapping tool


This project corresponds to my thesis work: <b>Gender Swapping as a Data Augmentation Technique: Developing Gender-Balanced Datasets for Ukrainian Language Processing</b>.

While all experimental results and analyses are presented in the thesis, this repository contains the full codebase used to run the experiments and evaluate the outcomes. The following sections describe the contents of each directory in the repository to facilitate easier navigation.


## Structure of the notebooks in the [src](src) directory:

This directory contains a collection of Jupyter notebooks developed during the research phase of the project. While the long-term goal is to consolidate these into a streamlined pipeline or a series of sequential scripts, the current structure reflects the exploratory nature of the work. Each notebook focuses on a specific component of the gender-swapping workflow or an individual experiment. They are organized in the order they were used to develop the dataset, train and evaluate models, and gather general performance metrics.


- <b>Gender-swapped dataset creation</b>

    - [Gender Swapping notebook](src/1_gender_swapping.ipynb): The main notebook that extracts sentences containing `JOB` entities, uses an LLM to perform gender swapping, prepares a dataset for annotation, and updates annotation files to account for offset shifts. The result is a modified dataset with gender-marked, swapped sentences.

    - [Filtering Non-Gender-Marked Sentences notebook](src/2_remove_not_swapped_sentence_from_the_text.ipynb): A helper notebook that filters the new dataset to retain only gender-swapped sentences, avoiding duplication of other entities. Corresponding annotation files are updated accordingly.

    - [Match Original and Swapped Sentences notebook](src/3_match_swapped_dataset_with_original_by_sentences.ipynb): Matches each modified sentence with its original counterpart to create a parallel dataset while preserving label and filename metadata.

    - [Script for Creating Meta Files notebook](src/4_creation_of_meta_files.ipynb): This script matches gender-swapped sentences with their original counterparts using filenames and entity labels extracted from annotation files. The output is a meta file containing index mappings for each sentence in the `.txt` files.

    After completing these steps, we obtained the [Gender-swapped corpora](data/v2.0-swapped), which includes `.txt`, `.ann`, and `.meta` files for each original file.


    *Note: To collect a gender-balanced dataset, we simply add the gender-swapped dataset to the original and merge their train-test split files.*

---

- <b>LLM</b>

    - [Constructing Dataset for LLM notebook](src/5_creation_of_parallel_dataset_for_llm.ipynb): Constructs a dataset by merging parallel sentences with gendered word pairs extracted from a dictionary (via GenderGid). The data is formatted to match the requirements for fine-tuning the [Aya-101 LLM](https://huggingface.co/CohereLabs/aya-101), using instruction-style prompts. Two input types are supported: full sentences and individual word pairs. These are mixed so that the input column contains both masculine and feminine examples. The dataset is then split into training and test sets (80/20).

    - [LLM fine-tuning notebook](src/ner_and_llm_models/train_llm_aya-101.ipynb): Fine-tunes the Aya-101 model using the dataset of parallel gender-marked sentences. The fine-tuned model is saved on the [HF repo](https://huggingface.co/linndfors/uk-gender-swapper-aya-101).

    - [LLM comparison evaluation notebook](src/ner_and_llm_models/eval_llm_aya-101.ipynb): Compares metrics including BLEU, BERTScore, ROUGE-L, and Exact Match across the original Aya-101 model and GPT-4o-mini. Results are saved [here](data/results_of_evaluation/LLM_models_comparisson).

---

- <b>NER</b>

    - [Training NER notebook](src/ner_and_llm_models/train_NER.ipynb): Trains the NER model using the [Gender-balanced dataset](data/v2.0-balanced). To prepare the data, the train, dev, and test sets are transformed into the [IOB format](data/iob_format/balanced_iob_format), then converted to spaCy format. The same [config](src/ner_and_llm_models/config.cfg) as the NER_UK model is used. The model is published on the [HF repo](https://huggingface.co/linndfors/uk_ner_gender-balanced).

    - The second part of the notebook compares the Original NER model (loaded from the [HF repo](https://huggingface.co/dchaplinsky/uk_ner_web_trf_13class)) with the Gender-balanced NER model across the original, swapped, and gender-balanced test sets. Results are saved [here](data/results_of_evaluation/NER_evaluation_results).


---

- <b>Metrics calculation/Evaluation</b>

    - [Extract JOB titles recognition using NER notebook](src/ner_and_llm_models/ner_for_JOB_entities_accuracy.ipynb): Extracts True Positives and False Negatives for `JOB` entities using the Gender-balanced NER model. Results are saved [here](data/results_of_evaluation/NER_JOB_class_results).

    - [Script to Classify Gender of Entities notebook](src/gender_classification_for_entities.ipynb): Classifies `JOB` entities into gender categories (female, male, common) by lemmatizing terms using Stanza and pymorphy, followed by dictionary-based classification with gendered word pairs. A section is also included for classifying `PERS` entities using a dataset of Ukrainian names (note: some names may not reflect common real-world usage, so caution is advised). This notebook also calculates <b>recall</b> for `JOB` entities, split by gender.

    - [Metrics Calculation notebook](src/metrics.ipynb): Computes various evaluation metrics, including experiments not covered in the other notebooks. Calculates: Exact Match without `PERS`, JOB Match, Token Count Match for LLM comparison. Check the original dataset to find the dictionary pairs matching. Also includes analysis and evaluation of the annotation project.

    - [Util folder](./src/util): Contains additional scripts for data inspection, minor filtering, and experimental analysis (e.g., checking whether indices in annotation files correspond to the content of text files, inspecting entity distributions in corpora, etc.).

----

## Structure of the [data](data) directory

- Corpora

    - [Original corpora](data/v2.0) – a direct copy of the original [NER-UK 2.0 corpora](https://github.com/lang-uk/ner-uk/tree/master/v2.0).
    - [Gender-swapped corpora](data/v2.0-swapped) – a gender-swapped version of the gender-marked text extracted from the original NER-UK 2.0 corpora.
    - [Augmented corpora](data/v2.0-balanced) – a merged version of the original and gender-swapped corpora, forming the final gender-balanced dataset.

    Each directory contains two subdirectories split into the "NashiGroshi" and "BRUK" datasets. Additionally, dev-test split files are provided for each corpus.

Also, you can find the LLM prompt used to generate the initial (bronze) gender-swapped dataset [here](data/prompt.txt).

*Note: Other files in this directory are functional outputs from notebooks and can be considered utilities.*

## Annotation Project

In this [file](annotation_project/annotation_instruction.txt), you can find the instructions provided to annotators to ensure consistency. It includes examples, annotation rules, reference dictionaries, and general guidelines for reviewing the dataset.

- [Dataset for annotation](annotation_project/sentences_for_annotation) – a collection of gender-parallel sentences generated by the LLM, requiring manual revision.
- [Dataset after annotation](annotation_project/sentences_after_annotation) – the same set of sentence pairs after annotation, where each pair is marked as *Correct*, *Incorrect*, or *Difficult to Determine*. After annotation, we processed the data to exclude pairs labeled as *Difficult to Determine* or those that remained unchanged after gender-swapping.
