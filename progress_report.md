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

Though the license for usage isn't clear so I will not include the raw data in my repository, I have included a link to it [here](https://people.cs.pitt.edu/~wiebe/pubs/acl99/). Though the format is unfamiliar, I can make a few observations: the data seems to consist of isolated words which are tagged for part of speech, 'nc' which I am not sure about, stem, quote, and cluster. All occurrences are tagged for subjectivity as well. It will take some time to truly understand and work with this data, but it is an extremely promising start.

### Framework for web scraping
1. [Researched how to scrape multiple articles at once](https://www.geeksforgeeks.org/how-to-scrape-multiple-pages-of-a-website-using-python/)
2. Attempted to webscrape a single article in [this jupyter notebook](data-pipeline.ipynb)
3. Planning to scrape 100 articles from each 'side' of the bias spectrum
