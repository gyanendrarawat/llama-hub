# Patronus AI FinanceBench Dataset

[![patronus-ai-logo (200 x 40 px)](https://github.com/nerdai/llama-hub/assets/92402603/62a6df3f-57a3-4d68-917b-b0947392efcd)](https://www.patronus.ai/)


This dataset is a subset of the original FinanceBench dataset. In particular, to
make this benchmark more computationally efficient, we only keep the documents for
which there are 2 or more questions. Such filtering, reduced the total unique pdf
documents from 98 to 32.

## CLI Usage

You can download `llamadatasets` directly using `llamaindex-cli`, which comes installed with the `llama-index` python package:

```bash
llamaindex-cli download-llamadataset PatronusAIFinanceBenchDataset --download-dir ./data
```

You can then inspect the files at `./data`.

## Code Usage

You can download the dataset to a directory, say `./data`. Then download the
convenient `RagEvaluatorPack` llamapack to run your own LlamaIndex RAG pipeline
with the llamadataset.

```python
from llama_index.llama_dataset import download_llama_dataset
from llama_index.llama_pack import download_llama_pack
from llama_index import VectorStoreIndex

# download and install dependencies for rag evaluator pack
RagEvaluatorPack = download_llama_pack(
  "RagEvaluatorPack", "./rag_evaluator_pack"
)
rag_evaluator_pack = RagEvaluatorPack()

# download and install dependencies for benchmark dataset
rag_dataset, documents = download_llama_dataset(
  "PatronusAIFinanceBenchDataset", "./data"
)

# build basic RAG system
index = VectorStoreIndex.from_documents(documents=documents)

# evaluate
query_engine = VectorStoreIndex.as_query_engine()  # previously defined, not shown here
rag_evaluate_pack.run(dataset=paul_graham_qa_data, query_engine=query_engine)
```