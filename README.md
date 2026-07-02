# ML Crash Course - Softserve

A hands-on crash course in Artificial Intelligence and Machine Learning, organized as a set of Jupyter notebooks. Each topic is split into **theory** notebooks (concepts + worked examples) and, where applicable, **task** notebooks (exercises to practice on your own).

## 📚 Contents

| # | Topic | Notebooks |
|---|-------|-----------|
| 1 | AI Intro | [Theory](<notebooks/ai%20intro/theory/AI_Intro.ipynb>) · [Task](<notebooks/ai%20intro/task/AI_Intro_Task_v2.ipynb>) |
| 2 | Search Algorithms in AI | [Theory Part 1](<notebooks/search%20algorithms/theory/Search_Algorithms_in_AI_part_1.ipynb>) · [Theory Part 2](<notebooks/search%20algorithms/theory/Search_Algorithms_in_AI_part_2.ipynb>) · [Task](<notebooks/search%20algorithms/task/Search_Tasks_L1.ipynb>) |
| 3 | Optimization in AI | [Theory](<notebooks/optimization/theory/Optimization_in_AI.ipynb>) · [Task](<notebooks/optimization/task/Optimization_Tasks.ipynb>) |
| 4 | Data Collection & Scraping | [Theory](<notebooks/data%20collection%20and%20scraping/theory/Data_Collection_and_Scraping.ipynb>) |
| 5 | Data Preprocessing & Visualization | [Preprocessing](<notebooks/data%20preprocessing%20and%20visualization/theory/Data_Preprocessing.ipynb>) · [Visualization](<notebooks/data%20preprocessing%20and%20visualization/theory/Data_Visualization.ipynb>) |
| 6 | Machine Learning | [Regression](<notebooks/machine%20learning/theory/Regression.ipynb>) · [Classification](<notebooks/machine%20learning/theory/Classification.ipynb>) · [Unsupervised Learning](<notebooks/machine%20learning/theory/Unsupervised_Learning.ipynb>) |
| 7 | Deep Learning | [Theory](<notebooks/deep%20%20learning/theory/Deep_Learning.ipynb>) |
| 8 | NLP | [Theory](<notebooks/nlp/theory/NLP.ipynb>) |
| 9 | AI Ethics | [Theory](<notebooks/ai%20ethics/theory/AI_Ethics.ipynb>) |
| 10 | Final Project | [Clothing image classification](<notebooks/final%20project/notebook.ipynb>) |

Every theory/task notebook also has an **"Open in Colab"** badge at the top if you'd rather run it in the cloud without any local setup.

## 🚀 Getting started (local setup)

This project uses a [`pyproject.toml`](pyproject.toml) to pin every dependency actually imported by the notebooks, and a [`.python-version`](.python-version) file pinning **Python 3.11**.

> **Why Python 3.11?** `scikit-learn-extra` (used for K-Medoids/CLARA in the *Unsupervised Learning* notebook) only ships pre-built wheels up to Python 3.11, and it requires `numpy<2.0`. Pinning 3.11 + `numpy<2` keeps it, `tensorflow==2.15.x` (last TF release before the NumPy 2.0 migration) and the rest of the stack installable without compiling anything from source.

### 1. Install Python 3.11

Using [`pyenv`](https://github.com/pyenv/pyenv) (recommended, reads `.python-version` automatically):

```bash
pyenv install 3.11
pyenv local 3.11
```

### 2. Create a virtual environment and install dependencies

Using [`uv`](https://docs.astral.sh/uv/) (fast, reads `pyproject.toml` + `.python-version` automatically):

```bash
uv sync
# search-algorithms notebooks also need an extra helper package pulled from GitHub:
uv sync --extra search-algorithms
```

Or with plain `venv` + `pip`:

```bash
python3.11 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install -e .
pip install -e ".[search-algorithms]"   # optional, for notebooks/search algorithms
```

### 3. Extra one-time setup

- **NLTK data** (used in `Data_Preprocessing`, `NLP`): download the corpora the notebooks need:
  ```bash
  python -m nltk.downloader punkt punkt_tab stopwords wordnet
  ```
- **Graphviz** (used by `pydot`/`networkx.drawing.nx_pydot` for graph layouts in the search algorithms notebooks): install the system binary in addition to the `pydot` Python package:
  ```bash
  # Debian/Ubuntu
  sudo apt-get install graphviz
  # macOS
  brew install graphviz
  ```
- **Google Colab-only cells**: a few notebooks contain a `from google.colab import drive` cell used to mount Google Drive when running on Colab. It's not a pip dependency and can simply be skipped when running locally.
- **`cooltest`**: a small grading/testing helper used only in the search algorithms notebooks, installed straight from its GitHub repo via the optional `search-algorithms` extra above.

### 4. Launch Jupyter

```bash
jupyter lab
```

## 🗂️ Project structure

```
notebooks/
├── ai intro/{theory,task}
├── search algorithms/{theory,task}
├── optimization/{theory,task}
├── data collection and scraping/theory
├── data preprocessing and visualization/theory
├── machine learning/theory
├── deep  learning/theory
├── nlp/theory
├── ai ethics/theory
└── final project/
pyproject.toml       # pinned dependencies
.python-version       # Python 3.11
```

## 📄 License

See [LICENSE](LICENSE).
