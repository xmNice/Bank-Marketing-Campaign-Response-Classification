Data Description: Bank-Marketing-Campaign-Response

The data is related with direct marketing campaigns of a Portuguese banking institution. 
The marketing campaigns were based on phone calls. 
Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed. 
Bank-full.csv dataset has 17 inputs, ordered by date.


=========================================
Goal: 
The classification goal is to predict if the client will subscribe (yes/no) a term deposit (variable y).

=========================================
Associated tasks:
A. Create the required dummy variables for the different predictors. Then Explore the data 
graphically in order to investigate the association between the response and the other 
features. Describe main findings.
B. Split the data into a training set and a test set separately for the successes and the 
failures.
C. Perform LDA, QDA, logistic regression, naive Bayes and KNN etc on the training data in 
order to predict response using the predictors.
D. Compare the performance of the different models in terms of the test errors, AUC for the 
different models.

=========================================
The Input Variables
1. age (numeric)
2. job : type of job (categorical: "admin.","bluecollar","entrepreneur","housemaid","management","retired","selfemployed","services","student","technician","unemployed","unknown")
3. marital : marital status (categorical: "divorced","married","single","unknown"; note: "divorced" 
means divorced or widowed)
4. education (categorical: 
"basic.4y","basic.6y","basic.9y","high.school","illiterate","professional.course",
"university.degree","unknown")
5. default: has credit in default? (categorical: "no","yes","unknown")
6. housing: has housing loan? (categorical: "no","yes","unknown")
7. loan: has personal loan? (categorical: "no","yes","unknown")
8. contact: contact communication type (categorical: "cellular","telephone") 
9. month: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
10. day_of_week: last contact day of the week (categorical: "mon","tue","wed","thu","fri")
11. duration: last contact duration, in seconds (numeric). 
Important note: this attribute highly affects 
the output target (e.g., if duration=0 then y="no"). Yet, the duration is not known before a call is 
performed. Also, after the end of the call y is obviously known. Thus, this input should only be 
included for benchmark purposes and should be discarded if the intention is to have a realistic 
predictive model.
12. campaign: number of contacts performed during this campaign and for this client (numeric, 
includes last contact)
13. pdays: number of days that passed by after the client was last contacted from a previous 
campaign (numeric; 999 means client was not previously contacted)
14. previous: number of contacts performed before this campaign and for this client (numeric)
15. poutcome: outcome of the previous marketing campaign (categorical: 
"failure","nonexistent","success")
16. emp.var.rate: employment variation rate - quarterly indicator (numeric)
17. cons.price.idx: consumer price index - monthly indicator (numeric) 
18. cons.conf.idx: consumer confidence index - monthly indicator (numeric) 
19. euribor3m: euribor 3 month rate - daily indicator (numeric)
20. nr.employed: number of employees - quarterly indicator (numeric)
21. Output variable (desired target): y - has the client subscribed a term deposit? (binary: "yes","no"

=========================================
About data leakage:
- Duration attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model. 

Data leakage (or leakage) happens when the training data contains information about the target, but similar data will not be available when the model is used for prediction.


=========================================
About the metrics:
The importance of precision vs. recall in a telephone campaign depends on the specific goals of the campaign:

Precision: This refers to the accuracy of identifying the right people to call.  High precision means a low rate of false positives - people who are unlikely to be interested being contacted. This is important for campaigns where it's crucial to avoid wasting time and resources on unproductive calls.

Recall: This refers to the completeness of identifying the right people to call.  High recall means a low rate of false negatives - missing people who might actually be interested. This is important for campaigns where reaching every potential customer is crucial.

A breakdown to help decide:

    Prioritize Precision if:
        The campaign has a limited budget or time for calls.
        Reaching the wrong people could damage the reputation (e.g., telemarketing for unwanted products).
        We have a good understanding of our target audience and can accurately identify potential customers.

    Prioritize Recall if:
        Reaching all potential customers is critical, even if some calls are unproductive.
        The cost of missing a potential customer outweighs the cost of some unproductive calls.
        We have a less clear understanding of our target audience and need to cast a wider net.

Finding the Balance:
In many cases, the ideal scenario is a balance between precision and recall.  Some strategies:

    (1) Machine Learning: Use data from past campaigns to train models that predict who is most likely to be receptive to our call.
    (2) Segmentation: Divide our target audience into subgroups with similar characteristics and tailor our approach for each segment.
    (3) Campaign Goals: Clearly define our campaign goals (e.g., maximize sales, increase brand awareness) to determine which metric (precision or recall) is more important.

Ultimately, the best approach depends on the specific context of the telephone campaign.


=========================================
Notebook contents:

      I Introduction
      II Data read and understanding
      III Data cleaning
      IV Exploratory data analysis (EDA)
          IV.1 Explore categorical variables
          IV.2 Explore numerical variables
          IV.3 Handle 'unknown' values and outliers
          IV.4 Milticollinearity and mutual information
          IV.5 PCA analysis
      V Model training
          V.1 Visualization with T-SNE
          V.2 Models trained with original X_train
          V.3 Models trained by adding PCA components
          V.4 Models trained with SMOTE-ENN over-sampling
          V.5 Performance evaluation
          V.6 Model interpretation
      VI Conclusion (work done, fingdings, difficuty, outlook )
