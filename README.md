# Copyright Transparency in Common Crawl 
This project aims to investigate the transparency of generative AI training datasets by examining how webpage content allow potentially copyrighted work to be traced 
to their original sources. The project will use the Common Crawl archive to understand how text indicators can support the identification of potentially copyrighted content.

# Project Overview 
Using Python, the study combines exploratory data analysis, data visualization, and logistic regression to evaluate the detectability of copyright-related information in large-scale web archives.

# Research Questions
How frequently do explicit copyright indicators appear within Common Crawl webpages?
How does copyright indicator prevalence vary across crawl releases and domain extensions?
To what extent can webpage characteristics predict the presence of copyright indicators?

# Data Source
This project uses data from Common Crawl, a publicly accessible archive of web crawl data. The analysis will focus on WET files, which contain extracted text from crawled webpages.
For each webpage, the source URL, crawl release identifier, crawl timestamp, extracted webpage text, and presence of copyright indicators will be collected.
To manage computational resources, a sample of WET files is selected from multiple Common Crawl releases and a maximum of 500 webpage records are extracted from each WET file. 

# Methodology
The Common Crawl WET files are accessed through HTTP requests and processed using the ArchiveIterator function from the Warcio library. 
The extraction process collects webpage text, including the URL, crawl identifier, and timestamp. The extracted records are then converted into a Pandas dataframe and saved in parquet form for further analysis.
Each extracted webpage text is examined for three explicit copyright indicators: Copyright symbol, the word copyright, and the phrase All Rights Reserved. Each indicator is represented as a Boolean variable indicating whether each was detected.
Additionally, the two variable indicator_count and has_copyright_indicator are created and used throughout the analysis and modeling process. 
indicator_count determines the number of different copyright indicators on a webpage, ranging from 0 to 3.
has_copyright_indicator is a binary variable determining whether as least one copyright indicator is present. 

Exploratory data analysis is conducted to identify patterns in copyright indicator prevalence. The analysis includes examining the number of indicators on each webpage, calculating the frequency and percentage of webpages containing each indicator, comparing indicator prevalence across domain extensions, and examining the relationship between webpage length and copyright indicator presence. 
Tables and visualizations are also created to better communicate these findings.

For the predictive modeling, the feature variables contain word count, character count, line count, domain extension, length of url, and the crawl id. The target variable is has_copyright_indicator. 
Categorical variables are converted into numerical using one-hot encoding. The numerical features are standardized for fitting the logistic regression model. 
The logistic regression model is used to investigate whether webpage characteristics can predict the presence of copyright indicators. The model is trained and evaluated using separate training and testing datasets.
Regression coefficients are examined to find associations between webpage characteristics and copyright indicator presence. 

# Model Evaluation
The logistic regression models is evaluated using accuracy, precision, recall, F1-score and ROC-AUC. 
The model produced 57.17% Accuracy, 57.70% Precision, 92.69% Recall, 0.711 F1 score and .554 ROC-AUC. 
The model achieved high recall for webpages containing copyright indicators but performed poorly when identifying webpages without them. Furthermore, the ROC-AUC score indicates limited ability to distinguish between the two classes. 
These findings suggest that basic webpage characteristics provide limited predictive information about the presence of copyright indicators in the data sample. 

# Ethical Considerations
This project examines copyright transparency as an issue related to data ethics and accountability. All analyses are based on publicly accessible Common Crawl data. The project does not attempt to establish copyright ownership or determine whether specific uses of collected content are legally authorized.
The findings are intended to contribute to discussions surrounding transparency, documentation, and the challenges of identifying potentially copyrighted materials in larger scale web data.
