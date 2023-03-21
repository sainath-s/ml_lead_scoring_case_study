**Problem Statement**

An education company named X Education sells online courses to industry professionals. On any given day, many professionals who are interested in the courses land on their website and browse for courses. 
<br/>
<br/>
The company markets its courses on several websites and search engines like Google. Once these people land on the website, they might browse the courses or fill up a form for the course or watch some videos. When these people fill up a form providing their email address or phone number, they are classified to be a lead. Moreover, the company also gets leads through past referrals. Once these leads are acquired, employees from the sales team start making calls, writing emails, etc. Through this process, some of the leads get converted while most do not. The typical lead conversion rate at X education is around 30%.
<br/>
<br/>
The company requires you to build a model wherein you need to assign a lead score to each of the leads such that the customers with a higher lead score have a higher conversion chance and the customers with a lower lead score have a lower conversion chance. The CEO, in particular, has given a ballpark of the target lead conversion rate to be around 80%.
<br/>
<br/>

We have went through the following steps
1. Data Cleaning
    * Handled Unkown values 'Select' which were present in many categorical columns
    * Dropped columns that are having more than 40% missing values
    * Dropped categorical columns which are having more than 80% class imbalance
    * Dropped Rows which are having less than 2% missing values
    * Performed Outlier Analysis on the Numerical Columns and limited the data to 99th percentile as the data more than 99th percentile were lessthan 2%
    * Performed Univariate analysis to check the distribution of data in Numerical and categorical columns
<br/>
<br/>

2. Data Preparation
    * created dummy variables for categorical columns
    * performed 80:20 train:test split
    * Performed Minmax feature scaling on numerical columns

<br/>
<br/>

3. Model Building and Evaluation
    * Started off with GLM from statsmodel and used RFE to perform feature selection and ended up with 15 estimators which are having p-value of < 0.05 and VIF is around 5
<br/>
<br/>

We have started building a logistic Regression Model starting with 60+ feature [after categorical variable conversion] and ended up 15 features with a Recall rate around 80%
<br/>
<br/>

using the ROC curve we evaluated the model performance  and through brute force calcuation of accuracy,sensitivit and specificity we have identified the threshold to be **0.35** for categorizing the leads as converted and not-converted

<br/>
<br/>

**Final Features** are:
'TotalVisits', 'Total Time Spent on Website','LeadOrigin_Landing Page Submission', 'LeadOrigin_Lead Add Form',
'LeadSource_Direct Traffic', 'LeadSource_Google','LeadSource_Organic Search', 'LeadSource_Referral Sites',
'LeadSource_Welingak Website', 'LastActivity_Had a Phone Conversation','LastActivity_SMS Sent', 'Specialization_Other',
'LastNotableActivity_Modified', 'LastNotableActivity_Olark Chat Conversation', 'LastNotableActivity_Unreachable'

<br/>
<br/>

**Observation:**
1. We got 15 features towards end of the training, Out of which 
    * Top 3 features which has a *postive effect* on the outcome is 
        * Total Time Spent on Website - coefficient 3.7857
        * LeadSource_Welingak Website - coefficient 2.7793
        * LastActivity_Had a Phone Conversation - coefficient 2.6726
    * Top 3 features which has a *negative effect* on the outcome is 
        * LeadSource_Referral Sites  - coefficient  -1.4605
        * LeadSource_Organic Search - coefficient -1.4441
        * LeadSource_Direct Traffic  - coefficient -1.4381
<br/>
<br/>


2. Metrics from the Train set are as below

    *  Accuracy                : 0.794333170493405
    *  Sensitivity             : 0.7962396152164407
    *  Specificty              : 0.7932018681888947
    *  FalsePositiveRate       : 0.20679813181110535
    *  PositivePredictiveValue : 0.6955691367456074
    *  NegativePredictiveValue : 0.867726369571388
    *  F1 Score                : 0.742507645259939

<br/>
<br/>

3. Metric from the Test set are as below

    * Accuracy                : 0.7978723404255319
    * Sensitivity             : 0.7786640079760718
    * Specificty              : 0.8096992019643954
    * FalsePositiveRate       : 0.19030079803560468
    * PositivePredictiveValue : 0.7158570119156737
    * NegativePredictiveValue : 0.8559377027903958
    * F1 Score                : 0.7459407831900668

<br/>
<br/>

4. From the model we can see that having phone conversation AND direct lead add form has a positive effect on the conversion .