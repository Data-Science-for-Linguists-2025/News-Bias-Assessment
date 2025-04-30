# Fox vs. Vox: A linguistic assessment of subjectivity in U.S. news sources
by Claire McLean

## 0. Introduction

## 1. Background
There is a generally known in the United States that certain news sources are more "biased" than others, and in different directions. This phenomenon is known as "media bias", and involves "unjustable favoritism" in news coverage (Media Bias, 2008). One type of media bias is partisan bias, which involves the favoring of one political party over another. When discussing bias in the media, it becomes necessary to analyze the specific details of a piece that indicate a bias. From a linguistic standpoint, there are many ways to operationalize this, including factive verbs, subjective intensifiers, and one-sided terms. Due to time constraints, it proved to be a very difficult feat to attempt to analyze each of these linguistic bias indicators. I decided to choose just one: subjective intensifiers. The choice became clear due to constraints on my ability to operationalize each of these bias indicators. Factive verbs are verbs that "presupposed the truth of their complement clause". Tagging factive verbs and identifying them in a piece of text proves to be a difficult feat, as it becomes necessary to assess the verbs semantically, which is not easily accomplished by a computer. Likewise, one-sided terms are a great indicator of bias, but rely on semantic judgements, which are difficult to compute using technology. The indicator of bias in media that proved to be relatively simple to parse using computational methods was subjective intensifiers, which are made up of an degree adverb followed by an adjective. In English, there are a limited number of degree adverbs, and a handful of them have been studied in relation to the adjective they intensify. These degree adverbs are 'very', 'so', 'quite', and 'too' (Pan, 2021). The CLAWS7 tagset is equipped with tags for degree adverbs, and 'very', 'so', 'quite', and 'too' were shown to be among the most common in the British National Corpus, which was the corpus of the project. Though locating the most common subjective intensifiers in the COCA would have been ideal as this research project focuses on American English, in order to tag these subjective intensifiers properly, I would need a tagging model that has the ability to tag degree adverbs. After many unsuccessful attempts to access and work with the CLAWS7 tagset, I decided to add to the existing research by Pan 2021 and identify the collocations of the 4 aforementioned degree adverbs in the context of American English.

Additionally, it was necessary to choose the specific U.S. news articles that would act as my corpus for this project. I decided to investigate existing U.S media bias spectra to determine which one best fit the needs of my project. The framework of the AllSides Media Bias Chart proved to be effective for this project as it assessses bias alone, not accuracy in reportng. It is also based on inputs from 'ordinary' Americans as well as experts a opposed to an AI model trained to detect bias. As this projects attempts to show how U.S. news sources that are widely known to be biased can have their subjectivity supported by linguistic research, the AllSides Media Bias Chart was ideal. I selected one source from the 'left' side of the bias chart (Vox) and one source from the 'right' side of the bias chart (Fox News) to ensure that the level of bias in each was roughly equal in each direction. The notion of 'equal' levels of bias here is strictly based on their positions in the bias chart and reflects only the perceptions of Americans and not a concrete statistic.

## 2. Data Sourcing
Sourcing the U.S. news article data proved to be a challenging task, as web scraping techniques were necessary to extract it from the sites. After researching and experimenting with an existing Fox News web scraper, I decided to create by own using BeautifulSoup. I built each [scraper](scraping_scripts.ipynb) to extract the article title and the article body text and create a dictionary for each article consisting of these two entries. Each article dictionary was then compiled into a list and a dataframe was created. The article text was then sentence and word tokenized for each news source. The relevant URLs are linked [here](data.md).

Additionally, I needed a corpus of text that would serve as a 'non-subjective' sample. I decided to use the Brown corpus as it contains text from a variety of sources, many of which are not journalistic in nature. Further, I decided to use the Brown corpus as opposed to an 'non-subjective' news source for several reasons. First, it is difficult to identify a news source that lacks any sort of media bias or subjectivity. Second, a source in the middle of the bias spectrum can still be subjective, but in favor of a moderate ideology. The Brown corpus is also readily available as part of the open-source NLTK library, which makes it easily accessible for this project.

## 3. Data cleanup
The data cleaning portion of this project was very straightforward. To begin, I designed the two webscrapers to extract only the data that was relevant for my research project. This eliminated extra data and information that was not necessary. Further, as the BeautifulSoup web scraping process involves the creation of dictionaries, the process of transforming both lists of dictionaries into pandas dataframes was simple. One challenge that arose when initially examining the dataframes was that there were a few extra terms related to encoding such as 'nbsp'. I kept these terms for the majority of my analysis, but removed them, as well as other punctuation symbols to create WordClouds that were visually meaningful. Additionally, it came to my attention that some additional phrases that were not part of the article text body were scraped as well, including links beginning with 'CLICK HERE'. These were also eliminated prior to my analysis using regex across both the Fox and Fox Opinion dataframes. Eliminating these links ensured that the data used in my project was only article text body data.

## 4. Analysis
The goals of this project are 1) to examine how the frequencies of subjective intensifier constructions in the 'standard' news articles (non-opinion) and a non-news text, and 2) to investigate whether there is a significant difference in the prevalence of subjective intensifiers between the stardard news articles and the opinion articles from the same sources. It is also important to note my use of the term 'un-subjective' text in relation to this project. Here, I use the term 'un-subjective' text to refer to bigrams that are not subjective intensifier constructions. Further, the term 'non-news text' refers to the Brown corpus as mentioned earlier. I began my analysis by first gathering some basic statistics of the news article data. The Fox News corpus contained 20442 tokens, and the Fox News Opinion corpus contained 25385 tokens. The Vox corpus contained 31689 tokens, and the Vox Opinion (The Big Idea) corpus contained 48751 tokens. **These values are plotted below in Figure 1.** The Fox News 'standard' corpus is slightly smaller than the Vox 'standard' corpus, and the 'opinion' corpora are larger in terms of token count than their 'standard' counterparts.

#### Figure 1
![Token Frequencies of Fox News and Vox corpora](images/token_freq.png)

#### The analysis portion of this project is divided into 3 parts: unigram analysis, bigram analysis, subjective intensifer analysis,and a final comparison of subjective intensifier data

### Unigram Analysis
When assessing the most common unigrams in each of the corpora, it came as no surprise that stopwords and punctuation symbols are the most common. The Jupyter Notebook section for the unigram distribution is available [here](https://nbviewer.jupyter.org/github/Data-Science-for-Linguists-2025/News-Bias-Assessment/blob/main/data-pipeline.ipynb#Part-3:-Unigram-Analysis). The encoding term 'nbsp' was also a frequent unigram in the Fox News Opinion corpus. The WordClouds below demonstrate the most common unigrams in each corpus. In order to visualize these unigram frequencies in a meaningful way, I removed stopwords and most punctuation symbols in the WordClouds, leaving only words that carry substantial meaning. In further analyses, the stopwords and punctuation are kept. **Figures 2, 3, 4, and 5 demonstrate the most common non-punctuation and non-stopword unigrams in each corpus.**

#### Figure 2
![Fox News Unigram WordCloud](images/fox_wc.png)

#### Figure 3
![Fox News Opinion Unigram WordCloud](images/fox_oped_wc.png)

#### Figure 4
![Vox Unigram WordCloud](images/vox_wc.png)

#### Figure 5
![Vox Opinion (The Big Idea) Unigram WordCloud](images/fox_oped_wc.png)

As shown by the figures above, some common unigrams across all 4 corpora include 'trump' and 'president', though their specific frequencies vary across each corpus. As all 4 corpora are sourced from the 'Politics' section of each news source, these frequent unigrams signal the political nature of each corpus. Additional words with high frequencies are 'fox', 'news', and 'government' in both the Fox News and Fox News Opinion corpora, and 'one' and 'court' in both the Vox and Vox Opinion (The Big Idea) corpora. This step in my analysis proved to be beneficial for this project as it gives contextual insight into the types of bigrams that will be found in the bigram analysis portion of the project.

### Bigram Analysis
The bigram analysis portion of this project along with the conditional frequencies of different bigrams also gives substantial exploratory insight into the content of the corpora and paves the way for an effective bigram analyisis of the subjective intensifier constructions. Though the unigram and bigram analysis are mostly exploratory, they are necessary steps in understanding the data. In the bigram analysis, stopwords and punctuation are maintained. As the word 'trump' was very common in all 4 corpora, a conditional frequency analysis was conducted to retrieve the most common words following 'trump'. The conditional frequency distribution took only the instances of 'trump' with the part-of-speech tag 'NN' (noun) to ensure that these bigrams relate to the U.S. President and not the verb 'trump'. **Figures 6, 7, 8, and 9 below demonstrate these conditional frequency distributions.**

#### Figure 6
![Fox News Trump WordCloud](images/fox_trump.png)

#### Figure 7
![Fox News Opinion Trump WordCloud](images/fox_oped_trump.png)

#### Figure 8
![Vox Trump WordCloud](images/vox_trump.png)

#### Figure 9
![Vox Opinion (The Big Idea) Trump WordCloud](images/vox_oped_trump.png)

In the above plots, the word 'administration' appears to be a very common word following the word 'trump'. Additionally, words like 'touts', 'hammered', 'publicly', 'unceremoniously' and 'risks' in the Fox News and Fox News Opinion WordClouds suggest a deeper level of subjectivity that goes beyond the scope of subjective intensifiers. The Vox and Vox Opinion (The Big Idea) corpora contain words such as 'hyped', 'denied', 'claims' and 'blamed', which also suggest a deeper level of subjectivity. These words all carry semantic connotations that could be used in future research to investigate subjectivity in a different way. Though the conditional frequency distribution analysis of words following 'trump' is strictly exploratory, it demonstrates that the notion of linguistic subjectivity goes deeper than subjective intensifiers alone.

### Subjective intensifiers
As the main research questions of this project relate to subjective intensifier data specifically, it is necessary to analyze the distribution of each of the four subjective intensifiers: 'very', 'so', 'quite', and 'too' in all 4 corpora. This was accomplished by first creating lists of all words following each of 4 subjective intensifiers in all 4 corpora, with the addition of the Brown corpus which stands as the non-news text against which each of the 4 corpora are compared. Following the creation of the lists, conditional frequency distributions were then constructed and plotted. However, s this research project focuses mainly on the raw frequencies of all subjective intensifier constructions, the frequency of each *specific* adjective following each of the 4 subjective intensifiers was not necessary for the final analysis. The frequency distribution was conducted strictly as an exploratory measure. **Figures 10, 11, 12, and 13 below demonstrate the frequency distributions of all 4 subjective intensifiers across all 4 corpora. As the Brown corpus subjective intensifier data is strictly used for the purpose of frequency comparision, it was not plotted**.

#### Figure 10
![Fox News SI Bigrams](images/fox_si_bigrams.png)

#### Figure 11
![Fox News Opinion SI Bigrams](images/fox_oped_si_bigrams.png)

#### Figure 12
![Vox SI Bigrams](images/vox_si_bigrams.png)

#### Figure 13
![Vox Opinion (The Big Idea) SI Bigrams](images/vox_oped_si_bigrams.png)

As shown in the above plots, words such as 'many' and 'much' were common across all 4 corpora. As these are very common words in English, it is not surprising that they would be frequent in all of the corpora. 

The next step of the analysis is obtaining frequencies of all subjective intensifier constructions in the 4 news corpora and the Brown corpus. In terms of the frequency of subjective intensifier constructions in the corpora, there were 40 constructions in the Fox News corpus, 11 constructions in the Fox News Opinion Corpus, 48 constructions in the Vox corpus, 70 constructions in the Vox Opinion (The Big Idea) corpus, and 1154 constructions in the Brown corpus. These numbers alone cannot be compared to one another as each corpus was a different size, as shown [here](https://nbviewer.jupyter.org/github/Data-Science-for-Linguists-2025/News-Bias-Assessment/blob/main/data-pipeline.ipynb#Part-2:-Linguistic-analysis-of-data). These values can however, be used to create subjective intensifier to non-subjective intensifier bigram proportions for each of the 5 corpora (including the Brown corpus). These proportions allow for comparison of subjective intensifier frequencies across the corpora. These proportions are calculated in the following section.

### Final comparison of subjective intensifier data
The final step in the analysis portion of this project is to compare the subjective intensifier to non-subjective intensifier bigram proportions across the corpora. Two different statistical analyses were conducted to accomplish this task: 1) a proportion comparison(rounded to the 4th decimal place), and 2) proportion z-tests between the Fox News corpus and the Brown corpus, the Vox corpus and the Brown corpus, the Fox Opinion corpus and the Brown corpus, the Vox Opinion (The Big Idea) corpus and the Brown corpus, and finally the Fox News (standard) corpus and the Vox (standard) corpus. The z-test serves as an effective way to measure whether there is a significant difference between two different proportions. For my purposes, I used a series of two-sample proportion z-tests. **Figures 14, 15, 16, 17, and 18 below demonstrate the proportions of subjective intensifier bigrams to non-subjective intensifier bigrams.**

#### Figure 14
![Fox News SI Proportion](images/fox_pie.png)

#### Figure 15
![Fox News Opinion SI Proportion](images/fox_oped_pie.png)

#### Figure 16
![Vox SI Proportion](images/vox_pie.png)

#### Figure 17
![Vox Opinion (The Big Idea) SI Proportion](images/vox_oped_pie.png)

#### Figure 18
![Brown SI Proportion](images/brown_pie.png)

The above figures show slight differences in the proportions of subjective intensifier bigrams to non-subjective intensifier bigrams. To begin, when comparing 

## 5. Conclusion

## 6. References
 (2008). Media bias. In L. L. Kaid, C. Holtz-Bacha (Eds.) Encyclopedia of political communication (Vol. 2, pp. 434-440). SAGE Publications, Inc., https://doi.org/10.4135/9781412953993.n387