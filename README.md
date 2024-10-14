# py-rust-stemmers
py-rust-stemmers is a high-performance Python wrapper around the rust-stemmers library, utilizing the Snowball stemming algorithm. This library allows for efficient stemming of words with support for parallel processing, making it a powerful tool for text processing tasks. The library is built using maturin to compile the Rust code into a Python package.

## Features
* Snowball Stemmer: Uses the well-known Snowball stemming algorithms for efficient word stemming in multiple languages.
* Parallelism Support: Offers parallel processing for batch stemming, providing significant speedup for larger text sequences.
* Rust Performance: Leverages the performance of Rust for fast, reliable text processing.

## Installation
You can install py-rust-stemmers via pip:

```pip install py-rust-stemmers```

## Usage
Here's a simple example showing how to use py-rust-stemmers to stem words using the Snowball algorithm:

```
from py_rust_stemmers import SnowballStemmer

# Initialize the stemmer for the English language
s = SnowballStemmer('english')

# Input text
text = """This stem form is often a word itself, but this is not always the case as this is not a requirement for text search systems, which are the intended field of use. We also aim to conflate words with the same meaning, rather than all words with a common linguistic root (so awe and awful don't have the same stem), and over-stemming is more problematic than under-stemming so we tend not to stem in cases that are hard to resolve. If you want to always reduce words to a root form and/or get a root form which is itself a word then Snowball's stemming algorithms likely aren't the right answer."""
words = text.split()

# Example usage of the methods
stemmed = s.stem_word(words[0])
print(f"Stemmed word: {stemmed}")

# Stem a list of words
stemmed_words = s.stem_words(words)
print(f"Stemmed words: {stemmed_words}")

# Stem words in parallel
stemmed_words_parallel = s.stem_words_parallel(words)
print(f"Stemmed words (parallel): {stemmed_words_parallel}")
```
___
## Methods
```stem_word(word: str) -> str```

This method stems a single word. It is best used for small or isolated stemming tasks.

Example:
```
s.stem_word("running")  # Output: "run"
```
___
```stem_words(words: List[str]) -> List[str]```

This method stems a list of words sequentially. It is ideal for processing short to moderately sized text sequences.

Example:

```s.stem_words(["running", "jumps", "easily"])  # Output: ["run", "jump", "easili"]```
___
```stem_words_parallel(words: List[str]) -> List[str]```

This method stems a list of words in parallel. It provides significant speedup for longer text sequences (e.g., sequences longer than 512 tokens) by utilizing parallel processing. It is ideal for batch processing of large datasets.

Example:

```s.stem_words_parallel(["running", "jumps", "easily"])  # Output: ["run", "jump", "easili"]```

## Build from source
* Install maturin
* Go to project dir

```
maturin build --release
pip install target/wheels/py_rust_stemmers-<your os/architecture/etc>.whl
```

## License
This project is licensed under the MIT License. See the LICENSE file for more details.