<p align="center">
    <a href="https://getvectorai.com">
        <img src="https://getvectorai.com/assets/logo-with-text.png" width="400"></img>
    </a>
</p>
<h3 align="center">
Vector AI is a framework designed to make the process of building production grade vector based applications as quickly and easily as possible. Create, store, manipulate, search and analyse vectors alongside json documents to power applications such as neural search, recommendations, personalisation, etc.
</h3>

- Visit our website at: https://getvectorai.com
- For Python Documentation: https://vector-ai.github.io/vectorai
- For REST API Documentation: https://api.vctr.ai/documentation
- Join our discord: https://discord.gg/CbwUxyD
- For a more gentle introduction comparing our features, read https://getvectorai.com/production-ready-search-in-5-minutes/

Features:
- **Multimedia Data Vectorisation**: Image2Vec, Audio2Vec, etc (Any data can be turned into vectors through machine learning)
- **Document Orientated Store**: Store your vectors alongside documents without having to do a db lookup for metadata about the vectors.
- **Vector Similarity Search**: Enable searching of vectors and rich multimedia with vector similarity search. The backbone of many popular A.I use cases like reverse image search, recommendations, personalisation, etc.
- **Hybrid Search**: There are scenarios where vector search is not as effective as traditional search, e.g. searching for skus. Vector AI lets you combine vector search with all the features of traditional search such as filtering, fuzzy search, keyword matching to create an even more powerful search.
- **Multi-Model Weighted Search**: Our Vector search is highly customisable and you can peform searches with multiple vectors from multiple models and give them different weightings.
- **Vector Operations**: Flexible search with out of the box operations on vectors. e.g. mean, median, sum, etc.
- **Aggregation**: All the traditional aggregation you'd expect. e.g. group by mean, pivot tables, etc
- **Clustering**: Interpret your vectors and data by allocating them to buckets and get statistics about these different buckets based on data you provide.
- **Vector Analytics**: Get better understanding of your vectors by using out-of-the-box practical vector analytics, giving you better understanding of the quality of your vectors.

## Quick Terminologies

- Models/Encoders (aka. Embedders) ~ Turns data into vectors e.g. Word2Vec turns words into vector
- Vector Similarity Search (aka. Nearest Neighbor Search, Distance Search)
- Collection (aka. Index, Table) ~ a collection is made up of multiple documents
- Documents (aka. Json, Item, Dictionary, Row) ~ a document can contain vectors, text and links to videos/images/audio.

## QuickStart

Install via pip! Compatible with any OS.

```
pip install vectorai
```

Check out our quickstart notebook on how to make a text/image/audio search engine in 5 minutes: [quickstart.ipynb](examples/quickstart.ipynb)

```
from vectorai import ViClient, request_api_key

api_key = request_api_key(username=<username>, email=<email>, description=<description>, referral_code="github_referred")

vi_client = ViClient(username=username, api_key=api_key)

from vectorai.models.deployed import ViText2Vec
text_encoder = ViText2Vec(username, api_key)

documents = [
    {
        '_id': 0,
        'color': 'red'
    },
    {
        '_id': 1,
        'color': 'blue'
    }
]

# Insert the data
vi_client.insert_documents('test-collection', documents, models={'color': text_encoder.encode})

# Search the data
vi_client.search('test-collection', text_encoder.encode('maroon'), 'color_vector_', page_size=2)

# Get Recommendations
vi_client.search_by_id('test-collection', '1', 'color_vector_', page_size=2)
```

## Access Powerful Vector Analytics 

Vector AI has powerful visualisations to allow you to analyse your vectors as easily as possible - in 1 line of code.

```
vi_client.plot_dimensionality_reduced_vectors(documents, 
    point_label='title', 
    dim_reduction_field='_dr_ivis', 
    cluster_field='centroid_title', cluster_label='centroid_title')

```

![View Dimensionality-Reduced Vectors](https://getvectorai.com/assets/gif/dr_example.gif)

```
vi_client.plot_1d_cosine_similarity(
    documents, 
    vector_fields='use_vector_',
    label='name', 
    anchor_document=documents[0])
```

Compare vectors and their search performance on your documents easily!
![1D plot cosine simlarity](https://getvectorai.com/assets/gif/1d_cosine_similarity.gif)

## Why Vector AI compared to other Nearest Neighbor implementations?

- **Production Ready**: Our API is fully managed and can scale to power hundreds of millions of searches a day. Even at millions of searches it is blazing fast through edge caching, GPU utilisation and software optimisation so you never have to worry about scaling your infrastructure as your use case scales.
- **Simple to use. Quick to get started.**: One of our core design principles is that we focus on how people can get started on using Vector AI as quickly as possible, whilst ensuring there is still a tonne of functionality and customisability options.
- **Richer understanding of your vectors and their properties**: Our library is designed to allow people to do more than just obtain nearest neighbors, but to actually experiment, analyse, interpret and improve on them the moment the data added to the index.
- **Store vector data with ease**: The document-orientated nature for Vector AI allows users to label, filter search and understand their vectors as much as possible.
- **Real time access to data**: Vector AI data is accessible in real time, as soon as the data is inserted it is searchable straight away. No need to wait hours to build an index.
- **Framework agnostic**: We are never going to force a specific framework on Vector AI. If you have a framework of choice, you can use it - as long as your documents are JSON-serializable! 

## Bring your own Model or Vector

You can bring your own model or vectors and enjoy all the rich vector functionality that Vector AI provides.

### Schema Rules for documents (BYO Vectors and IDs)

Ensure that any vector fields contain a '\_vector\_' in its name and that any ID fields have the name '\_id'.

For example:
```
example_item = {
    '_id': 'James',
    'skills_vector_': [0.123, 0.456, 0.789, 0.987, 0.654, 0.321]
}
```

The following will not be recognised as ID columns or vector columns.

```
example_item = {
    'name_id': 'James',
    'skillsvector_': [0.123, 0.456, 0.789, 0.987, 0.654, 0.321]
}
```

## Building Products with Vector AI
Creating a multi-language AI fashion assistant: https://fashionfiesta.me | [Blog](https://getvectorai.com/how-we-built-a-vector-powered-outfit-recommender/)

![Demo](https://getvectorai.com/assets/gif/fashion-fiesta-demo.gif)

Do share with us any blogs or websites you create with Vector AI!
