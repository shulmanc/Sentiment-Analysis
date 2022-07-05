**Background**
The Yelp website and app provide crowd-sourced reviews about businesses. We can use the Yelp Fusion API to iterate through a bunch of Toronto-area restaurants and download their reviews and star ratings as training data for a very simple Naive Bayes classifer to do sentiment analysis.

**The Problem**
It turns out that Yelp's Business Search API has a very signifcant limitation: it only displays the first sentence or two of each review, truncating the rest with an ellipsis at the end. This hinders a data-hungry model from reaching its peak potential.

The way Yelp intended the API to be used was for the consumer (i.e, the application developer using the API) to use the included reviews[x].url field to redirect the end-user to a web page containing the rest of the review (so that Yelp can get a few more ad impressions in the process). Our goal was to get around this problem and improve the results of the Naive Bayes model.

**The Solution**
I used a combination of techniques to improve the training dataset.

You only receive 50 reviews from a single API request. So, using pagination (using limit and offset inputs) ~3000 reviews were recieved significantly increasing the size of the training set

The data still had only the first sentence of a review. To get around this I scraped the review url using Beautiful Soup to get the full text of the review.

The chart below highlights the distribution of positive and negative reviews used 
![image](https://user-images.githubusercontent.com/60298572/177405611-daae350f-e36d-4a3c-a7d8-3abd69ccaec2.png)

The resulting model has a prediction accuracy of 82%! Highlighting a successful sentiment classifier
