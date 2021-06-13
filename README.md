# Introduction

## Problem exposition and Business Value

The problem I aimed to solve in this project relates to mental health at work, the associated costs and the services offered to employees that may help them manage and ultimately treat their mental health issues. This problem is framed as the following question: "Is it possible to accurately predict which individuals in the workplace have a mental illness, so that they may be offered the support and services they need as part of company mental health initiatives?"

In the past two decades or so, nearly every major mental illness has seen rates of incidence rise significantly. Therefore, more emphasis has been placed on the importance of mental health as the costs to the individual and to society become more apparent.

The major costs for businesses of untreated mental illnesses among employees are:

- absenteeism
- loss of productivity
- employee burnout
- health insurance
- rehiring (to replace an employee who has discontinued work due to mental healh reasons)

According to the [World Economic Forum](https://www.weforum.org/reports/global-economic-burden-non-communicable-diseases), mental health conditions will cost $16.1 trillion from 2011 to 2031. If we are able to accurately predict the individuals in the workplace who have a mental health condition and offer them the support and resources they need, [businesses may save 2 to 4 USD for every dollar they spend on intervention and prevention](https://www.thelancet.com/journals/lanpsy/article/PIIS2215-0366(16))

So, offering mental health services at work not only improves company culture, potentially making it easier to hire talent, but also makes sense from a purely financial point of view.

## Data

The data is provided by [Open Source Mental Illness](https://osmihelp.org/research) and is taken more specifically from their [2014 survey](https://www.kaggle.com/osmi/mental-health-in-tech-survey). It has 27 features, most of which are questions that elicit binary "Yes/No" responses. An example feature is "If you have a mental health condition, do you feel that it interferes with your work?"

# Approach and Insights

## Cleaning and EDA

Since the data was collected as part of a survey, there were some human errors in filling in information, ranging from misspellings to erroneous entries for Age. About 6% of the data was missing. I replaced NaNs with the mode or median depending on the feature, most interestingly in features where some of the answers provided were ambiguous in nature ("maybe", "don't know") and fixed the aforementioned misspellings manually.

For EDA, I chose 8 features to explore that belonging into 1 of 2 groups that I defined. These were variables that i) illustrated the cultural attitude of a company towards mental health or ii) could have possible causal relationships with mental health conditions. Because the majority of the features are categorical variables, there was not much inherent variety in the graphs created.

Among other insights, the EDA showed that about half of the respondents had sought treatment for mental health and that most respondents could avail mental health services, although a considerable minority could not. Individuals in older age groups tended to have sought treatment more so than younger individuals, with the caveat that the majority of the data belonged to the latter group, so generalisations are difficult.

## Feature Engineering

Feature engineering was brief and mostly focused on encoding categorical variables. For ordinal variables, I replaced the values manually in a manner that made intuitive sense. For nominal variables, I created dummies. This was not an issue in terms of memory usage because the cardinality of binary features is low, so only 2 dummies were created per nominal feature.

I did not create any interaction variables because no such combination made intuitive sense.

## Training Models and Evaluation Metrics

A significant part of the explanation in the project is devoted to justifying the choice of evaluation metrics. This was a combination of Recall and Precision with a slight preference for optimisation of the former. Briefly, the costs of high False Negatives is much greater than the cost of high False Positives for a company looking to improve their mental health initiatives, so optimising Recall is justified. However, Precision cannot be neglected because the cost of high False Positives would multiply very quickly as the number of employees increases, so this is a particular problem for larger organisations.

As stated, there is a detailed explanation in the work that elaborates further.

In terms of models, my approaches (selected) here included:

- BernoulliNB
- Decision Trees
- Support Vector Machines
- AdaBoost

I chose these models because they contain a good mix of model complexity and suitability for the problem.

# Results

I succeeded in the goal of improving upon the score of my baseline prediction. This had a Recall score of 100% but a Precision score of about 50%. The best performing model was BernoulliNB, which resulted in a Recall score of about 80% and a Precision score of 70%.

Using these scores, our model could detect the vast majority of people who actually have a mental illness (4 out of 5) while falsely predicting a small portion of individuals who do not have a mental illness, to have a mental illness. This minimises the annual budget (cost) a company would have to set aside because most of it would not be wasted on False Positives.

In terms of what could be improved upon, more advanced models such as neural networks could be used. More data could be obtained, as only 1200 or so observations existed. Richer data that is not binary in nature could also provide more predictive power.
