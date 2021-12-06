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
    
Module 2: Index Construction
---
Module 3: Efficiency Issues
---
Module 4: Vector Space Modules
---
Module 5: Evaluation & Relevance Feedback
---
Module 6: Advanced Retrieval Model
---
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
