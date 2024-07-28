# Decision Trees
## A decision tree algorithm coded from scratch
#### FurtherAI_DecisionTrees.ipynb contains the implementation of the algorithm, with explanations at each step of the way.
#### Trees are created for weather data toy dataset (weather-data.csv) and Covid-19 data (covid-data.csv)

## Algorithm explanation and results
I decided to implement the **ID3 algorithm**, using the ‘Learn-Decision-Tree’ pseudocode from Russell and Norvig, 2021 (p678). I used Pandas DataFrames as the main data structure as this offers a powerful way to manipulate columns within a dataset. The algorithm uses the ‘find_next_split’ function to find the best node to split the remaining data on. This is based on which node (feature) provides the highest information gain, which is calculated using the weighted entropies of all the values of the node. Whichever node is found to be best to split the data on is then added to the tree, and the various subtrees are explored in the same way, stopping when the data is pure or when the maximum depth of the tree is reached. If the tree reaches the maximum depth it makes a prediction based on the majority class of the values left in the remaining data.

The dataset I chose to explore looks at Covid presence in May 2020 among Indian people (Symptoms and COVID Presence (May 2020 data), n.d.). There are 5,434 entries and 21 variables including symptoms and what I will call, contact questions, with binary values depicting whether the variable is true for the respective person. The variable ‘Covid-19’ gives a binary value as to whether the person had Covid or not, and is the obvious response variable, so that is what I aim to predict with my classifier. I split the data 80/20 training/test sets. With this split, I achieved an accuracy of 0.95 on the test data with a maximum tree depth of 5. The baseline accuracy is 81% as this is the accuracy a classifier would achieve for just predicting the majority class every time. This shows that is a good classifier. I compared accuracies for maximum tree depths between 1 and 9 and found that as I increased the maximum tree depth, the accuracy improved considerably (by ~20%). This makes sense, as the more questions you ask, the more information you can gain to get a better sense of what the decision should be. There is a difficult trade-off between the interpretability of the decision tree and classification accuracy.

The tree with a depth of 3 (shown in figure below) first asks whether the person has travelled abroad. This is a strong first node because it has a pure outcome for “Yes”. It predicts positive for Covid, as all the participants who had travelled abroad had Covid. This perhaps suggests that there is a slight bias in the data, or that there is not enough data, as although there may have been a lot of Covid brought back to India from people travelling, it does not seem plausible that everyone who travelled abroad would have got Covid. Thus, it is important to recognise that it is just a small sample and is not necessarily indicative of the population. If the answer to “travel abroad” is “No” then it asks a series of health questions to gather information. Only 2 of the 5 leaf nodes for this 3 deep tree are pure, and 2 are only confident to between 65-70%. This is low considering the baseline accuracy of 81%. This shows that a depth of 3 is clearly not enough as it leaves some branches lacking enough information to make a confident decision. Another problem with this tree is that on one of the branches, answering the same question: “Attended Large Gathering”? with both “Yes” and “No” leads to the same leaf node: “Yes”. The algorithm has chosen to ask this question because it will have a strong value for information gain because “Attended Large Gathering” = “Yes” is pure, but as it is the last branch anyway it is superfluous. Despite these issues, the 3 deep tree achieves an accuracy of 92%, only 3% lower than the tree with a depth of 5.

<figure>
<img src="Diagram of 3 deep tree.png" alt="Decision tree used to predict Covid-19" height="500">
    <figcaption>Decision tree used to predict Covid-19. Depth 3 tree shown for brevity. At each leaf node the purity is shown based on the training data.</figcaption>
</figure>

## Bibliography

Russell, S. and Norvig, P., 2021. Artificial Intelligence: a Modern Approach, EBook, Global
Edition: A Modern Approach [Online]. Harlow, UNITED KINGDOM: Pearson
Education, Limited. Available from:
http://ebookcentral.proquest.com/lib/bath/detail.action?docID=5495854 [Accessed
24 August 2021].

Symptoms and COVID Presence (May 2020 data), n.d. [Online]. Available from:
https://kaggle.com/hemanthhari/symptoms-and-covid-presence [Accessed 28
February 2022].
