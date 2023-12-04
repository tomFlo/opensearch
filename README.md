# Hybrid Search
Hybrid Search Learning

## Project preparation
VS Code: create file under [.vscode](.vscode) directory with below content
```json
{
    "rest-client.environmentVariables": {
        "dev": {
            "host": "https://opensearch",
            "token": "token"
        }
    }
}
```

IntellJ IDEA: create http-client.private.env.json file in [requests](requests) directory with content
```json
{
  "dev": {
    "host": "https://opensearch",
    "token": "token"
  }
}
```

## Standard (keyword) search
Standard search, also known as keyword-based search, is the traditional method of retrieving information from a database or the internet. It relies on the use of keywords or phrases provided by the user to match and retrieve relevant documents or web pages. Standard search relies on keywords provided by users. It begins with indexing, creating a catalog of keywords for each document. When users enter a query, the search engine compares it to the indexed keywords, ranks matching documents based on relevance, and displays results for users to click and access the relevant content. While efficient for specific queries, standard search may struggle with ambiguous or context-dependent searches.  

Standard Search uses ranking function to estimate the relevance of a document to a given search query. Most commonly used relevancy algorith within search engines is Okapi BM25 (where BM stands for Best Matching)

Docs: https://opensearch.org/docs/latest/search-plugins/keyword-search/

[0-standard-serach.http](requests%2F0-standard-serach.http)  
[1-standard-serach-explain.http](requests%2F1-standard-serach-explain.http)

## Semantic Search
Semantic search goes beyond keyword matching to understand the context and meaning of a user's query. Rather than relying solely on exact keyword matches, semantic search considers the intent behind the words.  

Semantic search begins by understanding user queries, recognizing entities, and exploring broader concepts beyond exact keywords. It then analyzes contextual relationships and user intent, ultimately ranking results based on contextual relevance for more accurate and context-aware information retrieval.  

In order to perform semantic search data need to be converted to a vector embeddings which allows search engine to find nearest neighbours within the data to a vector which represents meaning of user query.

Vector embeddings can be created using one of multiple available pretrained NLP [models](https://www.sbert.net/docs/pretrained_models.html). In our case we will be using [multi-qa-mpnet-base-dot-v1](multi-qa-mpnet-base-dot-v1). 

Example
```text
"Certified natural gas took off in North America in 2021-2022, where will it go next?"
[0.028437773, 0.015929455, 0.042184412, 0.023656057, 0.03258522, ... , -0.0006613471]
```

Docs: https://opensearch.org/docs/latest/search-plugins/neural-search-tutorial/

[2-semantic-serach.http](requests%2F2-semantic-serach.http)  
[3-semantic-serach-explain.http](requests%2F3-semantic-serach-explain.http)

## Semantic Search with Chunked data
NLP models have their limitations like number of tokens which they can take on input and number of dimensions.  

Max number of input tokens limits the model from perspective of length of which the model would be able to transform into vector. In case of our model it's 512 tokens which means approximately 500 words. 

Number of dimensions describes length of a single vector embedding for a processed text and it describes how accurate particular model will be. More dimensions means more accurate but as well slower in calculation of vector and finding nearest neighbours. 

One of additional strategies for better accuracy of semantic search is data chunking. This strategy requires preprocessing of data and dividing it multiple chunks which fit to chosen model input.                  

[4-semantic-serach-chunks.http](requests%2F4-semantic-serach-chunks.http)    
[5-semantic-serach-chunks-explain.http](requests%2F5-semantic-serach-chunks-explain.http)

## Hybrid Search
Hybrid search combines both standard and semantic searches together getting best from both.  

Main problem in combining standard search and semantic search in out query is different algorithm used to calculate relevancy score. K-NN method returns relevancy score in scale from 0 to 1 when Standards search (BM25) returns it in scale from 0 to Max.Integer. This leads in some cases to keeping semantic results on back of the list.  


[6-hybrid-serach-basic.http](requests%2F6-hybrid-serach-basic.http)  
[7-hybrid-serach-basic-explain.http](requests%2F7-hybrid-serach-basic-explain.http)

## Hybrid Search: Hybrid Query
OpenSearch 2.11 introduced a new type of query: hybrid search. It allows to create post-processing normalization pipeline which takes relevancy scoring from different algorithms and bring them to common scale.

Docs: https://opensearch.org/docs/latest/search-plugins/hybrid-search/

[8-hybrid-serach.http](requests%2F8-hybrid-serach.http)  
[9-hybrid-serach-explain.http](requests%2F9-hybrid-serach-explain.http)

