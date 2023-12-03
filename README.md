# Unconference: Hybrid Search
Hybrid Search Learning

## Standard (keyword) search
Standard search, also known as keyword-based search, is the traditional method of retrieving information from a database or the internet. It relies on the use of keywords or phrases provided by the user to match and retrieve relevant documents or web pages. Standard search relies on keywords provided by users. It begins with indexing, creating a catalog of keywords for each document. When users enter a query, the search engine compares it to the indexed keywords, ranks matching documents based on relevance, and displays results for users to click and access the relevant content. While efficient for specific queries, standard search may struggle with ambiguous or context-dependent searches.  

Standard Search uses ranking function to estimate the relevance of a document to a given search query. Most commonly used relevancy algorith within search engines is Okapi BM25 (where BM stands for Best Matching)

Docs: https://opensearch.org/docs/latest/search-plugins/keyword-search/

[0-standard-serach.http](requests%2F0-standard-serach.http)  
[1-standard-serach-explain.http](requests%2F1-standard-serach-explain.http)

## Semantic Search
Semantic search goes beyond keyword matching to understand the context and meaning of a user's query. Rather than relying solely on exact keyword matches, semantic search considers the intent behind the words.  

Semantic search begins by understanding user queries, recognizing entities, and exploring broader concepts beyond exact keywords. It then analyzes contextual relationships and user intent, ultimately ranking results based on contextual relevance for more accurate and context-aware information retrieval.  

In order to perform semantic search data need to be converted to a vector embeddings which allows search engine to find neares neighbours with the data to a vector which represents meaning of user query,

Docs: https://opensearch.org/docs/latest/search-plugins/neural-search-tutorial/

[2-semantic-serach.http](requests%2F2-semantic-serach.http)  
[3-semantic-serach-explain.http](requests%2F3-semantic-serach-explain.http)

## Hybrid Search
Hybrid search combines both standard and semantic searches together getting best from both.  

Docs: https://opensearch.org/docs/latest/search-plugins/hybrid-search/

[6-hybrid-serach-basic.http](requests%2F6-hybrid-serach-basic.http)  
[7-hybrid-serach-basic-explain.http](requests%2F7-hybrid-serach-basic-explain.http)

