# Search System Basics

> Understanding Search Systems
>
> Reference: [Book] Elasticsearch Practical Guide

<br>

<br>

## 1. Understanding Search Systems

<br>

### 1-1. What is a Search System?

: Search services are referred to by names such as `search engine`, `search system`, and `search service`

- **Search Engine**
  - A program that collects information from the Web and provides search results
  - The implementation varies depending on the characteristics of the data provided as search results
- **Search System**
  - A general term for systems built on `search engines` to provide **reliable** search results based on large-scale data
  - **Collects** vast amounts of data using a `crawler`,
    - **Indexes** it using multiple `search engines`,
    - And provides search results through a `UI`
  - According to internal **policies**, documents with high **relevance** can be **placed at the top** of search results,
    - And **accuracy** of search can be improved by assigning **weights** to specific `fields` or `documents`

- **Search Service**
  - Provides search results as a service using a `search system` built on `search engines`

```
Search Service > Search System > Search Engine
```

<br>

<br>

### 1-2. Components of a Search System

: A search system consists of a **crawler** that **collects** information, **storage** that **stores** collected data, an **indexer** that **transforms** collected data into a form suitable for searching, and a **searcher** that **finds** matching documents from indexed data.

<br>

#### Crawler

- A program needed for websites, blogs, cafes, etc.
- Also called `crawler`, `spider`, `worms`, `web robot`, etc.
- Most information on the web including files, databases, web pages are collection targets
- For files, the `crawler` collects and **stores** information such as file name, file content, file path, then the `search engine` **searches** the stored information and answers user queries

<br>

#### Storage

- The physical storage where data is stored in the database
- The search engine stores **indexed** data in storage

<br>

#### Indexer

- To find information matching user queries in the information collected by the search engine, the collected data must be **processed** into a `searchable structure` and **stored**, and the `indexer` performs this role
- The indexer uses various **morphological analyzers** to **extract** `meaningful terms` from information and stores data in an **inverted index structure** favorable for searching

<br>

#### Searcher

- Receives user queries and **finds matching documents** from the inverted index structure stored by the indexer, returning them as results
- Whether a query and document match is determined by **similarity-based** search ranking algorithms
- Like the indexer, the searcher also uses **morphological analyzers** to extract meaningful terms from user queries for searching
  - Therefore, search quality varies depending on the morphological analyzer used!

<br><br>

### 1-3. Differences from Relational Databases

- Search engines and relational databases (RDBMS) share many similarities in that they both find and provide data matching queries to users
- However, there are many problems with providing search functionality using relational databases

<br>

#### Relational Database

- A database is a collection of data that integrates and manages data
  - Broadly divided into **relational** or **hierarchical** databases based on storage methods
- All data is **deduplicated** and **structured** as **structured data** stored in tables consisting of rows and columns
- Searching for desired information is possible using SQL statements, but only simple search through text matching is possible
  - That is, transforming text into multiple words or searching using multiple synonyms or similar words is not possible

<br>

#### Search Engine

- Search engines can **index** and **search** unstructured data that databases cannot handle
- **Natural language processing** is possible through **morphological analysis**, and fast search speed is guaranteed based on **inverted index structures**

<br>

#### Comparison of Key Concepts: Elasticsearch vs RDBMS

| Elasticsearch  | Relational Database |
| -------------- | ------------------- |
| Index          | Database            |
| Shard          | Partition           |
| Type           | Table               |
| Document       | Row                 |
| Field          | Column              |
| Mapping        | Schema              |
| Query DSL      | SQL                 |

<br>

<br>

## 2. Search Systems and Elasticsearch

- Nowadays, **NoSQL (No Structured Query Language)** is widely used for fast searching of large-scale data
- Elasticsearch can also be **classified** as a type of NoSQL, enabling near **real-time fast searching** through **distributed processing**
- It can search `large-scale unstructured data` that is difficult to handle with traditional databases, and supports both **full text search** and **structured search**
- Although it is fundamentally a search engine, Elasticsearch can also be utilized as a **large-scale storage** like `MongoDB` or `Hbase`

<br>

### 2-1. Why Elasticsearch is Powerful

<br>

#### 1. Open Source Search Engine

- Elasticsearch is an `open source` search engine developed based on Apache Foundation's Lucene
  - Therefore, it is used by countless people worldwide, and bugs are mostly resolved quickly when they occur

<br>

#### 2. Full Text Search

- Most databases like `PostgreSQL` and `MongoDB` only provide basic **text search functionality** due to limitations in basic query and indexing structures
  - However, Elasticsearch enables more advanced **full text search**
- **Full text search** means indexing entire contents to search for documents containing `specific terms`
  - Traditional RDBMS is not suitable for full text search, but Elasticsearch can search quickly by combining various feature-specific and language-specific plugins

<br>

#### 3. Statistical Analysis

- Unstructured log data can be collected and aggregated in one place for **statistical analysis**
- By integrating Elasticsearch with Kibana, you can **visualize** and **analyze** logs accumulating in **real-time**

<br>

#### 4. Schemaless

- Databases store and manage data by **transforming** it into a **conforming format** according to a **schema** structure
  - In contrast, Elasticsearch can automatically **index** and **search** **various forms of non-standardized documents**

<br>

#### 5. RESTful API

- Elasticsearch supports **HTTP-based RESTful API** and uses `JSON format` for both requests and responses, making it available on different platforms regardless of development language, OS, or system

<br>

#### 6. Multi-tenancy

- Even if indexes are different, as long as the `field names` to search are the same, **multiple indexes can be queried at once**
  - This can be used to provide multi-tenancy functionality

<br>

#### 7. Document-Oriented

- Multiple layers of data can be stored in an index as **structured documents** in `JSON format`
- **Hierarchical** documents can also be **easily queried with a single query**

<br>

#### 8. Inverted Index

- As a Lucene-based search engine, it supports inverted indexing
  - Here, an inverted index is a special data structure similar to the index page at the back of a paper book
- If you need to find all documents containing the term "search engine," normally you would have to read every document from beginning to end to get the desired results
  - However, with an inverted index structure, finding the **term** reveals the **location of documents containing that term**, enabling fast retrieval

<br>

#### 9. Scalability and Availability

- If Elasticsearch is **distributed** and **scaled**, it can process large volumes of documents more efficiently
- In a distributed environment, data is divided into small units called `shards`, and the **number of shards can be adjusted** each time an `index` is created
  - This allows **distributing** data based on its **type** and **characteristics** for fast processing

<br>

<br>

### 2-2. Weaknesses of Elasticsearch

1. It is **not "real-time"**
   - Generally, indexed data becomes searchable only after about 1 second
   - Indexed data goes through complex internal processes like `commit` and `flush`, so it is not real-time
     - Strictly speaking, it can be called Near Realtime
2. Does not provide **Transaction** and **rollback** functionality
   - Elasticsearch is fundamentally configured as a `distributed system`
   - Since it does not support rollback and transaction, which are **costly** for the overall cluster performance improvement, there is a risk of **data loss** in the worst case
3. Does not provide data **update**
   - Strictly speaking, when an update command is requested, Elasticsearch **deletes** the existing document and **creates a new document** with the changed content
     - For this reason, it incurs relatively higher costs compared to simple updates
       - However, this is not a major disadvantage because it can leverage the benefit of **immutability**!
