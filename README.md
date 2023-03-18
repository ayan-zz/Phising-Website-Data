![image](https://user-images.githubusercontent.com/64850346/226094629-98c97ece-a8f3-45e4-9a7d-977eaf93f1e3.png)


# Introduction:
A phishing website is a domain similar in name and appearance to an official website. They're made in order to fool someone into believing it is legitimate. The objective of this project is to perform EDA and feature engineering techniques in Task 1 and train machine learning models on the dataset created to predict phishing websites in Task 2. The datast is gathered from [UCI ML repo](https://archive.ics.uci.edu/ml/datasets/Phishing+Websites). 

## Phishing Websites Features
One of the challenges faced by our research was the unavailability of reliable training datasets. In fact, this challenge faces any researcher in the field. However, although plenty of articles about predicting phishing websites using data mining techniques have been disseminated these days, no reliable training dataset has been published publically, maybe because there is no agreement in literature on the definitive features that characterize phishing websites, hence it is difficult to shape a dataset that covers all possible features.

In this article, we shed light on the important features that have proved to be sound and effective in predicting phishing websites. In addition, we proposed some new features, experimentally assign new rules to some well-known features and update some other features.
Features:
```

'having_IP_Address', 
'URL_Length', 
'Shortining_Service',
'having_At_Symbol',
'double_slash_redirecting', 
'Prefix_Suffix',
'having_Sub_Domain',
'SSLfinal_State',
'Domain_registeration_length',
'Favicon', 
'port', 
'HTTPS_token', 
'Request_URL', 
'URL_of_Anchor',
'Links_in_tags', 
'SFH', 
'Submitting_to_email', 
'Abnormal_URL',
'Redirect', 
'on_mouseover', 
'RightClick', 
'popUpWidnow', 
'Iframe',
'age_of_domain',
'DNSRecord',
'web_traffic', 
'Page_Rank',
'Google_Index',
'Links_pointing_to_page', 
'Statistical_report',
'Result'
```
Detail of feature is available at [here](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Farchive.ics.uci.edu%2Fml%2Fmachine-learning-databases%2F00327%2FPhishing%2520Websites%2520Features.docx&wdOrigin=BROWSELINK)

# Data Ingestion 
From local system. Data format .arff type.
[Datalink](https://archive.ics.uci.edu/ml/machine-learning-databases/00327/)

### Importing necessary modules and libraries:
```

import pandas as pd
from scipy.io import arff
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
import warnings
warnings.filterwarnings('ignore')

```


### Loading and Reading the file and storing in a panda DataFrame
```
dff=arff.loadarff('Training Dataset.arff')
d1=pd.DataFrame(dff[0])
d1.head()

```
![image](https://user-images.githubusercontent.com/64850346/226087332-e30d54e8-921e-44a1-b3af-a40ae948d254.png)

```
print(d1.shape)
```
(11055, 31)

The column or feature variables are:
![image](https://user-images.githubusercontent.com/64850346/226087610-785134b1-77d7-4d77-8c94-7d7fb4be7844.png)

It is seen from the data set that the feature variable are having object data type which are classsified as:

* b'-1'
* b'0'
* b'1'

# EDA AND FEATURE ENGINEERING

### Check for null values:

![image](https://user-images.githubusercontent.com/64850346/226088030-df0dedd6-c07d-47a3-bb0d-e4cfdb9d5e85.png)

No null or nan type values are available. Data is clean

### Check for type of data types within the dataset

![image](https://user-images.githubusercontent.com/64850346/226087901-9d7ff786-467c-4d31-8041-10131eec7e0f.png)

NO numerical values within the dataset 

## Assumptions

![image](https://user-images.githubusercontent.com/64850346/226088212-6fbdb7fb-f990-4e23-8f0e-615566527432.png)

From the research paper it is found to be true that:
1. 1220 URLs lengths equals to 54 or more which constitute 48.8% of the total dataset size.
2. From URL_Anchor feature, we derive,
    Rule: IF {
    
      % of URL Of Anchor <31% → 𝐿𝑒𝑔𝑖𝑡𝑖𝑚𝑎𝑡𝑒
      
      % of URL Of Anchor ≥31% And≤67% → Suspicious 
      
      Otherwise→ Phishing
}

By approximation on % of feature variable distribution, we get:

b'-1' ---> Phising

b'0' ---> Suspicious

b'1' ---> Legitimate

### Replacing the string like objects into numerical values: 0,1,2

![image](https://user-images.githubusercontent.com/64850346/226088318-25bca0fc-8d2c-48bd-9a6e-b0729396263a.png)

Now all data are conveted into numerical values of 0,1 or 2

### Using pandas.get_dummy for dummy encoding and transformation of data of multivariate type to bivariate.
![image](https://user-images.githubusercontent.com/64850346/226088655-60bbf597-5f1f-49d5-bab1-3afc5bc643d7.png)
On careful observation we will see that the bivariate data are encoded into univariate datas with 2 features.
We will consider a single observation of the univariate data, this will explain the use of bivariate data (0/1) in a single column.

Dropping un-necessary dummy variables from the dataset.

![image](https://user-images.githubusercontent.com/64850346/226089298-7202ccc8-fad7-4103-9ce5-e6faa9e562f5.png)

![image](https://user-images.githubusercontent.com/64850346/226089326-e54d89a3-bf98-47f2-95d0-ec618df79dfd.png)

Now df_one dataset has modified dataset forfurther execution.

From research paper we get to know that the data has been grouped into 04 types of main feature characteristics as per the behaviour and location. They are :

* 1.1. Address Bar based Features
* 1.2. Abnormal Based Features
* 1.3. HTML and JavaScript based Features
* 1.4. Domain based Features
```

#HTML and JavaScript based Features
df_html=pd.DataFrame(df_one,columns=['Redirect_2','on_mouseover_1','RightClick_1','popUpWidnow_1', 'Iframe_1'])

#Abnormal Based Features
df_abnormal=pd.DataFrame(df_one,columns=['Request_URL_1','URL_of_Anchor_0','URL_of_Anchor_1', 'URL_of_Anchor_2', 'Links_in_tags_0',
       'Links_in_tags_1', 'Links_in_tags_2', 'SFH_0', 'SFH_1', 'SFH_2',
       'Submitting_to_email_1', 'Abnormal_URL_1'])
       
#Address Bar based Features
df_address=pd.DataFrame(df_one,columns=['having_IP_Address_1', 'URL_Length_0', 'URL_Length_1', 'URL_Length_2',
       'Shortining_Service_1', 'having_At_Symbol_1',
       'double_slash_redirecting_1', 'Prefix_Suffix_1', 'having_Sub_Domain_0',
       'having_Sub_Domain_1', 'having_Sub_Domain_2', 'SSLfinal_State_0',
       'SSLfinal_State_1', 'SSLfinal_State_2', 'Domain_registeration_length_1',
       'Favicon_1', 'port_1', 'HTTPS_token_1'])
       
#Domain based Features
df_domain=pd.DataFrame(df_one,columns=['age_of_domain_1', 'DNSRecord_1', 'web_traffic_0', 'web_traffic_1',
       'web_traffic_2', 'Page_Rank_1', 'Google_Index_1','Links_pointing_to_page_0', 'Links_pointing_to_page_1',
       'Links_pointing_to_page_2', 'Statistical_report_1'])
     
```
Plotting the same in seaborn:

![image](https://user-images.githubusercontent.com/64850346/226093724-71f8ab9a-9b67-44eb-9f61-78e2fb974d8b.png)

From the distribution it is evident to find some categories which are dominatng the main features.

Plotting multivariate data like URL_Length, Links_in_tags, web_traffic, URL_of_Anchor with the target variable 'Result'

![image](https://user-images.githubusercontent.com/64850346/226090633-6f11e459-72ba-466a-8e0a-2bd50eb03aeb.png)

![image](https://user-images.githubusercontent.com/64850346/226090674-67312ce3-7d4f-4fb4-a0a5-6b48d64e9ce5.png)

## Observations:

### 1. Url_length vs Result : Almost 55% of phising URL_Length are considered legitimate by target column. Around 40% phising URL_length are true to be phising data. About 45% of legitimate URL_Length data are considered phising. Suspicious type data are too minimum. 

### 2. Links_in_tags vs Result: Over 60% of phising Links_in_tags are considered as true to be phising. Round 38% data which are considered suspicious are true to be phising type. Below 45% data are phising for legitimate links

### 3. Web_Traffic vs Result: Phising data are equally distributed in phising and suspicious data types of Web_Traffic. Whereas for legitimate datas only about 27% data are contradicting to be phising.

### 4. URL_of_Anchor: Almost no contradiction found for phising data type of Url of Anchor. Around 27% of suspicious type data are found to be phising type. Where as rest are legitimate. Again below 5% data are found contradicting with legitimate type web_traffic feature.

### ---------TASK 2: TRAINING AND PREDICTION USING ML ALgos----------------------------------------------
### ---------To be continued-----------------------------------------------------------------------------
