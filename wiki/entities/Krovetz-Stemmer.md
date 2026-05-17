# Krovetz-Stemmer

The **Krovetz Stemmer** is a hybrid stemming algorithm that combines dictionary lookups with algorithmic rules.

## Mechanism
1. If a word is found in the dictionary, it is left unchanged.
2. If not, the algorithm attempts to remove a suffix such that the resulting stem is a valid word in the dictionary.

## Advantage
It is generally more precise than the Porter stemmer because it avoids reducing words to non-existent stems.

See also: [[Stemming]]
