## Gender-swapped data corpus

**This is the gender-balanced version** of the [Ukrainian NER corpus](https://github.com/lang-uk/ner-uk/tree/master/v2.0).
The original corpus was filtered to include only texts containing gendered entities, such as those labeled with the \texttt{JOB} tag. We then applied a gender-swapping method to augment the data. This approach enabled us to construct a gender-balanced dataset, ensuring a more equitable distribution of male and female representations (see Table 1,2).

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

- 965 texts
- 27971 NER entities
- 13 types of entities

|                | **NashiGroshi** | **Bruk** | **Total** |
|----------------|------------------|----------|-----------|
| JOB            | 2688             | 1276     | 3964      |
| PERS           | 2878             | 4741     | 7619      |
| ART            | 347              | 355      | 702       |
| DATE           | 1865             | 603      | 2468      |
| DOC            | 124              | 43       | 167       |
| LOC            | 1644             | 1727     | 3371      |
| MISC           | 117              | 436      | 553       |
| MON            | 1015             | 46       | 1061      |
| ORG            | 5692             | 899      | 6591      |
| PCT            | 234              | 78       | 312       |
| PERIOD         | 428              | 266      | 694       |
| QUANT          | 307              | 119      | 426       |
| TIME           | 5                | 38       | 43        |
| **Total**       | **17344**           | **10627**  | **27971**  |

There are five files for each `filename` file from the corpus:

- a file with the extension `.txt` contains the original file text. 
- a file with the extension `.ann` contains NER-annotations for the original file text.
- a file with the extension `-swapped.txt` contains the sentences that have been gender-swapped from the original text sentences. 
- a file with the extension `-swapped.ann` contains NER-annotations for the gender-swapped text.
- a file with the extension `-swapped.meta` maps each sentence in the gender-swapped file to its corresponding sentence in the original file by sentence index.

For model training and validation, use [Standard split into DEV and TEST sets](data/dev-test-split.txt).
