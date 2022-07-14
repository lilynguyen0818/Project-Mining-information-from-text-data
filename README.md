# Project: Mining information from text data

This project is an application of machine learning into finding similar items or sets of text data adopting different approaches including Jaccard similarities, MinHash and Local sensitive hashing (LSH) vectorized version. In practice, these techniques can be employed for the service such as plaragiasm check by comparing the subject texts with the texts of similar contents in the database.

The three techniques are employed for the comparison of their accuracy in finding similar items and the disadvantage of such technique in exchange for better accuracy.

Three tasks are developed to find out about the trade-off between the accuracy and the time to implement the codes of each technique.

## Description of the dataset

The dataset stores the information of a published artice such as the content of the article abstract, authors/editors of the article, time of publishment, address, publisher of the article and url to the article. All the information is presented in the bib form.

After parsing the dataset and transforming it into a dataframe, we can see that the data has 74430 entries and 20 features equivalent to 11.4 MB memory.

As the requirement of the first task is to randomly choose 1000 abstracts for testing to avoid system overloading, we need to preprocess the abstract column, for example, removing the empty abstracts, very short abstracts, and abstracts that are non latin.

The code shows that there are 109 entries with empty abstracts, 57 entries with very short abstracts (less than 200 characters), and 145 entries that are non latin. All those entries are dropped beforing randomly choosing 1000 abstracts.

## Task 1: Finding the similar items

For different k-shingles (3,5, and 10), similarity thresholds (0.1, 0.2, and 0.25), and hashing functions (50, 100 and 200), Jaccard similarities, Minhashing and LSH is adopted to find the abstracts that have similarity in their texts.

For 50 hashing functions, Jaccard similarity approach took the longest time for running. As k_shingles and threshold increases, the number of similar items found decrease. For small k_shingles and low threshold, jaccard similarty approach found more similar pairs than the other approach. Local sensitive hashing approach found the least similar pairs even though operation time for this approach is the most efficient, which shows the trade-off between efficiency and precision.

For 100 and 200 hashing functions, minhashing approach found more similar pairs compared to 50 hahsing functions.

## Task 2: Mining information for the text data

We use the whole anthologies abstract dataset to extract the list of authors and editors per publication, create baskets and perform a search of similar items in those baskets.

Three approaches are employed in this task including naive, A-priori and PCY algorithms for different support thresholds (10, 50, 100) and k-tuples, for k equal to 2, 3, and 4.

As a result, the number of frequent items decreases with the increase of support threshold. All approaches produces the same result. For naive approach, the operation time increases with the increase of the threshold, which is in contrast with the other methods. For low threshold, A priori and hash table took longer time than higher threshold.

When trying to test with different numbers of hashing tables, we notice that the results of items found are the same in different numbers of hashing tables. However, generally, with an increase in the numbers of hashing tables, the opertion time also increases. This can be understood as more tables take up more memories.


With increasing k-tuples, little to no frequent items are to be found. For 3- and 4-tuples, threshold at 10 or lower can help to find more frquent pairs. However, at lower threshold, the operation time is much longer.

## Task 3: Graphs and Social Networks

Unweighted nad weighted networks of the abstracts of similarity are drawn using obtained similar pairs for different threshold. Based on those networks, the communities are identified  and visualized using gephi software.


