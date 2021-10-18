---
layout: post
title:  "Fun with Natural Language Processing (NLP) - Part 1"
date:   2021-10-19 07:45:54 +0200
categories: nlp
---

When Apple introduced Siri about 10 years ago I was excited to be able to talk in natural language with a
computer system. It reminded me of TV series of the 80’s, like Knight Rider, Whiz Kids and Riptide. In Knight Rider,
you could talk with the car in natural language, ask questions, and if it did not know the answer immediately, it said
it would search database XY and come up with the answer a few seconds and cryptic character progressions on its screen
later. Now if I look at Siri and its competitors ten years later, then I am a little disappointed on the progress that
its „intelligence“ has made. A current TV ad praises a new feature, that you can ask the „virtual intelligence“ Alexa
what sound a certain animal makes, and then Alexa produces the animals sound (works also on Siri btw). But if you look
at that feature, and try out its capabilities by experiment (my kids did extensive research on that), it seems like
this feature is implemented pretty straight forward, without much kind of „intelligence“ on the way (only for 
recognizing the spoken human language).

When I lately read on the website of a company called [**AI21 labs**](https://www.ai21.com) about natural language
processing (NLP) and that it is a problem that demands for all kinds
of AI strategies and algorithms (not just DNNs or CNNs), I was reminded to my approaches that I did in that direction
starting in my childhood at age of about 11 or 12, of course inspired by these 80’s TV series. Back then, I wanted to
implement a „friend“ that I could teach with natural language (written via keyboard) and that would learn what I told
him and store it in a database, to be able to answer questions of me later. Over the years, I started several small
attempts on that in BASIC, Turbo Pascal, C, and C++. With all the progress being made in the past years and libraries
being available (like e.g. NLTK), I got interested now to give it another try, not to implement a better Siri, but more
to find out, where the hard challenges still are that prevent breakthrough progress in that domain.

So, the goal I try to achieve now is to

- build up a knowledge base by processing natural language texts (texts written to be understood/processed by humans,
  like e.g. articles in Wikipedia or on news-websites) or from textual conversation (pseudo messenger
  communication interface)
- answer questions by processing/evaluating/searching the knowledge base including reasoning

# Part 1: Learning from Real Simple Sentences
I start easy by trying to gather knowledge from real simple sentences (that I call RSS), that are of the kind:

```
<subject> <predicate> <object>
```

Even to this seemingly simple sentences, there are quite some challenges:
- subject and objects can have definite and indefinite articles in front
- there can be count words before subjects and objects
- subjects and objects can be in singular or plural
- different verbs can express the same or similar semantic meaning
- verb phrases can have further words for decoration

In this first example, I try to gather information from the following sentences, overcoming
the challenges I mentioned above:

```Python
sentences = [
  "The dog or domestic dog (Canis familiaris) is a domesticated descendant of the grey wolf, characterized by an upturning tail.",
  "A car has four wheels.",
  "A car has a steering.",
  "Dogs are animals.",
  "A dog is an animal.",
  "A dog is a pet",
  "A horse is an animal.",
  "A dog strays down the street slowly.",
  "A car is a vehicle.",
  "Trucks are vehicles.",
  "Bicycles are vehicles.",
  "A Cessna is a plane.",
  "A duo consists of two persons",
  "A trio consists of three persons.",
  "A bread is made of wheat flour.",
  "A bread is made of salt.",
  "Humans consist of water.",
  "Humans have blood.",
  "A human has a head.",
  "A human has 2 legs.",
  "Humans have two arms.",
  "A human head has two eyes.",
  "Human heads have two ears.",
  "The car has a manual transmission.",
  "The dog is characterized by an upturning tail."
]
```


And this is the resulting knowledge database I get with my Python code, as a Python dictionary:
```Python
{'things': {
'car': {'aggregates': [[4, 'wheel'], 'steering', 'transmission'], 'specializes': ['vehicle']},
'wheel': {'is part of': ['car']},
'steering': {'is part of': ['car']},
'animal': {'generalizes': ['dog', 'horse']},
'dog': {'specializes': ['animal', 'pet'], 'aggregates': ['tail']},
'pet': {'generalizes': ['dog']},
'horse': {'specializes': ['animal']},
'vehicle': {'generalizes': ['car', 'truck', 'bicycle']},
'truck': {'specializes': ['vehicle']},
'bicycle': {'specializes': ['vehicle']},
'plane': {'generalizes': ['Cessna']},
'Cessna': {'specializes': ['plane']},
'duo': {'aggregates': [[2, 'person']]},
'person': {'is part of': ['duo', 'trio']},
'trio': {'aggregates': [[3, 'person']]},
'bread': {'aggregates': ['wheat flour', 'salt']},
'wheat flour': {'is part of': ['bread']},
'salt': {'is part of': ['bread']},
'human': {'aggregates': ['water', 'blood', 'head', [2, 'leg'], [2, 'arm']]},
'water': {'is part of': ['human']},
'blood': {'is part of': ['human']},
'head': {'is part of': ['human'], 'aggregates': [[2, 'eye']]},
'leg': {'is part of': ['human']},
'arm': {'is part of': ['human']},
'eye': {'is part of': ['head']},
'Human head': {'aggregates': [[2, 'ear']]},
'ear': {'is part of': ['Human head']},
'transmission': {'is part of': ['car']},
'tail': {'is part of': ['dog']}
}}
```

This is the Source Code of my example, that led to the results:

[SmartVirtualFriend Repo - learnSentence.py Example (click here)](https://github.com/DrMarkusVoss/SmartVirtualFriend/blob/main/playground/learnFromSentences/learnSentence.py)

Now this simple example is already much more powerful than my childhood approaches, where I did know nothing yet 
about regular expressions and parsing theory. Also, there were no powerful libraries available, like the
NLTK that I used here.

Here is a chapter of an NLTK book that gives useful information, an overview and details on a processing chain
for natural languages:

[NLTK book chapter 7](https://www.nltk.org/book/ch07.html)

I use a **very simple grammar** for a **regular expression parser** of the NLTK library. The grammar aims basically at trying to identify "noun phrases" (NP) and "verb phrases" (VP). Then 
finally a real simple sentence (RSS) has the pattern: NP VP NP, where the first NP represents the
subject, the 2nd NP the object.

Now with this simple example quite some knowledge can be read in and stored, as you could see from the results
above. But you also already see quite some challenges:
- Not all sentences lead to new knowledge in the database, as some of them were too complex for my simple
  grammar and therefore not understood. The allowed grammar for the sentences that could be "understood" is very simple.
  Finding a grammar that covers all possible "human language" sentences, even if only in one language like english, is 
  difficult. You have to go beyond regular expressions.
- The more complex the grammars get, the more **ambiguity** they may or do contain (trying to cover human language). So
  you won't get one result, but more than one possible interpretation of the role of each word in the
  sentence. See the following chapter 8.1 of an NLTK book for details:
  [NLTK book chapter 8](https://www.nltk.org/book/ch08.html)

- **Not only sentences can be ambiguous, but also words can be.** E.g. a word like "manual" can be an adjective to a noun,
  like in "manual transmission", or it can be a noun itself where "manual" is a "guideline" or "user's guide". See in 
  the example knowledge base, where "wheat flour", "manual transmission" and "Human head" have been handled 
  differently. Especially the "human" before "head" has been classified different by the parser in both example
  sentences and therefore been handled different when filling the knowledge base.
- One important tool to handle ambiguity is **"context"**. **Knowing and understanding the context helps you to 
  eliminate wrong interpretations.** This will be a major topic for the future.
- Filling the knowledge base: In this example, the results of the parser are handled by my Python code
  and another classification step is done in Python. Depending on that the results are inserted into
  the knowledge base. It would be possible to also let that classification step be handled by the grammar and parser,
  in a way that all "logic" is captured by that grammar. See here an example for that: ...nltk chapter 10.
  Both approaches have advantages and disadvantages. This will be discussed in combination with 
  the next point in future again.
- What could you learn from a sentence like "A dog strays down the street slowly."? It could be a sentence as an 
  introduction of a journalistic article about e.g. slums. Would you learn that "dogs stray"? Or just ignore it 
  completely? How do you separate things that are "worth learning" from the "decoration stuff"?
- The representation of the knowledge itself (like in a dictionary in the example) is a quite huge challenge
  itself. From the current example we can derive the following:
  - How do you store knowledge about "combined nouns", like e.g. "manual transmission" or "wheat flour"? Do you only
    store the main noun like "transmission" or "wheat", or do you store the combined noun, or do you somehow
    store the "attribute" to the main noun as attribute? This questions will be explored in upcoming examples.
  - How do you store information about the "knowledge source"? In a growing knowledge base using information from
    different sources, you might later want to classify a source of information as "false", and remove all the
    knowledge that you got from that source (e.g. a dedicated Wikipedia page or new article). Now, how would you 
    annotate the "learned knowledge" with the information source? Putting it to every element and relation might blow
    up the database with a lot of additional data. This will also be investigated in further 
    examples.
  - How do you deal with different kinds of "truth" statements. In the examples there were a lot of fundamental
    statements, like e.g. "A dog is an animal.". But how do you deal with a statement like "Stella is the small,
    brown dog under the table."?
  - What is the "language" or meta model of the knowledge database? What semantics does it have? In my simple example I use so far
    bits of UML (Unified Modelling Language).
  - Should "information doubling" be avoided or appreciated? In the current example, a statement from one sentence
    gets encoded into the database often 2 times. Partly it cannot be avoided, partly it can. Should it? Currently I
    prefer the approach to double information in the knowledge base, in order to have a clearer "object" related
    structure. But you could also work with references. But do references really bring a benefit when 
    learning from different information sources? Is "keeping the size of the database small" an optimization 
    target worth to follow? Or is "easy to search" the target?
  - What would be a good implementation technology for a continuous growing knowledge base? A classical relational
    database? A file-based approach? Use GUIDs, hash tables? Keeping everything in RAM and in between doing a 
    serialization of the data structure to a file would most likely be not sufficient, I guess?

Stay tuned for further investigations...

Enjoy,

Markus
