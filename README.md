# PageRank Algorithm Implementation and Analysis

## 1. Introduction
This project focuses on the implementation and analysis of the PageRank algorithm and its optimized variant, the Block - Stripe algorithm. It aims to provide a comprehensive understanding of these algorithms and their performance on a specific dataset.

## 2. Algorithm Details
### 2.1 PageRank Algorithm
- **Principle**: PageRank, proposed by Larry Page of Google, is a crucial algorithm for ranking web pages in search engine results. It assesses the importance of web pages based on their link relationships. The core idea is that a page linked by more other pages is generally more important, and the weight is calculated iteratively.
- **Steps**:
  - **Initialization**: Given a set of N web pages, each page's PageRank value is initialized to $1/N$.
  - **Iterative Calculation**: Repeatedly calculate new PageRank values for each page until convergence. The formula for calculating the new PageRank value of page $i$ is $PR(i)=\frac{(1 - d)}{N}+d\sum(\frac{PR(j)}{L(j)})$, where $j$ refers to all pages linking to $i$, $L(j)$ is the number of outgoing links from page $j$, and $d$ is the damping factor (usually 0.85). After calculation, the PageRank values of each page are updated.
  - **Convergence**: The algorithm stops when all PageRank values reach a stable state.
  - **Special Handling**: Deals with circular links and pages without outgoing links (hanging nodes) by introducing damping factors and evenly distributing the PageRank values of hanging nodes.

### 2.2 Block - Stripe Algorithm
- **Principle**: This is an optimization algorithm designed to accelerate the PageRank calculation. In traditional PageRank calculations, iterating over the entire graph can be computationally expensive for large graphs. The Block - Stripe algorithm divides the graph into multiple blocks, performs iterative calculations on each block, and then combines the results, reducing computational complexity.
- **Steps**:
  - The graph is divided into multiple blocks, each containing a subset of nodes and corresponding edges.
  - Independent iterative PageRank calculations are performed on each block to update the PageRank values of each node.
  - The PageRank values of each block are combined to obtain the final PageRank value for the entire graph.

## 3. Dataset Description
The dataset used in this project is in the form of a text file (data.txt). Each line in the file represents an edge in the graph, with the format <FromNodeID, ToNodeID>. The dataset may contain duplicate data, which is treated as a single edge during the experiment. For hanging nodes (nodes without outgoing degrees) and circular links (node loops), a random jump mechanism is introduced.

## 4. Project Implementation
### 4.1 Basic PageRank Algorithm
- **Main Function**: Comprises three main processes: data processing and loading, PageRank algorithm implementation, and result saving.
- **Data Loading**: Opens the dataset file, reads each line, parses the source and target nodes, adds them to a list, obtains a unique list of nodes, initializes a graph object, prints the total and unique number of links, and finds the maximum node number to return the graph object.
- **Iterative PageRank Calculation**:
  - **Preprocessing**: Calculates the number of unique nodes in the graph and initializes the PageRank matrix.
  - **Iterative Calculation**: Calculates new PageRank values for each node according to the formula and adjusts to ensure the sum of PageRank values is 1.
  - **Stopping Criteria**: Calculates the maximum error in each iteration. If the error is less than a predefined threshold (EPSILON) or the maximum number of iterations (MAX_ITER) is reached, the iteration stops.
  - **Output Results**: Stores the calculated PageRank values in a dictionary and returns it.
- **Output Top 100**: Sorts the results according to the PageRank score and saves the top 100 to a specified file.

### 4.2 Block - Stripe Algorithm
- **Data Preprocessing**: Performs operations such as node mapping and numbering rearrangement. This includes adjusting the data structure (using 2D arrays or sparse matrices to represent edge relationships), optimizing calculations (making node relationships easier to map to different processing units or threads), and reducing processing complexity (simplifying node traversal without considering the original node numbering order).
- **Data Blocking**: Divides the processed data into blocks. When the number of target nodes in a block reaches a specified size (block_size), the block data is saved to disk, and the next block is processed. Intermediate results are saved for future use.
- **Iterative PageRank Calculation**:
  - Calculates the number of blocks, initializes node PageRank values, and iteratively calculates until convergence.
  - Calculates the error in each iteration and decides whether to continue based on the error.
  - Saves the calculated results.
- **Output Top 100**: Sorts the results according to the PageRank score, maps the nodeIDs back to the original ones, and saves the output to a file.

## 5. Experimental Results and Analysis
### 5.1 Basic PageRank Results
The results show the ranking, node ID, and PageRank value of the top 100 nodes with the highest PageRank scores.
### 5.2 Block - Stripe Results
Similar to the basic PageRank results, the ranking, node ID, and PageRank value of the top 100 nodes are presented.
### 5.3 Analysis
- **Result Comparison**: The overall ranking trends of the two algorithms are similar, but there are some differences in the PageRank rankings of the top 100 nodes. This may be due to the more efficient use of memory and computational resources and better handling of sparse matrices by the Block - Stripe algorithm for large - scale data.
- **Algorithm Efficiency**: The Block - Stripe algorithm may have higher computational efficiency and scalability compared to the basic PageRank algorithm, especially for large - scale data. It reduces memory and computational resource consumption by blocking data, thereby increasing the calculation speed.

## 6. Conclusion
This project successfully implements the PageRank and Block - Stripe algorithms. It provides a deep understanding of the algorithms' principles and implementation details, as well as mastering relevant optimization methods and calculation techniques. It also demonstrates how parameter adjustments can affect the algorithm results. The two algorithms show consistent overall trends but with some minor differences.
