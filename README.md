# Interactive visualizations prepared for the paper: Comparing Political Information Exposure on Facebook during Two Italian General Elections

Fabio Giglietto, Università degli Studi di Urbino Carlo Bo; Giada Marino, Università degli Studi di Urbino; Roberto Mincigrucci, Università degli Studi di Urbino Carlo Bo; Nicola Righetti, University of Vienna; Luca Rossi, IT University of Copenhagen; Anna Stanziano, Università degli Studi di Urbino Carlo Bo; Massimo Terenzi, Università degli Studi di Urbino Carlo Bo

Paper presented at the conference: AssoCompol - [Beyond digital political communication: platforms, algorithms and automation](https://www.compol.it/eventi/convegno/convegno-2023/), University of Torino. 8 - 10 June 2023

#### Getting started

This repository houses the code necessary to create two interactive visualizations, representing the news clusters identified during the Italian General Elections of 2018 and 2022. While the data required to reproduce these visualizations is not included, we have provided self-contained HTML files for the 2018 and 2022 interactive visualizations. **Please note, to access these, you'll need to download the raw HTML files**.

Otherwise you can explore the visualizations online: [2018](https://rawcdn.githack.com/lrossi79/Altair_NewsExposure_cluster_viz/4226dcc0c3ab8e1d31a8f68b8590b8af1bb04557/2018.html) \| [2022](https://rawcdn.githack.com/lrossi79/Altair_NewsExposure_cluster_viz/d4fe49b31673734269d5ebe7fa9509510fca338b/2022.html)

#### Abstract

The rise of social media has increased citizen news involvement, yet heightened misinformation risks. Studies aiming to estimate false news prevalence and understand its targets have faced methodological challenges due to various limitations of exposure measurement techniques. Various techniques, including surveys, tracking tools, and media diaries measure political information exposure, each with limitations. For accurate metrics, platform-provided data is necessary, yet often inaccessible. Using Meta's URL Shares Dataset, we examined the exposure of Italian Facebook users to political content in the 2018 and 2022 pre-election periods. We developed a binary classifier fine-tuning the OpenAI curie model achieving a precision of 0.911, recall of 0.883, and F1 score of 0.897. We determined political URL topics with a k-means clustering algorithm applied to document embeddings of 27,487 URLs in 2018 and 8,308 URLs in 2022. The OpenAI DaVinci model labeled each cluster. We respectively identified 27 clusters for 2018 and 24 for 2022. Our analysis revealed a significant reduction in the circulation and overall exposure of political links among Italian users between 2018 and 2022. Additionally, we noted a considerable shift in the platform's user base toward an older demographic. Stories related to the economy constituted a third of all views in 2022, while immigration emerged as the dominant topic in 2018. Despite these disparities, several common topics and a pervasive anti-establishment sentiment characterized both campaigns. Furthermore, our results indicated that older users were exposed to hyper-partisan sources more frequently than other users.

#### Method

This research used [Meta's Facebook Privacy-Protected Full URLs Data Set](https://socialscience.one/blog/unprecedented-facebook-urls-dataset-now-available-research-through-social-science-one), an anonymized dataset that allows researchers to study user interaction with external web links on Facebook. The utilized version, [version 10](https://dataverse.harvard.edu/file.xhtml?fileId=6290811&version=10.1), covers user interactions from 46 countries, including more than 68 million links shared on Facebook between January 1, 2017, and October 31, 2022. To protect user privacy, only URLs publicly shared by over 100 users, with Laplace random noise added, are included. The data includes various information about the links, including URL, parent domain, the date it was first shared, country code of the most frequent sharers, and rating by a third-party fact-checker if available.

The study focuses on the Italian political URLs that circulated on Facebook during the months preceding the Italian elections in 2018 and 2022. Initially, 84,874 URLs that were prevalently shared by Italian users were identified. From this, a sample of 4,190 titles and descriptions were used as a training set in the fine-tuning of a binary classifier of political versus non-political URLs. The manual classification of these URLs was performed by seven coders. After cleanup, the final fine-tuning dataset consisted of 3,800 valid cases (1,801 politics and 1,999 other).

Using the coded dataset, OpenAI's curie model was fine-tuned. Following a cleanup of the dataset to remove links that were not in Italian or had missing or inadequate titles and descriptions, 77,528 URLs were left. The fine-tuned model classified all URLs for both the 2018 and 2022 elections, labeling approximately half of them as political.

For all political URLs, vector representations (or embeddings) were retrieved using OpenAI's embeddings API. Cluster analysis was performed on these vectors to group political URLs by similarity, resulting in 27 clusters for the 2018 election and 24 for the 2022 election. Each cluster was automatically labeled using the OpenAI gpt-3.5-turbo model.

------------------------------------------------------------------------

Interactive visualization of the clusters: [2018](https://rawcdn.githack.com/lrossi79/Altair_NewsExposure_cluster_viz/4226dcc0c3ab8e1d31a8f68b8590b8af1bb04557/2018.html) \| [2022](https://rawcdn.githack.com/lrossi79/Altair_NewsExposure_cluster_viz/d4fe49b31673734269d5ebe7fa9509510fca338b/2022.html)

------------------------------------------------------------------------

Finally, using the unique identifiers of all political URLs classified in each cluster, the Facebook Privacy-Protected Full URLs Dataset was queried to count the number of Italian users - broken down by age classes - who viewed each URL. These values were then aggregated by clusters, taking into account the effect of the noise. This approach provided insights into how different age groups interacted with political content during the election periods.
