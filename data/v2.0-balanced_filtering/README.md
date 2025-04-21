## Gender-swapped data corpus

**This is the gender-balanced version** of the [Ukrainian NER corpus](https://github.com/lang-uk/ner-uk/tree/master/v2.0).
The original corpus was filtered to include only texts containing gendered entities, such as those labeled with the <b>JOB</b> tag. We then applied a gender-swapping method to augment the data. This approach enabled us to construct a gender-balanced dataset, ensuring a more equitable distribution of male and female representations (see Table 1,2).

| Dataset           | **Total** | **Male Count** | **Male %** | **Female Count** | **Female %** | **Common Count** | **Common %** | **Unknown Count** | **Unknown %**  |
|-------------------|-----------|----------------|------------|------------------|--------------|------------------|--------------|-------------------|----------------|
| Original dataset  | 1982      | 1646           | 83%        | 76               | 3.8%         | 223              | 11.3%        | 37                | 1.8%           |
| Augmented dataset | 3715      | 1828           | 49.2%      | 1392             | 37.4%        | 393              | 10.5%        | 102               | 2.7%           |



<p align="center"><strong>Table 1.</strong> Gender composition of <code>JOB</code> entities</p>

| Dataset           | **Total** | **Male Count** | **Male %** | **Female Count** | **Female %** | **Unknown Count** | **Unknown %**  |
|-------------------|-----------|----------------|------------|------------------|--------------|-------------------|----------------|
| Original dataset  | 6235      | 2120           | 34.0%      | 1286             | 20.6%        | 2829              | 45.4%          |
| Augmented dataset | 7517      | 2276           | 30.2%      | 2016             | 26.8%        | 3225              | 42.9%          |


<p align="center"><strong>Table 2.</strong> Gender composition of <code>PERS</code> entities</p>

### Description

The labeled data corpus is located in the `v2.0-balanced/data` folder.

Total in the corpus:

- 955 texts (train=600, dev=66, test=289)
- 27,378 NER entities
- 13 types of entities

|                | **NashiGroshi** | **Bruk** | **Total** |
|----------------|------------------|----------|-----------|
| JOB            | 2592             | 1123     | 3715      |
| PERS           | 2822             | 4695     | 7517      |
| ART            | 344              | 339      | 683       |
| DATE           | 1825             | 596      | 2421      |
| DOC            | 120              | 40       | 160       |
| LOC            | 1630             | 1711     | 3341      |
| MISC           | 116              | 434      | 550       |
| MON            | 1005             | 46       | 1051      |
| ORG            | 5598             | 882      | 6480      |
| PCT            | 234              | 77       | 311       |
| PERIOD         | 418              | 266      | 684       |
| QUANT          | 303              | 119      | 422       |
| TIME           | 5                | 38       | 43        |
| **Total**       | **17012**           | **10366**  | **27378**  |

There are five files for each `filename` file from the corpus:

- a file with the extension `.txt` contains the original file text. 
- a file with the extension `.ann` contains NER-annotations for the original file text.
- a file with the extension `-swapped.txt` contains the sentences that have been gender-swapped from the original text sentences. 
- a file with the extension `-swapped.ann` contains NER-annotations for the gender-swapped text.
- a file with the extension `-swapped.meta` maps each sentence in the gender-swapped file to its corresponding sentence in the original file by sentence index.

For model training and validation, use [Standard split into DEV and TEST sets](data/dev-test-split.txt).
