# Progress Report

## 2/11/24:
Added necessary files to repository and created project plan. Haven't chosen license yet.

## 2/26/24:

### Working data pipeline:
[Pipeline](data-pipeline.ipynb)

### Sharing plan:
My plan for sharing my project is to go with the Creative Commons 1.0 license.

### Framework for news source selection
In order to select proper news sources, I did some research on which sources are known to be the most biased. The [AllSides Media Bias Chart](https://www.allsides.com/media-bias/media-bias-chart) proved to be a good resource for several reasons. First, I am only operationalizing bias, not credibility or accuracy. The purpose of this project is to assess bias through a linguistic lens, not to critique a particular news source. AllSides, unlike other bias charts like [Ad Fonte](https://app.adfontesmedia.com/chart/interactive), looks only at bias and not at accuracy in reporting. Second, AllSides data is based on input from ordinary Americans as well as experts. It is not AI-based, which benefits this project as the goal of this project is to create a model to identify bias linguistically. Multiple machine learning models on top of the other (AI bias detection model, linguistic bias detection model) could make this methodology very complicated.

Using AllSides as a starting point, I then selected one news source (Vox) that leans left according to the chart. In order to remain as unbiased as possible in methodology, I also selected one news source (Fox News) that leans right. 

### Framework for linguistic corpora
This step has proved to be the most difficult part of my methodology so far. The article [On the subjectivity of intensifiers](https://www.sciencedirect.com/science/article/abs/pii/S0388000107000198) has been a helpful resource in getting started on finding data that is appropriate for the project. Some datasets I found in earlier steps of this project relate only to movie data, or lack a concrete linguistic variable that is operationalized. This article led me to research by Wiebe, Janyce M., Bruce, Rebecca F., & O'Hara, Thomas P. (1999) which studied subjectivity classifications and created a custom dataset that was manually annotated. 

Though the license for usage isn't clear, but after a correspondence with Dr. Na-Rae Han, it became clear that this data is both safe to use and commonly used for NLP projects. I have included a link to it [here](https://people.cs.pitt.edu/~wiebe/pubs/acl99/). Though the format is unfamiliar, I can make a few statements about the data based on the README file. First, the data is in the style of SGML markup. It follows the following structure:

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
3. Assessed dimensions of dataset

### Framework for web scraping
1. [Researched how to scrape multiple articles at once](https://www.geeksforgeeks.org/how-to-scrape-multiple-pages-of-a-website-using-python/)
2. Attempted to webscrape a single article in [this jupyter notebook](data-pipeline.ipynb)
3. Planning to scrape 100 articles from each 'side' of the bias spectrum
