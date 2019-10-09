# Using-Social-Network-to-Predict-the-Success-of-Novels

## Introduction

Successful novels have similar conversational network patterns, which are different from the patterns in less successful novels.

Conversational networks extracted from novels can be used as features to predict the success of the novels using machine learning methods such as SVM.

## Literature survey

Automatic attribution of quoted speech in literary narrative. Elson and McKeown. 2010 [1]
The paper has assembled a corpus of more than 3,000 quotations, whose speakers (if any) are manually identiﬁed, from a collection of 19th and 20th century literature by six authors. We are going to use this corpus as one of the 2 input data for our project.

Extracting Social Networks from Literary Fiction. Elson, Dames and McKeown. 2010 [2]
The paper presents a method for extracting social networks from literature, namely, nineteenth-century British novels and serials. derive the networks from dialogue interactions, and thus its method depends on the ability to determine when two characters are in conversation. Its approach involves character name chunking, quoted speech attribution and conversation detection given the set of quotes. Features are extracted from the social networks and examine their correlation with one another, as well as with metadata such as the novel’s setting.

Success with Style: Using Writing Style to Predict the Success of Novels. Ashok, Feng and Choi. 2013 [3]
The paper gives a method to predict the success of literary works, which is a curious question among publishers and aspiring writers alike. It examines the quantitative connection, if any, between writing style and successful literature. Our project, depending on the the idea from the second paper, “Extracting Social Networks from Literary Fiction” to achieve the goal of the third paper, predicting the success of novels. The main purpose of the project is to examine the quantitative connection between social network from literary fiction and its success. We also use dataset from this paper as the second one of the 2 input data for our project.

## Dataset

{1} We are going to use dataset of the paper “ Success with Style: Using Writing Style 
 to Predict the Success of Novels.”    http://www.cs.stonybrook.edu/~songfeng/success/data/novels.7z

{2} We use dataset from the paper “Automatic Attribution of Quoted Speech in Literary Narrative” for Quoted Speech Attribution step. (Note: We need to get the dataset from the paper’s author which hasn’t been done yet.)

## Methodology (Algorithm & machine learning techniques)

Implement a tool to extract conversational network features [2]
Character Identification
Process each novel with the Stanford NER tagger and extract noun phrases that were categorized as persons or organizations
Cluster the noun phrases into coreferents for the same entity. (Note: This step is not very clear to us now. Looks like in the paper, they do part of the work manually. If so, we need to find another method to do this step.)

Quoted Speech Attribution [1][2] (using dataset {2} for training)
Preprocessing: Identify all named entities and nominals that appear in the passage of text preceding the quote in question. These replace certain spans of text with symbols, and clean or normalize other parts.
Classification. Classify the quote into one of a set of syntactic categories. This serves to cluster together scenarios where the syntax strongly implies a particular solution.
Learning. Extract feature vector from the passage and send it to a trained model specific to its syntactic category. The model predicts the probability that each candidate is a speaker, then attributes the quote to the top candidate.

Constructing conversational networks [2]
Assign vertices to character entities that are mentioned repeatedly throughout the novel. Coreferents for the same name were grouped into the same vertex
Filter out the entities that are mentioned fewer than 3 times in the novel or are responsible for less than 1% of the named entity mentions in the novel
Assign undirected edge between vertices that represent adjacency in quoted speech fragments. Set the weight of each undirected edge between two character vertices to the total length, in words, of all quotes.
normalize each edge’s weight by the length of the novel

Feature Extraction [2]
Extract features from the conversational networks, including:
The number of characters
The number of speaking characters
The variance of the distribution of quoted speech
The number of quotes
The proportion of words in the novel that are quoted speech
The number of n-cliques in the network (e.g. 3-cliques, 4-cliques and so on)
The average degree of the graph
Average degree normalized by the number of characters

Apply the feature extraction tool from step 1 to training dataset (dataset {1} which is used in [3])
Train SVM classifier using the results from step 2.
Apply the feature extraction tool from step 1 to test dataset (dataset {1} which is used in [3])
Using trained SVM classifier from step 3 to predict the success of novels.
Evaluation and Analysis.

## Baselines

We are going to use 2 alternate methods for purposes of a baseline:
We will use POS feature to compute the baseline for each genre of novel

We ask 3 annotators to independently read the quotations from each novel and decide whether the novel is successful or not.

References
<pre>
[1] David K.Elson, Kathleen R.McKeownAutomatic. “Automatic Attribution of Quoted Speech in Literary Narrative”. In Proceedings of the Twenty-Fourth AAAI Conference on Artificial Intelligence (AAAI 2010), Atlanta, Georgia.
[2] David K.Elson, Nicholas Dames, Kathleen R.McKeown. “Extracting social networks from literary fiction”. In ACL '10 Proceedings of the 48th Annual Meeting of the Association for Computational Linguistics Pages 138-147
[3] Peter T. Davis, David K. Elson, and Judith L. Klavans. ”Methods for precise named entity matching in digital collections”. In Proceedings of the Third ACM/IEEE Joint Conference on Digital Libraries (JCDL ’03), Houston, Texas.
[4] Vikas Ganjigunte Ashok Song Feng Yejin Choi. “Success with Style: Using Writing Style to Predict the Success of Novels”
</pre>
