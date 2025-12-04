# LING 430 Final Project
This repository contains the narrative discourse data, coherence scores, and scripts for the LING 430 (Computational Linguistics) final project. The project aims to utilize computational linguistic techniques (i.e., microlinguistic and macrolinguistic feature derivation) and simple machine learning to predict coherence scores for narrative discourse transcripts in a manner that correlates with human assessments.

### Project Structure
This project uses transcripts from the HANNA and CoheSentia corpuses as samples of narrative discourse. These datasets collectively contain around 1500 human or large-language model generated stories, each approximately a paragraph long, and which have been scored by human raters for global or holistic coherence on a 1 - 5 scale. This repository contains notebooks for cleaning the raw narrative discourse data (referred to as transcripts), processing and formatting them in a variety of ways for feature analysis, and calculating a set of linguistic features for each transcript. Finally, it constructs a random forest classifier to attempt to classify test transcripts into coherence scores using the equivalent scale. In doing so, it aims to determine whether the given feature set is appropriate for automated assessment of narrative discourse coherence that can reflect the decisions of human scorers.

### Features
# TODO: update the features like this
A total of ***24*** features were selected as relevant for the classification analysis on the assumption that they are related to judgments of coherence and should thus be accurate predictors of scores. ***explain why 24 - 10 features per smallest class, minus the outlier 1 class***. The features and any corresponding theoretical justifications are listed below.
- *Number of Words*: total number of words in a transcript. Longer transcripts may be more difficult to understand, while very short transcripts may not be sufficient to produce a coherent narrative.
- *Part-of-Speech Proportions*: number of words tagged as a particular part of speech (pronouns, coordinating conjunctions, subordinating conjunctions) divided by total number of words. Both the proportion of pronouns and of conjunctions (coordinating and subordinating) have been related to comprehension difficulty (Graesser et al., 2004), which is thought to influence the perceived coherence of a text. Proportion code is based on an English linguistic feature pipeline developed by ***Pugalenthi, 2025***
- *Open-Closed Class Ratio*: ratio of number of open-class words (nouns, verbs, adjectives, and adverbs) to number of closed-class words (adpositions, auxiliaries, coordinating and subordinating conjunctions, determiners, interjections, numerals, particles, and pronouns). A higher open-closed class ratio indicates a greater proportion of content-carrying words compared to grammatical indicators, which may affect relevance and thus coherence (Maimon & Tsarfaty, 2025). Open-closed class ratio code is based on an English linguistic feature pipeline (***Pugalenthi, 2025***)
- *Type-Token Ratio*: number of unique words divided by total number of words. ***finish this***
- *Propositional Density*: number of words introducing or carrying ideas (adjectives, adverbs, adpositions, coordinating and subordinating conjunctions, verbs) divided by total number of words ***finish this***
- *Number of Logical Operators*: total number of logical operators (and, or, not, if...then) in a transcript. A higher count of logical operators correlates with greater analytical density and cognitive demand (Graesser et al., 2004), which may influence perceptions of coherence
- *Word Frequency Mean*: **finish this!!!** The values for word frequency were acquired from ***???***; the word frequency mean code is based on a pre-existing linguistic feature pipeline (***Pugalenthi, 2025***)
- *Semantic Diversity*: quantifies the number of contexts a word can appear in, averaged across all words in a transcript. Words with a higher semantic diversity can be ***used in more distinct contexts***, which might ***challenge processing and affect coherence***. The values for semantic diversity were acquired from Hoffman et al., 2012; the semantic diversity code is based on a pre-existing linguistic feature pipeline (***Pugalenthi, 2025***)
- *Semantic Thematic Similarity*: the average cosine similarity between each pair of words in a transcript; quantifies the degree to which a narrative contains words that are similar to one another, or have high co-occurrence ***citation***. Narratives with lower semantic thematic similarity provide more diverse information ***citation***, but may appear less coherent. Semantic thematic similarity code is based on a pre-existing English linguistic feature pipeline (***Pugalenthi, 2025***) using word2vec embeddings ***citation***
- *Surprisal*: degree to which a word is unexpected based on prior words, averaged across all words in a transcript. Surprisal code is based on a pre-existing English linguistic feature pipeline (***Pugalenthi, 2025***) using the GPT2 model from minicons ***citation***
- *Local Co-Reference Cohesion*: a quantification of the proportion of adjacent utterance pairs in a text that share a common noun (noun co-reference). The formula for local cohesion is ***finish this!!!*** (Graesser et al., 2004). Cohesion has been identified as a necessary feature for coherence (Maimon & Tsarfaty, 2025)
- *Global Co-Reference Cohesion*: a quantification of the proportion of all utterance pairs in a text that share a common noun. The formula for global coherence is ***finish this!!!*** (Graesser et al., 2004); this metric is correlated with local cohesion, but provides a more holistic measure of noun co-reference
- *Constituent Proportion*: number of high-level or sentence-level constituents (defined as a noun phrase, verb phrase, subordinate clause, or prepositional phrase) divided by total number of words. ***related to syntactic complexity, which is assumed to affect coherence ratings because why wouldn't it*** (Graesser et al., 2004) 
- *Mean Noun Phrase Length*: the average length of noun phrases in a transcript, quantifying the number of modifiers and therefore complexity of the phrase. Noun phrase length has been related to syntactic complexity (Graesser et al., 2004), which ***should affect coherence***
- *Mean Verb Phrase Length*: the average length of verb phrases in a transcript, quantifying the complexity of the phrase. As in noun phrases, verb phrase length is related to syntactic complexity (Graesser et al., 2004), which is thought to impact coherence
- *Number of Utterances*: total number of utterances in a transcript ***finish this***
- *Mean Words per Utterance*: mean number of words per utterance in a transcript ***finish this***
- *Local coherence*: **derived from Hoffman code** Local coherence has been used as an automated measure of retell coherence (**hoffman citation**), so it is expected to be correlated with human ratings
- *Dependency Distance Mean*: the distance between a word and its head word (***https://arxiv.org/pdf/2301.02057***), averaged across all words in a transcript. Transcripts with a higher dependency distance have ***more distance between words and their head words***, which may ***lower coherence/higher cognitive demand***
- *Adjacent Dependency Relation Mean*: 
- *First Order Coherence*: 
- *Second Order Coherence*: 

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
    This notebook uses the final feature data to run and fit a random forest classifier, the performance of which is then analyzed for various metrics. An explanation of the model performance and potential areas of improvement is included

### Dependencies

TODO - maybe add examples for the linguistic features?

### Citations
# TODO: CITE KESHA'S CODE

hoffman code: [text](https://osf.io/8atfn/overview) -> need to explain how coherence was calculated
frequency: https://www.ugent.be/pp/experimentele-psychologie/en/research/documents/subtlexus/brysbaertnew.pdf
semantic diversity: https://link.springer.com/article/10.3758/s13428-012-0278-x
surprisal: https://pypi.org/project/surprisal/
cite word2vec! google model
minicon: https://pypi.org/project/minicons/
textdescriptives: https://arxiv.org/abs/2301.02057
benepar: https://pypi.org/project/benepar/
(https://aclanthology.org/2025.naacl-long.277.pdf)