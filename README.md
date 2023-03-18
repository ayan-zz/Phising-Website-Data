# Phishing Websites Features
One of the challenges faced by our research was the unavailability of reliable training datasets. In fact, this challenge faces any researcher in the field. However, although plenty of articles about predicting phishing websites using data mining techniques have been disseminated these days, no reliable training dataset has been published publically, maybe because there is no agreement in literature on the definitive features that characterize phishing websites, hence it is difficult to shape a dataset that covers all possible features.

In this article, we shed light on the important features that have proved to be sound and effective in predicting phishing websites. In addition, we proposed some new features, experimentally assign new rules to some well-known features and update some other features.
Features:
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







# Usage

See [action.yml](action.yml)

<!-- TODO: document custom workflow -->

# Artifact validation

While using this action is optional, we highly recommend it since it takes care of producing (mostly) valid artifacts.

A Pages artifact must:

- Be called `github-pages`
- Be a single [`gzip` archive][gzip] containing a single [`tar` file][tar]

The [`tar` file][tar] must:

- be under 10GB in size
- not contain any symbolic or hard links

# Release instructions

In order to release a new version of this Action:

1. Locate the semantic version of the [upcoming release][release-list] (a draft is maintained by the [`draft-release` workflow][draft-release]).

2. Publish the draft release from the `main` branch with semantic version as the tag name, _with_ the checkbox to publish to the GitHub Marketplace checked. :ballot_box_with_check:

3. After publishing the release, the [`release` workflow][release] will automatically run to create/update the corresponding the major version tag such as `v0`.

   ⚠️ Environment approval is required. Check the [Release workflow run list][release-workflow-runs].

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE).

<!-- references -->
[pages]: https://pages.github.com
[release-list]: https://github.com/actions/upload-pages-artifact/releases
[draft-release]: .github/workflows/draft-release.yml
[release]: .github/workflows/release.yml
[release-workflow-runs]: /actions/workflows/release.yml
[gzip]: https://en.wikipedia.org/wiki/Gzip
[tar]: https://en.wikipedia.org/wiki/Tar_(computing)
