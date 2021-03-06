# cds-language_Assignment_5

***Class assignment for language analytics class at Aarhus University.***

***2021-04-06***




# LDA topic modeling: exploration of topics in American television sitcom 'Friends'


## About the research question
This assignment is Class Assignment 5 - applying unsupervised machine learning to text data. For this assignment I have chosen to train an LDA model on American television sitcom FRIENDS full script (10 seasons and 228 episodes). TV show FRIENDS is one of the  most popular TV series in history and I am a huge fan of it (I have seen the full series at least 3 times). Therefore, it is very interesting to test whether the conversations of the characters can be used to find meaningful topics. If so, then it can be used to define what the characters were talking about the most, which could be used for sociological purposes. This investigation is purely exploratory. I will investigate the following questions:

__QUESTION 1:__ Can LDA model find coherent and semantically meaningful topics FRIENDS´ main characters are talking about?

__QUESTION 2:__ Can the dialogues/monologues of different characters be easily compared and does it reflect relevant topics according to a character? 


## Methods
The problem of the task relates to uncovering hidden structure in a collection of texts - screenplay script of TV series FRIENDS. To address this problem, firstly, I have preprocessed the full screenplay script of FRIENDS TV series and prepared it for the topic modeling task (see Data section below). Secondly, I have used Latent Dirichlet Allocation (LDA) algorithm to perform topic modeling using ```Gensim``` package. I trained LDA model on full TV show´s script and on filtered dialogue lines from each character separately, which resulted in 7 LDA models. Each model was looking for 15 topics. The script outputs ```pyLDAvis``` topic graphs as html files for the full script and each character separately. Also, it saves CSV files for full script and each character to further investigate the topics and their keywords, prints perplexity and coherence metrics for each model to the terminal.


## Repository contents

| File | Description |
| --- | --- |
| data/ | Folder containing input files for the script |
| data/FRIENDS_Script.zip | Archived input txt files of FRIENDS TV show screenplay scripts |
| output/ | Folder containing CSV files produced by the script |
| output/topics_full.csv | Keywords and other metrics for each topic of the full script LDA model |
| output/topics_character.csv | Keywords and other metrics for each topic of each FRIENDS main character´s LDA model (6 files) |
| src/ | Folder containing the script |
| src/LDA.py | The topic modeling script |
| utils/ | Folder containing utility script for the project |
| utils/lda_utils.py | utility script used for data preprocessing |
| viz/ | Folder containing output pyLDAvis graphs produced by the script |
| viz/full_vis.html | html file of pyLDAvis graph of the full script LDA model |
| viz/character_vis.html | html files of pyLDAvis graphs of each FRIENDS main character´s LDA model (6 files) |
| LICENCSE| A software license defining what other users can and can't do with the source code |
| README.md | Description of the assignment and the instructions |
| create_lda_venv.sh | bash file for creating a virtual environmment  |
| kill_lda_venv.sh | bash file for removing a virtual environment |
| requirements.txt | list of python packages required to run the script |




## Data

Data for this project consists of txt files of the Screenplay Scripts and Dialogue for each episode in the FRIENDS TV Show (228 episodes in total).

Data can be found here: https://www.kaggle.com/blessondensil294/friends-tv-series-screenplay-script


__Data structure__

All the txt files must be located in 'FRIENDS_TV_script' folder located in 'data' folder.


__Data preprocessing__

The Screenplay Scripts and Dialogue were preprocessed before training LDA models. Preprocessing involved the following steps:
-  separating staging directions from conversations and returning only conversations
-  filtering out frequent but semantically meaningless words
-  creating chunks of 30-40 sentences (40 for full script, 30 for separate character models)
-  removing stopwords, forming bigrams and trigrams with a threshold value of 100, performing lemmatization of NOUNS (see lda_utils utility functions in utils folder)
-  filtering each character lines for LDA models


## Intructions to run the code

The code was tested on an HP computer with Windows 10 operating system. It was executed on Jupyter worker02.

__Code parameters__


| Parameter | Description |
| --- | --- |
| input_files  (input) | Directory of input files |
| number_topics (n_topics) | Number of topics for LDA model to look for. Default = 15 |
| threshold_value (t) | A score threshold for forming the bigram and trigram models (higher means fewer phrases). Default = 100 |
| postags (pos) | Choose part-of-speech to train LDA model on. Allowed postags: NOUN, ADJ, VERB, ADV. Default = NOUN |



__Steps__

Set-up:
```
#1 Open terminal on worker02 or locally
#2 Navigate to the environment where you want to clone this repository
#3 Clone the repository
$ git clone https://github.com/Rutatu/cds-language_Assignment_5.git 

#4 Navigate to the newly cloned repo
$ cd cds-language_Assignment_5

#5 Create virtual environment with its dependencies and activate it
$ bash create_lda_venv.sh
$ source ./lda/bin/activate

#6 Unzip the input files in a data folder
$ cd data
$ unzip FRIENDS_Script.zip -d FRIENDS_TV_script

``` 

Run the code:

```
#7 Navigate to the directory of the script
$ cd ../src

#8 Run the code with default parameters
$ python LDA.py -input ../data/FRIENDS_TV_script

#9 Run the code with self-chosen parameters
$ python LDA.py -input ../data/FRIENDS_TV_script -n_top 5 -t 150 -pos ADJ

#10 To remove the newly created virtual environment
$ bash kill_lda_venv.sh

#11 To find out possible arguments for the script
$ python LDA.py --help


 ```

I hope it worked!



## Results

## Answers to research questions

__A to Q1:__ The pyLDAvis graph of the full script shows that it is possible to distinguish between relatively separate topics (the bubbles do not overlap too much and there is some distance between them). Most of the topics are rather specific (the majority of bubbles are quite small), probably reflecting  specific episodes or seasons. Nevertheless, as expected, most frequent terms are ´friend´, ´baby´, ´wedding´, ´coffee´, ´date´, ´sex´, which roughly reflect the most crucial topics in the show.

__A to Q2:__ The overall structure of the separate characters´  pyLDAvis graphs (size, position of the bubbles) is similar to the full script graph. Thus, we can say that it does distinguish meaningful topics, but they tend to be pretty specific. Interestingly, most frequent terms for each character represent them pretty well (you must have seen the episodes many times to say that).

Most relevant frequent terms for each character:
- __Chandler:__ wedding, game, sleep, work, relationship
- __Ross:__ date, baby, dad, love, wedding
- __Rachel:__ ross, baby, coffee, purse
- __Phoebe:__ mom, grandmother, fun
- __Monica:__ baby, problem, cookie, potato, wedding
- __Joey:__ girl, butt, sex, night, pheebs, woman


## Models Metrics

Full script
Perplexity: - 10.55
Coherence: 0.28

Chandler
Perplexity: - 7.87
Coherence: 0.30

Monica
Perplexity: - 7.88
Coherence: 0.27

Ross
Perplexity: - 7.51
Coherence: 0.28

Rachel
Perplexity: - 7.82
Coherence: 0.31

Phoebe
Perplexity: - 8.09
Coherence: 0.33

Joey
Perplexity: - 8.01
Coherence: 0.33

The best model based on perplexity is Full script model. If we compare only characters´ models, then it is Phoebe´s model.
The best model based on coherence is Joey´s and Phoebe´s models.
However, the differences between scores are very small and, thus, it does not tell us much.

## Limitations
- only some of the semantically meaningless words were filtered out from the script. Filtering out more of them could lead to better performance.
- in this script the number of chunks in preprocessing stage: 30, min_count of bigrams: 10 and number of topics in lda model: 15 were set to be identical for each character. Each character would need further investigation and it would make more sense to set individualized metrics.
- the comparison of characters is very basic and shallow. It could have been more informative if chosen different, more advanced methods

## Results summary
Overall, the models perform not too badly but still far from very good. Every character has 1-2 broad topics which are more general and a lot of specific ones, which reflect the characters´ personalities very well. However, it is not always easy to prescribe them to a specific topic category and they tend to overlap. If invested more time in data cleaning and more thoughtful metrics choice, it has a potential to perform pretty well.


