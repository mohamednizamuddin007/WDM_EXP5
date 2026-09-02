### EX5 Information Retrieval Using Boolean Model in Python
## NAME : MOHAMED NIZAMUDDIN A
## REG NO: 212224040194

### AIM: To implement Information Retrieval Using Boolean Model in Python.
### Description:
<div align = "justify">
The Boolean model in Information Retrieval (IR) is a fundamental model used for searching and retrieving information from a collection of documents. It operates on the principles of set theory and logic, where documents are represented as sets of terms or words, and queries are expressed as Boolean expressions using logical operators such as AND, OR, and NOT.
  
### Procedure:
1. ***Initialize the BooleanRetrieval class:*** The BooleanRetrieval class is defined to manage the indexing and searching of documents.
2. ***Constructor and Index Initialization:*** The class constructor initializes an empty index to store the inverted index mapping terms to documents.
3. ***Indexing Documents:***
    <p> a) The index_document method is responsible for indexing documents.
    <p> b) Tokenize the text content of documents, converting them into lowercase terms.
    <p> c) For each term in the document, it adds an entry in the index, associating the term with the document ID. </p>
4. ***Fetch Web Page Text:***
    <p>a) The fetch_webpage_text method uses the requests library to fetch content from a given URL.
    <p>b) Extract text content from the fetched HTML using BeautifulSoup.
    <p>c) The extracted text is returned for further processing.
5. ***Boolean Search:***
    <p>a) The boolean_search method performs Boolean searches on the indexed documents.
    <p>b) Tokenize the input query and iterates through its terms.
    <p>c) For each term in the query, it retrieves documents containing that term and performs Boolean operations (AND, OR, NOT) based on the query's structure.

### Program:
```
    import numpy as np
    import pandas as pd
    class BooleanRetrieval:
        def __init__(self):
            self.index = {}
            self.documents_matrix = None

    def index_document(self, doc_id, text):
        terms = text.lower().split()
        print("Document -", doc_id, terms)

        for term in terms:
            if term not in self.index:
                self.index[term] = set()
            self.index[term].add(doc_id)

    def create_documents_matrix(self, documents):
        terms = list(self.index.keys())
        num_docs = len(documents)
        num_terms = len(terms)

        self.documents_matrix = np.zeros((num_docs, num_terms), dtype=int)

        for i, (doc_id, text) in enumerate(documents.items()):
            doc_terms = text.lower().split()
            for term in doc_terms:
                if term in self.index:
                    term_id = terms.index(term)
                    self.documents_matrix[i, term_id] = 1

    def print_documents_matrix_table(self):
        df = pd.DataFrame(self.documents_matrix, columns=self.index.keys())
        print(df)

    def print_all_terms(self):
        print("All terms in the documents:")
        print(list(self.index.keys()))

    def boolean_search(self, query):
     parts = query.lower().split()
        if len(parts) == 1:
            return self.index.get(parts[0], set())
        
        if len(parts) == 2 and parts[0] == 'not':
            term = parts[1]
            term_docs = self.index.get(term, set())
            return self.all_doc_ids - term_docs
        if len(parts) != 3:
            return "Invalid query format. Use 'term1 operator term2' (e.g., 'python and information')."

        term1, operator, term2 = parts[0], parts[1], parts[2]
        
        result_set1 = self.index.get(term1, set())
        result_set2 = self.index.get(term2, set())
        
        if operator == 'and':
            return result_set1.intersection(result_set2)
        elif operator == 'or':
            return result_set1.union(result_set2)
        elif operator == 'not':
            return result_set1.difference(result_set2)
        else:
            return "Unsupported operator. Use 'and', 'or', or 'not'."

if __name__ == "__main__":
    indexer = BooleanRetrieval()

    documents = {
        1: "Python is a programming language",
        2: "Information retrieval deals with finding information",
        3: "Boolean models are used in information retrieval"
    }

    for doc_id, text in documents.items():
        indexer.index_document(doc_id, text)

    indexer.create_documents_matrix(documents)
    indexer.print_documents_matrix_table()
    indexer.print_all_terms()

    query = input("Enter your boolean query: ")
    results = indexer.boolean_search(query)
    if results:
        print(f"Results for '{query}': {results}")
    else:
        print("No results found for the query.")
```
### Output:
<img width="1820" height="487" alt="494244933-0ae6dec7-8374-47b7-9cce-acf55411a426" src="https://github.com/user-attachments/assets/4dd8c9b0-ff61-462a-bfa1-9ce3f37318be" />
<img width="1811" height="486" alt="494247314-fa4ce7fd-16da-45e0-9565-b5dd51fcb13e" src="https://github.com/user-attachments/assets/7d96c03c-8650-4a97-8c31-8da137029b38" />
<img width="1818" height="487" alt="494248064-c6180e41-6f96-4855-8d04-f891aee04b49" src="https://github.com/user-attachments/assets/015c23c2-59b6-4663-b9e4-e6a1f86b79b2" />



### Result:
  Implementation of Information Retrieval Using Boolean Model in Python is successfully completed.


