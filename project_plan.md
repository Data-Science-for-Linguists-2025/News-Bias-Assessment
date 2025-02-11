# Claire's Project Plan
## News Bias Assessment

### Summary of project
This project will use linguistic methodologies to assess bias in major U.S. news source articles. More specifically, the goal of the project is to first identify news sources that are commonly known to be biased in any direction (literature review will be required), then use the scikit-learn package to train a model to detect bias using annotated datasets of the following linguistic phenomena:

- Factive verbs
- Subjective intensifiers
- One-sided terms

Note: this list may be reduced to one or two phenomena depending on time and resources.

The ultimate aim of this project is to see if 'biased' news articles use polarized or biased language, according to the above list of identifiers. The identifiers will be indentified in the web-scraped news article dataset which will allow me to assess bias in a way that is both linguistically relevant and supported by previous research (Recasens, et. al, 2013).

### Data
I will web-scrape a dataset of various news articles across (5?) different major U.S. news sources.

I will apply annotated datasets of linguistically-biased language to the news article dataset. Here are some options for biased language datasets:

[Opinosis: A Graph Based Approach to Abstractive Summarization of Highly Redundant Opinions](http://kavita-ganesan.com/opinosis/#.Wmljc6iWYow)

[The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset)
Note: The above dataset contains movie reviews, which are generally considered to be opinions as opposed to facts. Will need to look further into this data to see if it is appropriate for this project.

[Arguments-Fact vs Opinion](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/VYJO3A)

### Analysis
I will use the web-scraped news data as well as datasets containing factive verbs, subjective intensifiers, one-sided terms, or generally-accepted 'biased' terms to train a model to see if more biased news sources use more biased language.


### Helpful resources
[Cognitive factive verbs across languages](https://www.sciencedirect.com/science/article/pii/S0388000121001054)
[Neural Models of Factuality](https://aclanthology.org/N18-1067.pdf)
[Annotating Factive Verbs](http://www.lrec-conf.org/proceedings/lrec2012/pdf/757_Paper.pdf)