# Word-frequency-and-parts-of-speech-tagger

The project reads text from a csv file, calculates the frequency of words using the "Counter" library from collection,
attaches parts of speech for the words using the parts of speech tagger, picks the top 30 adjectives, adds it into a dataframe
and saves the dataframe to an excel file.

# Code Example

import pandas as pd
import collections
from collections import Counter
import nltk

table = pd.read_excel('RJ.xlsx')
df = pd.DataFrame(table)
df1 = table['Text'].str.lower().str.split() #seperates the words in a string
c = list(df1)

def word_count():
    for x in range(1):
        c1 = Counter(c[x]).most_common(30)
        list1 = list(c1)
        return [x[0] for x in list1]
          
             
def pos_tag():
    for x in range(1):
        c1 = Counter(c[x])
        tagged = nltk.pos_tag(c1)
        noun = [word for word, pos in tagged if pos == 'JJ']
        return noun

for x in range(1):
    c1 = Counter(c[x]).most_common(30) 
words = set(word_count())&set(pos_tag())

b = [item for item in c1 if item[0] in words]
DF = pd.DataFrame(b)


DF.to_excel(writer, sheet_name = 'Top words')
writer.save()
