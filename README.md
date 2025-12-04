# LING 430 Final Project
This repository contains the narrative discourse data, coherence scores, and scripts for the LING 430 (Computational Linguistics) final project. The project aims to utilize computational linguistic techniques (i.e., microlinguistic and macrolinguistic feature derivation) and simple machine learning to predict coherence scores for narrative discourse transcripts in a manner that correlates with human assessments.

### Project Structure
This project uses transcripts from the HANNA and CoheSentia corpuses as samples of narrative discourse. These datasets collectively contain around 1500 human or large-language model generated stories, each approximately a paragraph long, and which have been scored by human raters for global or holistic coherence on a 1 - 5 scale. This repository contains notebooks for cleaning the raw narrative discourse data (referred to as transcripts), processing and formatting them in a variety of ways for feature analysis, and calculating a set of linguistic features for each transcript. Finally, it constructs a random forest classifier to attempt to classify test transcripts into coherence scores using the equivalent scale. In doing so, it aims to determine whether the given feature set is appropriate for automated assessment of narrative discourse coherence that can reflect the decisions of human scorers.

### Features
# TODO: update the features like this
A total of 24 features were selected as relevant for the classification analysis on the assumption that they are related to judgments of coherence and should thus be accurate predictors of scores. ***explain why 24 - 10 features per smallest class, minus the outlier 1 class***. The features and any corresponding theoretical justifications are listed below.
- *Number of Words*: total number of words in a transcript.
- *Part-of-Speech Proportions*: number of words tagged as a particular part of speech (pronouns, coordinating conjunctions, subordinating conjunctions) divided by total number of words. Both the proportion of pronouns and of conjunctions (coordinating and subordinating) have been related to comprehension difficulty (Graesser et al., 2004), which is thought to influence the perceived coherence of a text
- *Open-Closed Class Ratio*: ratio of number of open-class words (nouns, verbs, adjectives, and adverbs) to number of closed-class words (adpositions, auxiliaries, coordinating and subordinating conjunctions, determiners, interjections, numerals, particles, and pronouns)
- *Type-Token Ratio*: number of unique words divided by total number of words
- *Propositional Density*: number of words introducing or carrying ideas (adjectives, adverbs, adpositions, coordinating and subordinating conjunctions, verbs) divided by total number of words
- *Number of Logical Operators*: total number of logical operators (and, or, not, if...then) in a transcript
- *Word Frequency Mean*: **finish this!!!**
- *Semantic Diversity*: **finish this**
    - Semantic diversity data was acquired from **finish this!!!**
- *Semantic Thematic Distance*: **finish this**
- *Surprisal*: degree to which a word is unexpected based on prior words, averaged across all words in a transcript
- *Local Cohesion*: 
- *Global Cohesion*:
- *Constituent Proportion*:
- *Mean Noun Phrase Length*:
- *Mean Verb Phrase Length*:
- *Number of Utterances*: total number of utterances in a transcript
- *Mean Words per Utterance*: mean number of words per utterance in a transcript
- *Local coherence*: **derived from Hoffman code**
- dependency_distance_mean	prop_adjacent_dependency_relation_mean	first_order_coherence	second_order_coherence

### Order of Data Processing
1. [transcript_preprocessing.ipynb](transcript_preprocessing.ipynb)  
    This notebook preprocesses the transcripts from [HANNA](/raw_data/hanna_stories_annotations.csv) and [CoheSentia](/raw_data/cohesentia_stories_1.json) to produce [a file](/processed_data/transcripts.csv) of cleaned and truncated transcripts
2. [transcript_formatting.ipynb](transcript_formatting.ipynb)  
    This notebook takes the cleaned but unformatted transcripts from the step above, and produces [several files](/processed_data) of transcripts reformatted with various conventions (corrected punctuation, no punctuation, segmented by utterance boundaries based on punctuation, or single-word segmentation for local coherence)
3. [linguistic_feature_calculation.ipynb](linguistic_feature_calculation.ipynb)  
    This notebook calculates a large set of [linguistic features](/linguistic_features), including the 24 used in classification, given the processed and formatted transcript files
4. [feature_processing.ipynb](feature_processing.ipynb)  
    This notebook takes the multiple files containing feature data produced by the prior step, cleans, and z-scores the data to produce an [output file](/linguistic_features/linguistic_feature_set.csv) with the 24 normalized classification features
5. [classification.ipynb](classification.ipynb)
    This notebook uses the final feature data to run and fit a random forest classifier, the performance of which is then analyzed for various metrics. An explanation of the model performance and potential areas of improvement is included.

### Dependencies


hoffman code: [text](https://osf.io/8atfn/overview) -> need to explain how coherence was calculated
frequency: https://www.ugent.be/pp/experimentele-psychologie/en/research/documents/subtlexus/brysbaertnew.pdf
semantic diversity: https://link.springer.com/article/10.3758/s13428-012-0278-x
surprisal: https://pypi.org/project/surprisal/
cite word2vec! google model
minicon: https://pypi.org/project/minicons/
textdescriptives: https://arxiv.org/abs/2301.02057
benepar: https://pypi.org/project/benepar/

# Features (file:///Users/emicatx/Downloads/BF03195564.pdf):

TODO - maybe add examples for the linguistic features?

### Citations
# TODO: CITE KESHA'S CODE