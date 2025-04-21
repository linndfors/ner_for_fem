## Gender-swapped data corpus

**This is the gender-balanced version** of the [Ukrainian NER corpus](https://github.com/lang-uk/ner-uk/tree/master/v2.0).
The original corpus was filtered to include only texts containing gendered entities, such as those labeled with the <b>JOB</b> tag. We then applied a gender-swapping method to augment the data. This approach enabled us to construct a gender-balanced dataset, ensuring a more equitable distribution of male and female representations (see Table 1,2).

        | Dataset           | **Total** | **Male Count** | **Male %** | **Female Count** | **Female %** | **Common Count** | **Common %** | **Unknown Count** | **Unknown %**  |
        |-------------------|-----------|----------------|------------|------------------|--------------|------------------|--------------|-------------------|----------------|
        | Original dataset  | 1982      | 1643           | 83%        | 73               | 3.6%         | 223              | 11.3%        | 37                | 1.8%           |
        | Swapped dataset   | 1982      | 226            | 11.4%      | 1443             | 73%          | 212              | 10.7%        | 95                | 4.8%           |
        | Balanced dataset  | 3964      | 1869           | 47%        | 1516             | 38%          | 435              | 11%          | 132               | 3.2%           |


<p align="center"><strong>Table 1.</strong> Gender composition of <code>JOB</code> entities</p>

                    | Dataset           | **Total** | **Male Count** | **Male %** | **Female Count** | **Female %** | **Unknown Count** | **Unknown %**  |
                    |-------------------|-----------|----------------|------------|------------------|--------------|-------------------|----------------|
                    | Original dataset  | 6235      | 2120           | 34%        | 1286             | 20.6%        | 2829              | 45.4%          |
                    | Swapped dataset   | 1384      | 222            | 16%        | 734              | 53%          | 428               | 31%            |
                    | Balanced dataset  | 7619      | 2342           | 30.7%      | 2020             | 26.5%        | 3257              | 42.7%          |

<p align="center"><strong>Table 2.</strong> Gender composition of <code>PERS</code> entities</p>

### Description

The labeled data corpus is located in the `v2.0-balanced/data` folder.

Total in the corpus:

- 965 texts (train=600, dev=66, test=289)
- 27971 NER entities
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
