# Progress report

The [progress.py](progress.py) is a Python script that loops through the corpus files and reports the number of texts, genres covered, unique characters and number of tokens per language. Unlike [file_counts](../file_counts) and [line_counts](../line_counts) this report returns zero values for languages that are not covered yet. The output format is a `CSV` file of the following structure:  `language,number_texts,number_genres,number_characters,number_tokens`. The `CSV` file will be written to the same directory as the script.

The report can be produced in two modes:

1. Using simple tokenization (fast; 7-9 minutes as per 30.03.20)
- The command for producing the report in this mode: `python progress.py -s`
- The output file is named `progress_simple.csv`
- The first mode tokenizes the texts in a simple way, i.e. splits the texts by white spaces. The report in this mode provides approximate number of tokens for most of the languages; the numbers are less reliable for Burmese, Chinese, Japanese, Korean and Thai.

2. Using advanced tokenization (slow; approx. 4.5 hours as per 30.03.20)
- The command for producing the report in this mode: `python progress.py -a`
- The output file is named `progress_advanced.csv`

The second mode tokenizes the texts language specifically by using different Python libraries:

- `word_breaker`: Burmese
- `pythainlp`: Thai
- `wordfreq`: English, Finnish, French, German, Greek, Hindi, Indonesian, Japanese, Korean, Mandarin, Persian, Russian, Spanish, Turkish
- `NLTK`: other languages

Before running the code in an advanced mode, please install the required libraries by running the command:

`pip install -r requirements.txt`

Additional preparation steps:

a) Download the `word_breaker` library for Burmese from [this repository](https://github.com/stevenay/myan-word-breaker), unzip it into the same folder where you store the script `progress.py`

b) Install Japanese dictionary `mecab-ipadic`. Installation file for Linux can be found [here](https://packages.ubuntu.com/xenial/all/mecab-ipadic-utf8/download)

c) Install Korean dictionary `mecab-ko-dic`. Installation commands for Linux:

```
wget https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/mecab-ko-dic-2.0.1-20150920.tar.gz
tar zxfv mecab-ko-dic-2.0.1-20150920.tar.gz
cd mecab-ko-dic-2.0.1-20150920
./configure
sudo ldconfig
make
sudo make install
```