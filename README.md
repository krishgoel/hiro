# HIRO: Hierarchical Information Retrieval Optimization
> A Querying Mechanism Coupled with [RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval](https://arxiv.org/abs/2401.18059)

**HIRO** introduces a novel querying approach that optimizes information retrieval in Retrieval-Augmented Generation (RAG) systems using hierarchical structures, employing recursive similarity scoring and branch pruning to refine the context delivered to language models, enhancing both accuracy and efficiency.

Link to the original paper: [HIRO: Hierarchical Information Retrieval Optimization](https://arxiv.org/abs/2406.09979)

## Installation Guide
To use HIRO coupled with RAPTOR, clone the HIRO Repository and install the required dependencies (ensure Python 3.8+ is installed):

```bash
git clone https://github.com/KrishGoel/hiro.git
cd hiro
pip install -r requirements.txt
```

## HIRO Querying in Action

To get started with HIRO Querying, follow these steps:

### Setting Up RAPTOR with HIRO

Set your OpenAI Key and initialize RAPTOR with the HIRO configuration, adjust the `tr_hiro_selection_threshold` and `tr_hiro_delta_threshold` parameters to optimize the retrieval process (we recommend using Bayesian Optimization for hyperparameter tuning for large scale applications):

```python
import os
os.environ["OPENAI_API_KEY"] = "your-openai-api-key"

from raptor import RetrievalAugmentation, RetrievalAugmentationConfig

hiro_config = RetrievalAugmentationConfig(
    tr_selection_mode="hiro",
    tr_hiro_selection_threshold=0.6,
    tr_hiro_delta_threshold=0.08
)

RA = RetrievalAugmentation(config=hiro_config)
```

### Basic Usage

```python
# Adding text documents
with open('text_file.txt', 'r') as file:
    text = file.read()
RA.add_documents(text)

# Saving a tree
SAVE_PATH = "demo/douglas_adams"
RA.save(SAVE_PATH)

# Loading a saved tree
RA = RetrievalAugmentation(tree=SAVE_PATH)

# Question-Answering
question = "What is the answer to life, the universe, and everything else?"
answer = RA.answer_question(question=question)
print("Answer: ", answer)
```

For information on extending RAPTOR with custom models and advanced usage, refer to the [original RAPTOR Documentation](https://github.com/parthsarthi03/raptor/blob/master/README.md).

## License

HIRO is released under the [MIT License](./LICENSE.txt).