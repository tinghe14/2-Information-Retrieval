Book: **Introduction to information retrieval**.      
Book Source: Available at http://nlp.stanford.edu/IR-book/information-retrieval-book.html

Module 1: Boolean Retrieval
---
Information Retrieval:
- field concerned with the organization, storage, and retrieval of information for text, semistructured data(xml), video images and speech

Three major problems in IR:
- polysemy: words can have multiple meanings
  - ambiguity pervasive
  - distrinctions vary in granularity
- synonymy: the same concept can be expressed using different words
  - English provides no canonical典范的 way to reference people and things
  - speackers of a language learn preferential ways of expressing things
- morphology: many word forms are related and small affixed adjust meaning
  - we like to use a query using the word 'airplane' to mnatch the concept but it won't cover the same meaning words, 'aircraft, planes'.

Boolean Model:
- relevant documents are determined using set operations/set-membership (eg, query = 'rabies AND shot')
  - boolean AND
  - pros:
    - good performance with well-constructred queries
    - representation is space-compact
    - bit-operations are efficient
    - results are transparent
  - cons:
    - if a document contains words more than once, it doesn't matter
    - if a document contains many other words besides the query terms, the model ignores this
    - scores are 0/1 (specificity is low)
    - long queries are hard to construct

Document Representations:
- term-document matrix
  - key data structure: inverted files
    - dictionary with it positing lists which contain a list of documents containing that term and the number of times that term occurs (word A: (doc id A, count A)
    - it is a large binary files, typically 15%-20% the size of the indexed text
    - after all document have been parsed the inverted file is sorted
    - multiple terms entries for a single document are merged and frequency information added
    - the file is commonly split into a dictionary and a posting file

Tokenization
- difficult to identify & normalize words (eg: 'Dr. Peter')
- issues:
  - punctuation
    - sometimes favor keeping interior punctuation
  - case
    - you can reduce to all upper or lower, or preserve first character (fails on McNamee) 
  - numbers
    - throw away or retain some
      - usefull: air florida #90, 1/20/2009, gateway 2000
  - abbreviations
    - I.B.M or IBM
    - keep a list and pick canonical form 
  - contractions and possessives 所有格
    - remove suffix (don't -> do and n't)
    - expand (don't -> do not)
    - leave interior quote marks alone
  - other steps
    - stopword removal
    - simple normalization of word forms: stemming
    
Module 2: Index Construction
---
Terminiology
- indexing term (the sub-atomic particles of documents. In practice, terms are essentially words. however, it can bt stemmed words, multi-word phrases or other strings)
- vocabulary size (the number of unique indexing terms, also called dictionary size)
- corpus (alternative term for document colleciton)
- DOCID (id for each document)
- document frequency (df(term))
- collrection frequency / corpus frequncy (cf(term))
- term count or term frequency (tf(term, docid) for a particular document, the num of times that a given term appears in it)
- dictionary (generally the dictionary is a list of words, their document frequency and a pointer to a postings list)
- posting or postings entry (a tuple that indicates how many times a term apppears in a document such as (doc5, 3))
- inverted file / inverted index (a set of postings lists for terms)
Tokenizaiton
- stopwords
- stemming: transforming related word forms into a common representation, usually by identifying a root form or stem
Tolerant Retrieval
- background
  - indexing terms from documents may not match user query terms, two common reasons
    - lexical variation (building, builder, buildings)
    - misspelling
- wildcard queries
  - mon*: find all docs containing any word begining 'mon'
  - easy with binary tree or B-tree lexicon
  - here we have an enumeration of all terms in the dictionary that match the wild-card query
- spelling correction
  - two main flavors: isolated word (check each word on its own for misspelling)
    - isolated word correction: get a lexicon and a character sequence Q, return the words in the lexicon cloest to Q
      - closes: edit distance(S1,S2, the minimum number of basic operations to convert one to other-insert, delete, replace), weighted edit distance(as before, but the weight of an operation depends on the characters involved), n-gram overlap(enumerate all the n-grams in the query string, threshold by number of matching n-grams)
        - Jaccard coefficient (commonly used measure of overlap)
        - dice coefficient
  - context-sensitive (look at surrounding words)
    - examination of co-occurrence patterns can help from spelling correction
    - soundex: class of heuristics to expand a query into phonetic equivalents
word-based information retrieval
- most traditional information retrieval systems indexed documents according to the words in those documents
- word-based retrieval performs poory when the documents to be retrieved are garbled乱码 or contain spelling mistakes
- character n-gram tokenizaiton can help
  - represent text as overlapping substrings
Index Construction
- minimal memory
  - front-coding (and arrays or B-trees)
  - perfect hash functions
- basic dictionary representations
  - space requirement
    - the space required for the vocabulary is rather small. Heaps' law the vocabulary v, grows as O(t^beta)
    - the occurrences (inverted file) demand much more space. since each word appearing in the text is referenced once in that structure, the space is O(t)
- indexing methods
  - indexing methods
  - dynamic indexes
  
Module 3: Efficiency Issues
---
Zipf's law
- the kth most frequent term has frequency proportional to 1/k
index compressions
- an index requires less pace than a text
- compression method
  - encoding numbers in binary
  - unary coding, etc

Module 4: Vector Space Models
---
relevance
- goal of IR is to retrieve all and only the relevant documents in a collection for a particular user with a particular need for information
  - only documents that share features with the query are relebant (we speak generally of indexing terms)
    - using term frequency
      - repitiion can be rewarded
      - better documents have amore features in common with the query
      - and if a document and the query share no words in common, the document is not relevant
        - inverse document frequency
          - ![IDF](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/IDF.png)
vector-space model
- binary weights are too limitng, use term frequency
- documents and queries are n-dimensional vectors
- documents are ranked against queriese using a vector comparision
  - sample metrics: cosine (most common), inner product, dice
  - cosine
    - ![Cos similarity](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Cos%20Similarity.png)
    - vector representation of query and colelction
    - inner product
    - vector length
    - vector cosine
      - problem
        - term independence: different terms are considered independent/ orthogonal
        - equal importance: like boolean models, the naive VSM treats all words as equally important
          - term weights (most two factors)
            - repitition (term frequency)
            - rarity (schemes like IDF reward rareness; but they do not depend on given document)
            - TF-IDF
            - ![tf-idf](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/TF-IDF.png)

Module 5: Evaluation & Relevance Feedback
---
evaluation of IR performance
- relevance
  - in what ways can a document be relevant to a query
    - answer question precisely or partically
    - sugeest a source for more information
    - give background information
    - remind the user of other knowledge
  - degree of relevance
    - binary: relevant or not
    - on a scale: 0-100
  - evaluation metrics
    - precision/recall
      - can't know true recall value except in small collections
    - another way to evaluate
      - fix the number of documents retrieved at several levels: top 5, top 10, top 20
        - this is a way to focus on how well the system ranks the first k documents
    - there is a tradeoff between precision and recall
      - so measure precision at different levels of recall
        - interpolate
        - ![interpolate1](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Interpolate1.png)
        - ![interpolate2](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Interpolate2.png)
        - ![interpolate3](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Interpolate3.png)
        - average over multiple queries
query refinement
- how to reformulate the query?
  - thesaurus expansion: suggest terms similar to query terms (see car add automobile)
    - instructor note: thesaurus-based query expansion is best with controlled vocabulary search
  - relevance feedback: suggest terms and documents similar to retrieveed documents that have been judged by a user to be relevant
    - rocchio's method
      - ![rocchio](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Rocchio's%20method.png)
  - term re-weighting

Module 6: Advanced Retrieval Model
---
historic probabilistic model
- rigorous formal model attempts to predict the probability that given a document will be relevant to a given query (probability ranking principle, accurate estimates of probabilities)
probabilistic model
- angle between two vectors (how empirical)
- formulation biased towards an interactive process
  - initally posit a set of candidate documents
  - the user will rate initial documents
  - now the system can make a better guess
- probabilistic framework
  - compute odds of relevance for a document
  - binary weights are used
  - in practice, no human feedback is required
    - basic idea
      - for a given query, if we know some documents that are relevant, terms that occur in those documents should be given greater weighting in searching for other relevant documents/ by making assumptions about the distribution of terms and applying Bayes Theorem, it is possible to derive weights theoretically.
statistical language model
      - binary independence model (most simplest)
        - binary = boolean: documents are represented as binary incidence vector of terms
        - indepence: terms occur in documents independently 
          - queries: binary term incidence vector
          - ![BIM](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Binary%20Independence%20M.png)
          - ![BIM2](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Binary%20Independence%20Final%20Model.png)
- statistical language model (what comes next? shut? up? the door?)
  - n-gram language models (n-grams: a sequence of n words (commonly words, not characters))
    - chain rule
      - counting fails
        - this approach doesn;t generalize
          - longer n-grams are likely to be rate and estimates will have higher variance
          - some n-grams will never be seen in training data, we don't want to fail due to these zero counts
          - solution: markov models (sequence of random variables)
            - unigram model (based solely on current word) bigram model(based on pervious word and current word) trigram model (based on prior 2 words and current word)
            - data sparsity (non seen text)
              - add-one/ laplace
              - backoff model
              - other complex alternatives (good-turing, witten-bell, knesar-ney)
           - ![language model](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/language%20models.png)
           - insufficient data
             - a simple idea that works well in practice is to use a mixture between document multinomial and collection distribution
             - ![mixture model](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/Mixture%20model.png) 
             - ![summary](https://github.com/tinghe14/COURSE-2Information-Retrieval/blob/main/Pics%20in%20Note/basic%20mixture%20model%20summary.png)
Module 7: Text Classification
---
Chapter 13 - Text Classification & Naïve Bayes
- before this chapters, this book has mainly discussed the process of as hoc retireval, where users have transient information needs that they try to address by posing one or more queries to a search engine. However, you might have ongoing information needs
  - standing query: a standing query is like any other query except that it is periodically executed on a colleciton to which new documents are incrementally added over time.
  - to caputre the generality and scope of the problem space to which standing queries belong, we now introduce the general notion of a classification problem.
  - classificatin using standing quries is also called routing or filtering.
- rules:
  - classification by the use of standing quries, which can be thought of as rules, most commonly wrriten by hand
    - example: 'multicore computer chips' can be set rules as '(multicore OR multi-core) AND (chip OR processor OR microprocessor)'
  - a rule caputres a certain combination of kwyworrds that indeicates class.
  - hand-coded rules have good scaling propoerties, but creating and maintaining them over time is labor intensive,
  - apart from manual classification and hand-crafed rules, there is a third approach to text classification, namely, machine learning-based text classficatin.
- statisitcal text classification:
  - labeling: the process of of annotating each document with its class

Chapter 14 - Vector Space Classification
Chapter 15 - Support Vector Machines & Machine Learning on Documents
Module 8: Multilingual IR
---
Module 9: Web Search Part 1
---
Module 10: Web Search Part 2
---
Module 11: Distrbuted Processing & Multimedia Processing
---
Module 12: NLP and IR
---
Module 13: Exam
---
Module 14: Class Projects
---
