# Progress Report

## 2/11/25:
Added necessary files to repository and created project plan. Haven't chosen license yet.

## 2/26/25:

### Working data pipeline:
[Pipeline](data-pipeline.ipynb)

### Sharing plan:
My plan for sharing my project is to go with the Creative Commons 1.0 license.

### Framework for news source selection
In order to select proper news sources, I did some research on which sources are known to be the most biased. The [AllSides Media Bias Chart](https://www.allsides.com/media-bias/media-bias-chart) proved to be a good resource for several reasons. First, I am only operationalizing bias, not credibility or accuracy. The purpose of this project is to assess bias through a linguistic lens, not to critique a particular news source. AllSides, unlike other bias charts like [Ad Fonte](https://app.adfontesmedia.com/chart/interactive), looks only at bias and not at accuracy in reporting. Second, AllSides data is based on input from ordinary Americans as well as experts. It is not AI-based, which benefits this project as the goal of this project is to create a model to identify bias linguistically. Multiple machine learning models on top of the other (AI bias detection model, linguistic bias detection model) could make this methodology very complicated.

Using AllSides as a starting point, I then selected one news source (Vox) that leans left according to the chart. In order to remain as unbiased as possible in methodology, I also selected one news source (Fox News) that leans right. 

### Framework for linguistic corpora
This step has proved to be the most difficult part of my methodology so far. The article [On the subjectivity of intensifiers](https://www.sciencedirect.com/science/article/abs/pii/S0388000107000198) has been a helpful resource in getting started on finding data that is appropriate for the project. Some datasets I found in earlier steps of this project relate only to movie data, or lack a concrete linguistic variable that is operationalized. This article led me to research by Wiebe, Janyce M., Bruce, Rebecca F., & O'Hara, Thomas P. (1999) which studied subjectivity classifications and created a custom dataset that was manually annotated.

Though the license for usage isn't clear, but after a correspondence with a professor, it became clear that this data is both safe to use and commonly used for NLP projects. I attempted to search for a license in the README file and the paper itself but it was not availabe. I have included a link to it [here](https://people.cs.pitt.edu/~wiebe/pubs/acl99/). Though the format is unfamiliar, I can make a few statements about the data based on the README file. First, the data is in the style of SGML markup. It follows the following structure:

format:
    article start tag
    paragraph_i start tag
    sentence_ij start tag
    clause_ijk start tag with subjectivity annotations (cluster attribute)
    ...

example:

<TXT art=FEAT docnum=891101-0108 tnum=??>
<MC  cluster=2 uid=1 soa="other" cmt="rs">
<wf pos=DT stem=an quote=0>An</wf>
(Wiebe et. al., 1999)

**Note:** It appears that the 'cluster' argument corresponds to the subjectivity annotation. As stated in the README, "Objective clauses are indicated by the attribute value cluster=1, and subjective clauses are indicated by cluster=2" (Wiebe et. al., 1999).

### Data pipeline for corpus
1. Assessed and researched style of data (SGML markup) and how to parse using Python. [Documentation for parser here](https://stackless.readthedocs.io/en/2.7-slp/library/sgmllib.html). [More information here](https://book.diveintopython.org/html_processing/introducing_sgmllib.html)
2. Read in dataset (subjectivity.data) [Reading in .data file tutorial](https://www.geeksforgeeks.org/how-to-read-data-files-in-python/)
3. Assessed dimensions of dataset (813 lines)
4. **Still working on processing corpus**; it has proved to be a more challenging task than anticipated. I began trying to parse it using BeautifulSoup but was unsuccessful. I will now endeavor to use regex to parse it instead, which will be slightly time-consuming!

### Framework for web scraping
1. [Researched how to scrape multiple articles at once](https://www.geeksforgeeks.org/how-to-scrape-multiple-pages-of-a-website-using-python/)
2. Attempted to webscrape a single article in [this jupyter notebook](data-pipeline.ipynb)
3. Planning to scrape 100 articles from each 'side' of the bias spectrum

## 3/21/25 (Progress Report 2)

### Working data pipeline:
[Pipeline](data-pipeline.ipynb)

### Framework for news source selection: Complete

### Framework for linguistic corpora: In progress
As outlined in the 2/26/25 progress report, the framework for linguistic corpora has certainly proved to be the most difficult part of this project's methodology. The following steps were taken to wrangle the [Subjective Intensifiers data](https://people.cs.pitt.edu/~wiebe/pubs/acl99/):

1. Turned data into a list of lists, with each entry/word being a sublist and each attribute and corresponding value being smaller sublists within the sublist
2. Attempted to create a dictionary from list of lists. The vision was for each word/entry to become a dictionary and for each value and attribute combination to be entries

Unfortunately, I was informed that the usage of this data relies heavily on data from the Penn Treebank, which is very expensive to use and therefore not feasable for this project. After some conversation with my TA, I decided to switch gears and choose another corpus to work from. This proved to be a good decision for many reasons. First, the subjective intensifiers data I was working with did not have a super clear license, which I was informed could be related to the age of the dataset. Second, the documentation for the data was rather sparse, and it was difficult to discern exactly what each tag indicated and how the data was formatted. NLTK does offer a small portion of the WSJ Penn Treebank data, but I believe that this is not sufficient for the project.

Instead of using the subjective intensifiers dataset that I was originally planning on using, I decided to look into some other ways that subjective intensifiers have been used in research. I came across an interesting research project [Intensification for discursive evaluation: a corpus-pragmatic view](https://www.degruyter.com/document/doi/10.1515/text-2020-0046/html?lang=en&srsltid=AfmBOopo-N_F6woyYgpgxoaxHIQ8dCifhyuLTKkrBdLBzL-2lpt8Kckp). The research focuses on the "internal structure(s) of meaning conveyed by “intensifier + adjective” constructions in naturally occurring text and speech", which makes this research a great baseline for my project The research uses the intensifiers 'very', 'so', 'quite', and 'too', and assesses the collocates for each. The corpus used is the BNC (British National Corpus) sampler, which would be a great fit for my project except for the fact that it is a corpus of British English. Since my project assesses linguistic bias in U.S. news articles, I need a corpus that reflects American English. The following [article](https://www.english-corpora.org/coca/compare-bnc.asp#:~:text=The%20Corpus%20of%20Contemporary%20American%20English%20(560%2B%20million%20words),not%20available%20from%20the%20BNC) discusses the BNC and the COCA (Corpus of Contemporary American English) and compares and contrasts the two. Based on this article and the similarities between the two corpora, I have decided to use the COCA along with the same four objective intensifiers as outlined by (Pan, 2021): 'very', 'so', 'quite', and 'too', to serve as the corpus for my project in place of the subjective intensifiers data by (Wiebe et. al., 1999).

### Framework for web scraping: In progress
As expected, webscraping has proved to be a very difficult undertaking. After an unsuccessful attempt at building a web scraper from scratch with only the assistance of BeautifulSoup tutorials, I looked online to see if a successful web scraper had been created that would fit my needs for this project. With one of my news sources being Fox News, I began my search for a Fox News webscraper, which I was able to find [here](https://github.com/StickmanNinja/Fox-News-Web-Scraper/tree/master). This scraper has been very helpful, but has still presented some challenges. First, I believe this scraper was made using an earlier version of Python, so I needed to modify it to fit Python 3.12. Further, I changed some variable names and made a few other small adjustments to customize the scraper. The license for the scraper is Apache 2.0 so I felt comfortable using it as a starting point. The Apache 2.0 license allows for modification, distribution, private use, and more.

One large issue that I ran into with the parser was its inability to locate the h3 tag which indicates the article title. The act of locating of this tag is essential for retrieving the news article data. My hypothesis is that somewhere within one of the functions, the scraped data goes from a nested format to an unnested format, which I believe is causing the parser to not locate certain tags upon command. This issue is one that I will discuss with my TA and/or professor. Once this issue is resolved, I will be able to successfully scrape many Fox News articles at once!

### Sharing scheme for found data
The University of Pittsburgh has an academic license for COCA. For this reason, I feel comfortable using this corpus for my project, thought I hesitate to link any data here. I am still not sure how much of the data is protected by an academic license. 

Though I have not successfully scraped the news article data, the sharing scheme for this portion of my found data is also unclear. After doing a bit of research into the [Fox News Network LLC Terms of Use Agreement](https://www.foxnews.com/terms-of-use), I read the following: "The Company Services are offered for your personal use only and may not be used for commercial purposes." However, a Google search into webscaping legality and the existance of multiple Fox News Web Scapers leads me to believe that I am allowed to scape this data. Though I am not using data for commercial purposes, I do not feel comfortable including any data here until further discussion with a professor.

### Sharing plan:
My plan for sharing my project is to go with the Creative Commons 1.0 license. I am comfortable with the use and redistribution of my project materials and do not expect credit. For this reason, after discussing the protocol for the COCA data sharing within this repository and nailing down the amount of data that I will be able to share, it is possible that I will only be able to share portions of the data in order to not breach the academic license that the University of Pittsburgh has for the COCA data.

## 4/1/25 (Progress Report 3)