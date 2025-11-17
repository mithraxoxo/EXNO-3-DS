## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT


            import pandas as pd
            df=pd.read_csv("Encoding Data.csv")
            df

<img width="490" height="349" alt="image" src="https://github.com/user-attachments/assets/5a20d441-a73e-4d33-8d68-92a4f8d347f8" />

            from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
            pm=['Hot','Warm','Cold']
            e1=OrdinalEncoder(categories=[pm])
            e1.fit_transform(df[["ord_2"]])

<img width="372" height="241" alt="image" src="https://github.com/user-attachments/assets/9da46015-d464-43ac-a9f6-4df6c9993563" />

    df['bo2']=e1.fit_transform(df[["ord_2"]])
    df

<img width="475" height="356" alt="image" src="https://github.com/user-attachments/assets/464a319f-60a0-4bce-b767-b9775d86e507" />

    le=LabelEncoder()
    dfc=df.copy()
    dfc['ord_2']=le.fit_transform(dfc['ord_2'])
    dfc
    
<img width="424" height="353" alt="image" src="https://github.com/user-attachments/assets/a87c7deb-864f-4583-8527-0fe1c7126f5e" />
    
    from sklearn.preprocessing import OneHotEncoder
    ohe=OneHotEncoder()
    df2=df.copy()
    enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
    df2=pd.concat([df2,enc],axis=1)
    df2
    
<img width="443" height="347" alt="image" src="https://github.com/user-attachments/assets/d77b4f8b-cdee-41ea-aa90-db5e2e301a6c" />

      pd.get_dummies(df2,columns=["nom_0"])           

<img width="697" height="367" alt="image" src="https://github.com/user-attachments/assets/83dc27cf-5cec-4751-9e6d-7e71d95ce214" />

    pip install --upgrade category_encoders

    from category_encoders import BinaryEncoder
    df=pd.read_csv("data.csv")
    df
    be=BinaryEncoder()
    nd=be.fit_transform(df['Ord_2'])
    df
    dfb=pd.concat([df,nd],axis=1)
    dfb    
<img width="808" height="367" alt="image" src="https://github.com/user-attachments/assets/59504766-b351-4dea-b3b1-2d8287485c5b" />


    
    from category_encoders import TargetEncoder
    te=TargetEncoder()
    CC=df.copy()
    new=te.fit_transform(X=CC["City"],y=CC["Target"])
    CC=pd.concat([CC,new],axis=1)
    CC

<img width="587" height="365" alt="image" src="https://github.com/user-attachments/assets/8580253f-563e-4c42-b0df-6108cf16c52d" />

    import pandas as pd
    from scipy import stats
    import numpy as np
    df=pd.read_csv("Data_to_Transform.csv")
    df 

<img width="835" height="433" alt="image" src="https://github.com/user-attachments/assets/df5a29e8-55a5-4fea-8922-6d570a62b479" />

    df.skew()    
<img width="394" height="116" alt="image" src="https://github.com/user-attachments/assets/da2b1f6c-0e30-42ac-9c9b-cbded754a374" />
    
    np.log(df["Highly Positive Skew"])
    
<img width="655" height="284" alt="image" src="https://github.com/user-attachments/assets/98c031f4-dbf2-4bfb-b86e-8306da2492fe" />

    np.reciprocal(df["Moderate Positive Skew"])

<img width="611" height="261" alt="image" src="https://github.com/user-attachments/assets/5bc6b552-0abf-43f7-837a-d99991fbc9b9" />

     np.sqrt(df["Highly Positive Skew"])    


<img width="638" height="260" alt="image" src="https://github.com/user-attachments/assets/6f359862-1de9-4aff-906d-b92707b6dc4a" />

     np.square(df["Highly Positive Skew"])

<img width="624" height="268" alt="image" src="https://github.com/user-attachments/assets/4076e6aa-d08f-4b73-be22-026accfcee2e" />

    df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
    df

<img width="1147" height="427" alt="image" src="https://github.com/user-attachments/assets/fdbc35f5-3223-43a0-be55-192cef2f190a" />


     df.skew()
 <img width="459" height="139" alt="image" src="https://github.com/user-attachments/assets/ed5f2ac5-63d8-46e8-82df-43e086b455e8" />
    
    df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
    df.skew() 
    
<img width="559" height="186" alt="image" src="https://github.com/user-attachments/assets/2aef12d8-cf60-4cdf-8e2e-88d5701c9bd0" />
    
    from sklearn.preprocessing import QuantileTransformer
    qt=QuantileTransformer(output_distribution='normal')
    df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
    df    
<img width="1250" height="430" alt="image" src="https://github.com/user-attachments/assets/1911ff01-5a09-40c5-9297-103fb8ecc4db" />

    import seaborn as sns
    import statsmodels.api as sm
    import matplotlib.pyplot as plt
    sm.qqplot(df["Moderate Negative Skew"],line='45')
    plt.show()

<img width="962" height="559" alt="image" src="https://github.com/user-attachments/assets/62d1c5aa-249b-44f0-bdb2-f262a3bcbae8" />

    sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
    plt.show()

<img width="794" height="545" alt="image" src="https://github.com/user-attachments/assets/59bf93f8-2d83-4429-986a-403bd5bc7148" />

from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()

<img width="811" height="545" alt="image" src="https://github.com/user-attachments/assets/10dcf24a-3b27-4024-ba64-26c898866837" />

df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line='45')
plt.show()   

<img width="754" height="530" alt="image" src="https://github.com/user-attachments/assets/500742f3-9fbc-44fc-8931-d9805ad5488f" />
    dt=pd.read_csv("titanic_dataset.csv")
    dt
<img width="1264" height="436" alt="image" src="https://github.com/user-attachments/assets/e5ccabf4-4baa-464d-9f25-782dcb501836" />
    
    
    from sklearn.preprocessing import QuantileTransformer
    qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
    dt["Age_1"]=qt.fit_transform(dt[["Age"]])
    sm.qqplot(dt['Age'],line='45') 
    plt.show()
  <img width="832" height="545" alt="image" src="https://github.com/user-attachments/assets/f742e7e0-28e0-40d7-b9d7-c110110596b3" />

    sm.qqplot(df["Highly Negative Skew_1"],line='45')
    plt
    
<img width="890" height="518" alt="image" src="https://github.com/user-attachments/assets/aa4f1d2f-7423-4894-9980-a700b3144494" />


    

     
# RESULT:
    
The code was run successfully.
       

 
