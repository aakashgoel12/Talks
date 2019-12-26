
![SegmentLocal](images/step0/intro.png "segment")

# Text Similarity
****

How much two strings are similar ?

![SegmentLocal](images/step0/whatDoYouMean.gif "segment")

How humans usually defines how similar are two strings ?
Two strings can be similar in many ways:

    1) Word level
        A) Try to capture inflectious form of string (multiple ways of writing)
           Example:[1]
               i) Singular/Plural: course and courses
              ii) Tense: take and took
             iii) Contractions: aren't and are not
              iv) Expansions: TCS and Tata Consultancy Services
               v) Typo Mistake: poetry and peotry  
              vi) Canonical forms: MBA and M.B.A, B.Tech and BTech
             vii) Replacement words/emojis: @ and at, u and you, happy and :)
            viii) Is a type relation/ Synonyms: Color (red, green, orange)  
            
    2) Multiple word (Phrase) level
        i) Different way of writing (usually multiple words):
            --> Segmentation: Newyork and New york
            --> Location of word: GTB Nagar, Delhi == Delhi, GTB Nagar OR Delhi meetup == Meetup delhi
            --> Missing of word: Hindustan private limited == Hindustan limited
            --> Missing of word with inflection: Hindustan private limited == Hindustan ltd.
            
    3) Sentence Level
        i) Lexical similarity: Number of common words matter instead of meaning of sentence
            Example:[2]
                PASS
                    S1 = My name is Aakash Goel.
                    S2 = Aakash Goel is my name.
                ---------------------------------
                PASS BY CHANCE
                    S1 = A girl is styling her hair.
                    S2 = A girl is brushing her hair.

                    S1 = One woman is measuring another woman's ankle.
                    S2 = A woman measures another woman's ankle.
                ---------------------------------
                FAIL
                    S1 = How are you ?
                    S2 = How old are you ?
                    
                    S1 = record the play
                    S2 = play the record
       ii) Semantic similarity: Actual meaning of sentence matters instead of common words
           Example:[3]
               S1 = The weather is cold today.
               S2 = It is freezing today. 

![SegmentLocal](images/step0/semantic.png "segment")

## STEP I: Setting up Problem
****

Lets set some **background** first:

User browsing through some Question Answering website like Quora, StackOverflow and it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question.[4]

**IDEA:** Can we identify question pairs that have the same intent? 

Doing so will make it easier to find high quality answers to questions resulting in an improved experience for Quora writers, seekers, and readers.

From **Modelling Propective**,
    
    GOAL: Predict whether given two questions are similar or not

## STEP II:Getting Data
****
Kaggle organized competition "Quora Question Pairs" (https://www.kaggle.com/c/quora-question-pairs/data)

Also, using **embeddings** like word2vec (https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit), GLOVE (https://nlp.stanford.edu/projects/glove/), FastText (https://fasttext.cc/docs/en/english-vectors.html)

**Other Datasets**: 
- https://nlp.stanford.edu/projects/snli/
- http://alt.qcri.org/semeval2017/task3/

![SegmentLocal](images/step2/data1.png "segment")

![SegmentLocal](images/step2/data1_1.png "segment")

## STEP III: Clean and Prepare data
All Ideas regarding feature engineering:
****

![SegmentLocal](images/step3/eda1.png "segment")

**Feature Engineering** [6]

**Basic** Features
- Number of coomon words in question 1 and question 2
- Number of characters and words in question 1 and question 2
- Number of character without spaces
- Difference in length of question 1 and question 2

**Fuzzy Wuzzy** Features
- Token Sort, Token Set, Partial token set, Partial token sort, levenshtein, QRatio, WRatio

**Word2Vec** Features
![SegmentLocal](images/step3/wordvec1.png "segment")
- cosine distance
- word mover distance (WMD) uses the **word embeddings** of the words in two texts to measure the **minimum distance** that the words in one text need
to **travel in semantic space** to reach the words in the other text.[5]
![SegmentLocal](images/step3/wmd.png "segment")


![SegmentLocal](images/step3/import1.png "segment")

**Get vector of sentence from word vector** [5,7,8,]
- Average of all the word vectors in a sentence, It ignores the order of words and sentence semantics
- Average of Word2Vec vectors with TF-IDF, It again loses word order within the sentence
- Doc2Vec: Train your dataset using Doc2Vec and then use the sentence vectors
- Pre-trained sentence encoders
    - Google's Universal Sentence Encoder: Encodes text into high dimensional vectors that can be used for text classification, semantic similarity, clustering and other natural language tasks [9,10]
    - Facebook's Infersent: One of architecture it uses is Bi-LSTM with max/mean pooling [11,12]
      ![SegmentLocal](images/step3/infersent.jpg "segment")

![SegmentLocal](images/step3/feature1.png "segment")


![SegmentLocal](images/step3/feature1_1.png "segment")
![SegmentLocal](images/step3/feature1_2.png "segment")

## Step IV: Building  Model 

![SegmentLocal](images/step4/model.png "segment")
Above image used for reference purpose only as it good snapshot of pipieline [14] 

Below are common steps across deep learning based model:
- Preprocessing data
    - Tokenizer, Pad Sequences
    - Prepare Embedding layer
![SegmentLocal](images/step4/common_steps1.png "segment")
![SegmentLocal](images/step4/common_steps2.png "segment")
- Development of model architecture
- Model fit
- check model result and robustness

**Approach 1**: CNN - Version1

![SegmentLocal](images/step4/tech1.png "segment")
![SegmentLocal](images/step4/tech1_result.png "segment")

**Approach 2**: CNN - Version2 [15]

![SegmentLocal](images/step4/tech2.png "segment")
![SegmentLocal](images/step4/tech2_1.png "segment")
![SegmentLocal](images/step4/tech2_2.png "segment")
![SegmentLocal](images/step4/tech2_3.png "segment")
![SegmentLocal](images/step4/tech2_result.png "segment")

**Approach 3**: CNN + LSTM 

![SegmentLocal](images/step4/tech3.png "segment")
![SegmentLocal](images/step4/tech3_1.png "segment")
![SegmentLocal](images/step4/tech3_2.png "segment")
![SegmentLocal](images/step4/tech3_result.png "segment")

References
****
1) http://www.cse.iitd.ac.in/~mausam/courses/csl772/autumn2014/lectures/03-morph.pdf

2) https://medium.com/@adriensieg/text-similarities-da019229c894

3) https://ai.googleblog.com/2018/05/advances-in-semantic-textual-similarity.html

4) https://www.kaggle.com/c/quora-question-pairs

5) https://medium.com/@adriensieg/text-similarities-da019229c894

6) https://www.youtube.com/watch?v=vA1V8A69e9c

7) https://stackoverflow.com/questions/29760935/how-to-get-vector-for-a-sentence-from-the-word2vec-of-tokens-in-sentence

8) https://medium.com/explorations-in-language-and-learning/how-to-obtain-sentence-vectors-2a6d88bd3c8b

9) https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/46808.pdf

10) https://www.nishanpantha.com.np/programming/universal-sentence-encoder-semantic-search.html

11) https://arxiv.org/pdf/1705.02364.pdf

12) https://medium.com/analytics-vidhya/sentence-embeddings-facebooks-infersent-6ac4a9fc2001

13) https://paperswithcode.com/task/semantic-textual-similarity

14) https://mc.ai/identifying-duplicate-questions-part-1%E2%80%8A-%E2%80%8Aproblem-description-data-processing/

15) https://www.kaggle.com/rethfro/1d-cnn-single-model-score-0-14-0-16-or-0-23
