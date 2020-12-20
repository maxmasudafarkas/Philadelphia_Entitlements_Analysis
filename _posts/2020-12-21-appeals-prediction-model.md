---
title: "Zoning Appeals Decision Prediction Model"
date: 2020-12-21
published: true
tags: [dataviz]
excerpt: "Using scikit-learn to predict whether a zoning permit appeal will be approved or denied by the Philadelphia Zoning Board of Adjustment."
toc: true
toc_sticky: true
---

Like the Olympian government agencies portrayed in the stories of Franz Kafka, zoning boards are notorious for being unpredictable and impossible to bargain with, plead as one might. Acquiring the requisite permits and entitlements can create a great deal of uncertainty for small property owners and large developers alike, adding excess costs to a real estate development process that is already excessively costly.

This problem begs an important question: Are zoning decisions as unpredictable as they often appear to be? Stated differently, are there metrics, or "features," which we can use to predict whether an agency will give a zoning appeal its blessing? The machine learning model below would suggest that the answer is, oftentimes, yes.

## Step 1: Merging Appeals Decision Data with Property Data

To create a model that can predict whether a zoning appeal will be approved or denied based on a property's characteristics, we first need to create a central dataframe that combines (1) the ZBA appeals decisions and (2) data on each subject property. We already have the former in the L&I appeals dataset, and we can acquire the latter data through the Office of Property Assessment's (OPA) dataset on Philadelphia properties.

To integrate the OPA data into the appeals dataset, we will need to identify the column that is common to both sets. In the appeals dataset, this column is named "opa_account_num," and in the OPA dataset, it is listed as "parcel_number."

We can isolate the individual opa_account_num values as follows:

```python
opa_account_num = li_appeals_geo['opa_account_num'].dropna()
opa_account_num = opa_account_num.astype(int).astype(str)
opa_account_num = opa_account_num.tolist()
```

Once we have our list of relevant values, we can pull the OPA dataset using the Open Data Philly API and trim the dataset down to the properties with parcel_number values that match those of our above opa_account_num list:

```python
opa_raw = carto2gpd.get(open_data_philly_api, 'opa_properties_public')
opa_trimmed = opa_raw[(opa_raw['parcel_number'].isin(opa_account_num))==True]
```

Finally, we can then merge the trimmed OPA dataset into our original appeals dataset, leaving us with a central dataset containing both the appeals decisions and the features of each relevant property:

```python
li_appeals_opa = li_appeals_geo.merge(opa_trimmed, how="left", left_on='opa_account_num', right_on="parcel_number")
```

## Step 2: Processing the Appeals Decision Data

Next, we need to process the appeals data so that each appeals decision reflects a simple binary of either "approved" or "denied." In its raw form, the appeals dataset reflects a range of possible appeals decisions, which all fall into one of those two broad categories. We can see this range using the value_counts() function:

```python
li_appeals_opa['decision'].value_counts()
```

We can aggregate each of these variations of approvals and denials in the following lists:

```python
approved = [
    'AFFIRMED',
    'APPROVED'
    'Approved',
    'GRANTED',
    'GRANTED/PROV',
    'Granted',
    'ISSUED',
    'LATE-APPRVD',
    'NEWHEARYES',
    'SUSTAINED'
]

denied = [
    'DENIED',
    'DENIED/PROV',
    'DISMI/ENFORC',
    'DISMISSED',
    'Denied',
    'Dismissed',
    'HELD',
    'HELD/INFO',
    'LATE-DENIED',
    'Refused',
    'REFUSED',
    'WITHDRAWN',
    'Withdrawn'
]
```

To prepare the machine learning model, we can add a column to our dataframe that contains a binary 1 or 0 to indicate whether the subject property was approved (i.e. 1) or denied (i.e. 0):

```python
approved_sel = li_appeals_opa['decision'].isin(approved)

li_appeals_opa["decision_binary"] = 0
li_appeals_opa.loc[approved_sel, "decision_binary"] = 1
```

## Step 3: Building the Prediction Model with scikit-learn

Now that the dataset contains OPA property information and the appeals decision for each denoted by 1 or 0, building the prediction model requires choosing the individual property features that will be used to predict the appeals outcome. These features can be divided into numerical and categorical columns:

```python
numerical_columns = [
    "sale_price",
    "market_value",
    "total_area",
    "number_stories",
    "frontage",
    "taxable_building",
    "taxable_land",
    "total_livable_area"
]

categorical_columns = [
    "GEOID10",
    "exterior_condition",
    "interior_condition",
    "zip_code",
    "name",
    "zoning",
    "building_code",
    "building_code_description",
    "category_code",
    "category_code_description",
    "year_built"
]
```

We can then apply a column transformer to account for the two different types of features:

```python
transformer = ColumnTransformer(
    transformers=[
        ("num", StandardScaler(), numerical_columns),
        ("cat", OneHotEncoder(handle_unknown="ignore"), categorical_columns),
    ]
)
```
We can then divide the dataset into a 70/30 train-test split and apply a random forest model to create the appeals decision predictor. After optimizing for hyperparameters, we can evaluate the accuracy of the model:

```python
transformer = ColumnTransformer(
    transformers=[
        ("num", StandardScaler(), numerical_columns),
        ("cat", OneHotEncoder(handle_unknown="ignore"), categorical_columns),
    ]
)scores = cross_val_score(
    forest_pipe_grid,
    train_set,
    y_train,
    cv=3,
)

print("R^2 scores = ", scores)
print("Scores mean = ", scores.mean())
print("Score std dev = ", scores.std())
```
> R^2 scores =  [0.7398524  0.7337902  0.72614655]
> Scores mean =  0.7332630469161834
> Score std dev =  0.005607792443237735

A mean score of 0.733 indicates that our random forest model can serve as a fairly accurate tool to predict whether a zoning appeal will succeed or fail based on a given set of property characteristics. 
