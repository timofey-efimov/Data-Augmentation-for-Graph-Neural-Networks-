# Data-Augmentation-for-Graph-Neural-Networks-

This is repository for the code, which augments the dataset for graph neural networks.
Right now the code works for topology-based classification problems. 

This code is for the final project for [ELEC573: Network Science and Analytics](http://networkscience.rice.edu/), offered at Rice University




 <font size="5s"> Click on the image to see video of the project presentation: </font>
 <br>
[ <img src="https://i.ibb.co/ZSzZnqK/2022-12-12-11.png" alt="drawing" height="300"/>](https://www.youtube.com/watch?v=4yZ9ck3_f88)

## Project Authors: 

[Timofey Efimov](https://github.com/timofey-efimov), [Robbie Kenworthy](https://github.com/mahoganu)

<!-- ABOUT THE PROJECT -->
## About The Project


Data augmentation is a common technique used in machine learning to increase the size and diversity of a dataset. However, it can be more complicated to perform data augmentation on graph datasets, as graph neural networks operate on non-Euclidean structures. In this paper, we propose a data augmentation model that uses graphons to generate new graphs and Gromov-Wasserstein distance to measure the similarity between the original and newly generated graphs. This approach allows us to augment our graph dataset in a way that preserves the structure and relationships within the data.


 

### Data Description

[Dataset Link](https://snap.stanford.edu/data/reddit_threads.html)

The dataset we selected was on that contained approximately 200,000 Reddit threads,
and we distinguished whether these threads were discussion-based or not. The structure of these
graphs is based on replies to the initial post. Discussion posts will often have much longer chains of
comments, as people reply to others in the form of a dialog between them while posts that are not
will be much more centralized around the initial post. These distinctive structures allow for a much
easier graph classification problem, that also enables us to gain insight into the effectiveness of our
graph sampling technique.

The binary classification can be represented as follows:

 <font size="5s"> Input for the binary graph classification problem </font>
 <br>
 <img src="https://i.ibb.co/FV3wpR6/binary1.png" alt="drawing" width="300"/>


<font size="5s"> Result of binary graph classification </font>
 <br>
 <img src="https://i.ibb.co/S0f5CX6/binary2.png" alt="drawing" width="300"/>


 <font size="5s"> Example of the graph from Reddit Dataset: </font>
 <br>
 <img src="https://i.ibb.co/6tPdrQ4/10nodes.png" alt="drawing" width="300"/>


<font size="5s"> Example of newly generated graph of 10 times bigger, similar to previous one in structure: </font>
 <br>
 <img src="https://i.ibb.co/Jqmrj79/100nodes.png" alt="drawing" width="300"/>

### Graph Neural Network


<font size="5s"> Neural Network Structure: </font>
 <br>
 <img src="https://i.ibb.co/qNStXct/NNarch.png" alt="drawing" width="500"/>
 
To provide context, this structure defines feature dimensionality at each iteration, it's not entire graph neural network architecture
Each layer is graph convolutional layer with a trainable skip connection.


### Algorithm Description

The main idea behind this data augmentation technique is separate a small
group of graphs from the original dataset, and for each of the graphs
in the group infer a graphon. Then, by linear combination with equal weights
find the "average" graphon for this group. In our case, we defined group
as all graphs with the same number of nodes.

Once the group graphon is found, we need to sample graphs of 3 times previous
number of nodes size. Number of samples is a variable that can be tuned
in the code. Among these samples using Gromov-Wasserstein distances
we can find the samples that are closest to the stochastic block
model that represents the "average" graphon.

More mathematical and precise algorithm description is below:

 <img src="https://i.ibb.co/Xz2tgDX/Algorithm1.png" alt="drawing" width="500"/>


 <br>
 <img src="https://i.ibb.co/JC6s3Hg/Algorithm2.png" alt="drawing" width="500"/>


It is important to note that for graphon inference adjacency matrices
are sorted by node degrees so that it would be possible to meaningfully
combine inferred graphons(align them). The example of the
graphon, inferred from 1000 nodes, 600 preferentially attached node
Barabasi-Albert graphon is below:

<img src="https://i.ibb.co/PgLx6S8/barabasi.png" alt="drawing" width="300"/>


### Built With

<!-- * [![py][Python]][Python-url]
* [![sp][Spacy]][Spacy-url] -->

 ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
