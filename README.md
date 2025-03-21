# Qdrant VectorDatabase study notes
---
# [Introduction to Vector database](https://qdrant.tech/articles/what-is-a-vector-database/)

## **What is a Vector Database?**
- A Vector Database is a **specialized system** designed to efficiently handle **high-dimensional vector data**
- A Vector databse uses **indexing, querying and retrieving** to enable advanced analysis and similarity searches.
- A vector database allow us to **understand the context or conceptual similarity of unstructured data** by representing them as vectors
  
## **When to use a vector database?**

- When we have **unstructured data** as our type of data, when the focus of the storage is to **capture the context and semantics**, and/or the use case is to build a **similarity search, recommendation system, RAG or anomaly detection**.

## What is a vector?
- A vector is a **numerical representation** of daa that can **capture the context and semantics** of a textual data
- A vector has: ID, dimensions and payload

## What is a vector ID?
- Is the **unique identifier**, and work as the **primary key in a vector database**. It's essential for associationg the vector with its corresponding "real-world" data (image, text, sound file, etc)

## What is a vector dimensions?
- Is the **core representation of the data**. At the core of every vector **is a set of numbers**, which together form a representation of the data is a **multi-dimensional space**

  ### How thes numbers are generated?
  - These numbers are generated **by embedding models**, such as deep learning algorithms and **capture the essential pattersn or relationships within the data**.
  
## What are collections?
- A collection is essentially a group of vectors (or **points**) that are **logically grouped** together based on **similarity or a specific task**
- Every vector is a collection shares the same dimensionality and can be compared using a single metric

## **What are the types of vectors?**
- **Dense Vectors:** Dense with information, every element in the vector contributes to the **semantic meaning**, **relationships** and **nuances** of the data.

- **Sparse Vectors:** Vectors with no fixed length, but only a few non-zero elements.
Useful for **exact token match** and **collaborative filtering recommendations**.

- **MultiVectors:** Matrices of numbers with fixed length but variable height.
Usually obtained from late interaction models like ColBERT.

## What are distance metrics?
- Are metrics that defines how simialrity between vectors is calculated
  ### Euclidean distance
    - The straight-line path. It's like measuring physical distance between two points in space
  ### Cosine similarity
    - This one is about the angle, not the length. It measures how two vectors point in the same direction. Works well for text or documents.
  ### Dot product
    - Measure how much two vectors align. It's popular in recommendation system

## What is indexing?
  - Is like creating an entry in a traditional database, but vectors need to be indexed in a way taht makes them easy to search later on.
  ### What is HNSW?
  - HNSW (Hierarchical Navigable Small World) is a powerful **indexing algorithm** that most vector databases rely on to **organize vectors for fast and efficient search**
  - It builds a **multi-layered graph**, where **each vector is a node** and **connections represent similarity**. The **higher layers** connect broadly **similar vectors**, while **lower layers** **link vectors** that are **closely related**, making the **searches progressively more refined** as they go deeper
  ### Payload indexing
  - You can configure indexes for both vectors and payloads independently. The payload index is responsible for optimizing filtering based on metadata

## Searching: Approximate Nearest Neighbors (ANN) Search
- Similarity search allows you to search by **meaning**
- WHen the user queries the database, this query is also converted into a vector, the algorithm quickly identifies the area of the graph likely to contain vectors closes to the query vector

## What is vector quantization?
Vector quantization is a technique that reduces the **size in bytes** of vectors. Techniques like **Scalar Quantization** and **Product Quantization** are also popular alternatives when **optimizing vector compression.**



# [Vector embeddings](https://qdrant.tech/articles/what-are-embeddings/)
## What are embeddings?
- Embeddings are **numerical** machine learning **representations** of the **semantic** of the input data. They capture the **meaning of complex**, high-dimensional data, like text, images, or audio, into vectors. Enabling algorithms to process and analyze the data more efficiently.

## What are the main limitations of Word2Vec and GloVe?
- The limitations of Word2Vec and GloVe include **generating a single vector per word**, blending **nuances** into one representation, and relying on **co-occurrence**, which can **lead to biases and limitations** in capturing complex relationships between words.

## What are the advantage of models like BERT and GPT?
- Models like BERT and GPT have the advantage of **capturing complex relationships** between words and their **contexts** through their use of the **transformer architecture and self-attention mechanism**. This allows them to generate **high-quality vector embeddings** that can capture **nuanced differences in word meanings**.

---
# [Hybrid search](https://qdrant.tech/articles/hybrid-search/)
## What's late interaction?
- Late interaction refers to a type of interaction between the tokens of the query and the document that occurs during the search process.
- In the context of ColBERT, late interaction models create a separate embedding for each token of text, and the final score is calculated based on the interaction between the tokens of the query and the document.

## Why use Reciprocal Rank Fusion method instead of reranking?
- It's a more straightforward approach that involves normalizing the scores returned by each method and then calculating a final score using a formula.

---
# [Vector quantization](https://qdrant.tech/articles/what-is-vector-quantization/)
## What's product quantization?
- Product Quantization is a method used to compress high-dimensional vectors by representing them with a smaller set of representative points.
- The process begins by splitting the original high-dimensional vectors into smaller sub-vectors. Each sub-vector represents a segment of the original vector, capturing different characteristics of the data.

## What's binary quantization?
- Significant boost in speed.
- Values greater than zero are converted to 1.
- Values less than or equal to zero are converted to 0.

## What's scalar quantization?
- Transform float32 (4 bytes) values into int8 (1 byte) values


## What's vector quantization?
- Vector quantization is a data compression technique used to reduce the size of high-dimensional data.
- Compressing vectors reduces memory usage while maintaining nearly all of the essential information.
- This method allows for more efficient storage and faster search operations, particularly in large datasets.

---
# [Sparse vectors](https://qdrant.tech/articles/sparse-vectors/)

## What's a sparse vectors?
- A sparse vector is a representation of a document or query where each dimension corresponds to a word or subword, with most values being zero.
- Sparse vectors are useful in domains where many rare keywords or specialized terms are present.

## How sparse vectors improve search systems efficiency?
- Sparse vectors can improve search systems efficiency by reducing the dimensionality of the data and using only the most relevant terms.

## What's term expansion in SPLADE?
- Term expansion is a process where SPLADE expands a query or document to include contextually relevant terms that are not explicitly mentioned.

---
# [Resource optimization](https://qdrant.tech/articles/vector-search-resource-optimization/)

## Explain the 3 key HNSW parameters
- **m** controls the graph's **complexity** and **memory usage**.
- **ef_construct** affects the index building process and its **accuracy**.
- **ef** influences the search **query speed** and **accuracy**.

## What are the benefits of scalar quantization?
- Memory usage will drop: float32 -> int8 (32 / 8 = 4)
- Accuracy loss is minimal

## What are the benefits of binary quantization?
- Efficient similarity calculations: Emulates **Hamming distance** through dot product comparisons, **making it fast and effective**.
- Perfect for high-dimensional vectors: Works well with embedding models like **OpenAI’s text-embedding-ada-002** or **Cohere’s embed-english-v3.0**.

## Which are the methods to manage large vector datasets?
- Multitenancy and sharding

## What's Multitenancy?
- Is a software architecture where multiple independent users (or tenants) share the same resources or environment.

## Why choosing Multitenancy?
- **Logical Isolation:** Ensures **each tenant’s data remains separate** while residing in the same collection.
- **Minimized Overhead**: **Reduces resource consumption** compared to maintaining separate collections for each user.
- **Scalability**: Handles **high user volumes** without compromising performance.

## What's Sharding?
- Sharding is a critical strategy in Qdrant for splitting collections into smaller units, called shards, to efficiently distribute data across multiple nodes.

## Which are the methods to optimize the query?
- Filtering, batch processing, reranking, rescoring, and oversampling,

## Explain Filtering
- Filtering allows you to **select only the required fields** in your query results. By limiting the output size, you can significantly **reduce response time** and **improve performance**.

## Explain Batch Processing
- Batch processing **consolidates multiple operations into a single execution cycle**, **reducing request overhead** and enhancing throughput.
- Instead of inserting vectors individually, group them into **medium-sized batches** to **minimize the number of database requests** and the overhead of frequent writes.

## Explain Hybrid Search
- Hybrid search **combines keyword filtering with vector similarity search**, enabling faster and more precise results.
- Keywords help **narrow down** the dataset quickly, while vector similarity **ensures semantic accuracy**.
- This search method **combines dense and sparse vectors**.

## Explain Oversampling
- Oversampling is a technique that helps **compensate for any precision lost due to quantization**.
- Since quantization simplifies vectors, some relevant matches could be missed in the initial search. To avoid this, you can **retrieve more candidates**, increasing the chances that the **most relevant vectors** make it into the final results.

## Explain Rescoring
- After oversampling to gather more potential matches, **each candidate is re-evaluated based on additional criteria** to ensure **higher accuracy** and **relevance** to the query.
- The rescoring process **maps the quantized vectors to their corresponding original vectors**, allowing you to consider factors like **context, metadata, or additional relevance** that wasn’t included in the initial search, leading to more accurate results.

## Explain Reranking
- Reranking adjusts the **order of search results** based on additional criteria, ensuring the **most relevant results are prioritized**.
- This method is about taking the results from **different search methods** and **reordering** them based on **some additional processing** using the content of the documents, not just the scores

## Which are the storage methods?
- InMemory and Memmap

## Explain InMemory Storage
- **How it works**: **All data is stored in RAM**, providing the **fastest access times** for queries and operations.
- **When to use it**: This setup is ideal for applications **where performance is critical**, and your RAM capacity can accommodate all data.
- **Advantages**: **Maximum speed** for queries and updates.
- **Limitations**: RAM usage can become a **bottleneck** as your **dataset grows**.


## Explain Memmap Storage
- **How it works**: Instead of loading all data into memory, **memmap storage maps data files directly to a virtual address space on disk**. The system’s page cache handles data access, making it highly efficient.
- **When to use it**: Perfect for **storing large collections** that **exceed your available RAM** while still maintaining near in-memory performance when enough RAM is available.
- **Advantages**: **Balances performance and memory usage**, allowing you to work with **datasets larger** than your physical RAM.
- **Limitations**: **Slightly slower than pure in-memory storage** but significantly more scalable.


---
# [Optimizing memory](https://qdrant.tech/articles/indexing-optimization/)

- **Disable HNSW for dense vectors**: Set **m to 0** to prevent building the HNSW graph for incoming vectors, **reducing unnecessary memory and CPU usage**.
- **Store vector data on disk immediately**: Use on_disk: true to store vector data on disk right from the start, **reducing memory usage and making bulk ingestion more efficient**.
- **Enable on-disk storage for indexes**: Store indexes on disk to **reduce memory usage and prevent out-of-memory errors**.
- **Use scalar quantization**: Compress vectors to **reduce memory usage** and preserve performance advantages of RAM-based search.
- **Adjust indexing threshold**: Set a **positive threshold** to delay indexing and **batch more vectors at once**, potentially using more RAM at the moment of index build, but fewer builds overall.


