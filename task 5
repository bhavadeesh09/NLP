#task 5
import nltk
from nltk.tokenize import word_tokenize
nltk.download('punkt')
nltk.download('punkt_tab')
import string
import random
import nltk
from nltk.corpus import stopwords, reuters
from collections import Counter, defaultdict
from nltk import FreqDist, ngrams

nltk.download('punkt')
nltk.download('stopwords')
nltk.download('reuters')

sents = reuters.sents()
stop_word = set(stopwords.words('english'))


extra_punct = ' " - _'
string.punctuation += extra_punct
removal_list = set(stop_word).union(set(string.punctuation)).union({'\t', 'rt'})

unigram = []
bigram = []
trigram = []

for sentence in sents:

    sentence = [w.lower() for w in sentence if w != '.']
    unigram.extend(sentence)
    bigram.extend(list(ngrams(sentence, 2, pad_left=True, pad_right=True)))
    trigram.extend(list(ngrams(sentence, 3, pad_left=True, pad_right=True)))


def remove_stopwords_ngrams(ngrams_list):
    cleaned = []
    for tup in ngrams_list:

        if isinstance(tup, str):
            words = [tup]
        else:
            words = [w for w in tup if w is not None]


        if any(w not in removal_list for w in words):
            cleaned.append(tup)
    return cleaned

unigram = remove_stopwords_ngrams(unigram)
bigram = remove_stopwords_ngrams(bigram)
trigram = remove_stopwords_ngrams(trigram)

freq_uni = FreqDist(unigram)
freq_bi = FreqDist(bigram)
freq_tri = FreqDist(trigram)


d = defaultdict(Counter)
for (a, b, c), freq in freq_tri.items():
    if (a is not None) and (b is not None) and (c is not None):
        d[(a, b)][c] += freq

def pick_word(counter):
    "choose a random element from the counter elements"
    return random.choice(list(counter.elements()))

prefix = ("he", "is")
print(" ".join(prefix))
s = " ".join(prefix)

for i in range(19):
    suffix = pick_word(d[prefix])
    s = s + ' ' + suffix
    print(s)
    prefix = (prefix[1], suffix)
