```
#importing dependencies
import pandas as pd
import os
import numpy as np
from matplotlib import pyplot as plt
from scipy import stats
%matplotlib inline
import matplotlib
```

```
clinicalTrialData = pd.read_csv("raw_data/clinicaltrial_data.csv")
clinicalTrialData.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>f932</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>g107</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a457</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c819</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

```
clinicalTrialData.columns
```

    Index(['Mouse ID', 'Timepoint', 'Tumor Volume (mm3)', 'Metastatic Sites'], dtype='object')

```
mouseDrugData = pd.read_csv("raw_data/mouse_drug_data.csv")
mouseDrugData.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>f234</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>1</th>
      <td>x402</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a492</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>3</th>
      <td>w540</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>v764</td>
      <td>Stelasyn</td>
    </tr>
  </tbody>
</table>
</div>

```
#merge the two data
trialDataCombine_df = pd.merge(clinicalTrialData, mouseDrugData, how="outer", on="Mouse ID")
trialDataCombine_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>

```
fourdrug_trial_df = trialDataCombine_df.loc [(trialDataCombine_df["Drug"] == "Capomulin") | (trialDataCombine_df["Drug"] == "Infubinol") | (trialDataCombine_df["Drug"] == "Ketapril") | (trialDataCombine_df["Drug"] == "Placebo"), :]
fourdrug_trial_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>

```
fourDrugTrial_df = trialDataCombine_df.loc[(trialDataCombine_df["Drug"]== "Capomulin")|
(trialDataCombine_df["Drug"]=="Infubinol")|(trialDataCombine_df["Drug"]=="Ketapril") | (trialDataCombine_df["Drug"]== "Placebo"), :]
fourDrugTrial_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>

# Tumor Response To Treatment

```
tumorGroup_df = fourDrugTrial_df.groupby(["Drug", "Timepoint"])
tumorSem_df = pd.DataFrame(tumorGroup_df["Tumor Volume (mm3)"] .sem())
tumorSem_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tumor Volume (mm3)</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.448593</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.702684</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.838617</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.909731</td>
    </tr>
  </tbody>
</table>
</div>

```
#numpy Array for locating capomulin drug in Tumor volume (mm3)
capomulinYerr_df = tumorSem_df.loc["Capomulin", ["Tumor Volume (mm3)"]]
capomulinYerr = capomulinYerr_df.iloc[:, 0].values
capomulinYerr
```

    array([0.        , 0.44859285, 0.70268437, 0.83861725, 0.90973069,
           0.88164215, 0.93445951, 1.05224089, 1.22360839, 1.22397745])

```
#numpy Array for locating infubinol drug in Tumor volume (mm3)
infubinolYerr_df = tumorSem_df.loc["Infubinol", ["Tumor Volume (mm3)"]]
infubinolYerr = infubinolYerr_df.iloc[:, 0].values
infubinolYerr
```

    array([0.        , 0.2351023 , 0.28234591, 0.357705  , 0.47620951,
           0.55031457, 0.63106108, 0.98415494, 1.05521965, 1.14442738])

```
#numpy Array for locating ketapril drug in Tumor volume (mm3)
ketaprilYerr_df = tumorSem_df.loc["Ketapril", ["Tumor Volume (mm3)"]]
ketaprilYerr = infubinolYerr_df.iloc[:, 0].values
ketaprilYerr
```

    array([0.        , 0.2351023 , 0.28234591, 0.357705  , 0.47620951,
           0.55031457, 0.63106108, 0.98415494, 1.05521965, 1.14442738])

```
#numpy Array for locating placebo drug in Tumor volume (mm3)
placeboYerr_df = tumorSem_df.loc["Placebo", ["Tumor Volume (mm3)"]]
placeboYerr = placeboYerr_df.iloc[:, 0].values
placeboYerr
```

    array([0.        , 0.21809078, 0.40206381, 0.61446144, 0.83960917,
           1.03487199, 1.21823118, 1.2874806 , 1.37063404, 1.3517256 ])

```
#The mean value of the Tumor Volume (mm3)
tumorMean_df = pd.DataFrame(tumorGroup_df ["Tumor Volume (mm3)"].mean())
tumorMean_df.reset_index(inplace=True)
tumorMean_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>44.266086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>43.084291</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>42.064317</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>40.716325</td>
    </tr>
  </tbody>
</table>
</div>

```
#Renaming Tumor Volume column for capomulin drug to Capomulin
capomulin_df = tumorMean_df.loc[tumorMean_df["Drug"] =="Capomulin" , :]
capomulin_df
renameCapomulin_df = capomulin_df.rename(columns={"Tumor Volume (mm3)" : "Capomulin"})
renameCapomulin_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>44.266086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>43.084291</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>42.064317</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>40.716325</td>
    </tr>
  </tbody>
</table>
</div>

```
#Renaming Tumor Volume column for infubinol drug to Infubinol
infubinol_df = tumorMean_df.loc[tumorMean_df["Drug"] =="Infubinol" , :]
infubinol_df
renameInfubinol_df = infubinol_df.rename(columns={"Tumor Volume (mm3)" : "Infubinol"})
renameInfubinol_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Infubinol</td>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Infubinol</td>
      <td>5</td>
      <td>47.062001</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Infubinol</td>
      <td>10</td>
      <td>49.403909</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Infubinol</td>
      <td>15</td>
      <td>51.296397</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Infubinol</td>
      <td>20</td>
      <td>53.197691</td>
    </tr>
  </tbody>
</table>
</div>

```
#Renaming Tumor Volume column for capomulin drug to Ketapril
ketapril_df = tumorMean_df.loc[tumorMean_df["Drug"] =="Ketapril" , :]
ketapril_df
renameKetapril_df = ketapril_df.rename(columns={"Tumor Volume (mm3)" : "Ketapril"})
renameKetapril_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>47.389175</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>49.582269</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>52.399974</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>54.920935</td>
    </tr>
  </tbody>
</table>
</div>

```
#Renaming tumor volume for capomulin drug to Placebo
placebo_df = tumorMean_df.loc[tumorMean_df["Drug"] =="Placebo" , :]
placebo_df
renamePlacebo_df = placebo_df.rename(columns={"Tumor Volume (mm3)" : "Placebo"})
renamePlacebo_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>30</th>
      <td>Placebo</td>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Placebo</td>
      <td>5</td>
      <td>47.125589</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Placebo</td>
      <td>10</td>
      <td>49.423329</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Placebo</td>
      <td>15</td>
      <td>51.359742</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Placebo</td>
      <td>20</td>
      <td>54.364417</td>
    </tr>
  </tbody>
</table>
</div>

```
#merging Data Frames of various drugs(continue tomorrow)
firstMerge_df = pd.merge(renameCapomulin_df, renameInfubinol_df, on = "Timepoint")
firstMerge_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>45.000000</td>
      <td>Infubinol</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>44.266086</td>
      <td>Infubinol</td>
      <td>47.062001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>43.084291</td>
      <td>Infubinol</td>
      <td>49.403909</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>42.064317</td>
      <td>Infubinol</td>
      <td>51.296397</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>40.716325</td>
      <td>Infubinol</td>
      <td>53.197691</td>
    </tr>
  </tbody>
</table>
</div>

```
secondMerge_df = pd.merge(renameKetapril_df, renamePlacebo_df, on = "Timepoint")
secondMerge_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
      <th>Drug_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>45.000000</td>
      <td>Placebo</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>47.389175</td>
      <td>Placebo</td>
      <td>47.125589</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>49.582269</td>
      <td>Placebo</td>
      <td>49.423329</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>52.399974</td>
      <td>Placebo</td>
      <td>51.359742</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>54.920935</td>
      <td>Placebo</td>
      <td>54.364417</td>
    </tr>
  </tbody>
</table>
</div>

```
finalMerge_df = pd.merge(firstMerge_df, secondMerge_df, on = "Timepoint")
finalMerge_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y_x</th>
      <th>Infubinol</th>
      <th>Drug_x_y</th>
      <th>Ketapril</th>
      <th>Drug_y_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>45.000000</td>
      <td>Infubinol</td>
      <td>45.000000</td>
      <td>Ketapril</td>
      <td>45.000000</td>
      <td>Placebo</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>44.266086</td>
      <td>Infubinol</td>
      <td>47.062001</td>
      <td>Ketapril</td>
      <td>47.389175</td>
      <td>Placebo</td>
      <td>47.125589</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>43.084291</td>
      <td>Infubinol</td>
      <td>49.403909</td>
      <td>Ketapril</td>
      <td>49.582269</td>
      <td>Placebo</td>
      <td>49.423329</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>42.064317</td>
      <td>Infubinol</td>
      <td>51.296397</td>
      <td>Ketapril</td>
      <td>52.399974</td>
      <td>Placebo</td>
      <td>51.359742</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>40.716325</td>
      <td>Infubinol</td>
      <td>53.197691</td>
      <td>Ketapril</td>
      <td>54.920935</td>
      <td>Placebo</td>
      <td>54.364417</td>
    </tr>
  </tbody>
</table>
</div>

```
#finally finding tumor response for all 4 drugs
tumorResponse_df=finalMerge_df[["Timepoint", "Capomulin", "Infubinol", "Ketapril", "Placebo"]]
tumorResponse_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>44.266086</td>
      <td>47.062001</td>
      <td>47.389175</td>
      <td>47.125589</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>43.084291</td>
      <td>49.403909</td>
      <td>49.582269</td>
      <td>49.423329</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>42.064317</td>
      <td>51.296397</td>
      <td>52.399974</td>
      <td>51.359742</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>40.716325</td>
      <td>53.197691</td>
      <td>54.920935</td>
      <td>54.364417</td>
    </tr>
  </tbody>
</table>
</div>

```
#plotting the Capomulin line
ax = tumorResponse_df.plot(kind='scatter', x='Timepoint',y='Capomulin', linestyle='--', color='red', marker='o', yerr=capomulinYerr);
ax.errorbar(x=tumorResponse_df['Timepoint'],y=tumorResponse_df['Capomulin'], yerr=capomulinYerr, fmt='o', mfc='r', mec='k', ms=6, mew=1, linestyle='--',alpha=0.5, label="Capomulin")

#plotting the Infubinol line
tumorResponse_df.plot(kind='scatter', x='Timepoint', y='Infubinol', linestyle='--', color='DarkGreen', marker='d', yerr = infubinolYerr, ax=ax);
ax.errorbar(x=tumorResponse_df['Timepoint'],y=tumorResponse_df['Infubinol'], yerr=infubinolYerr, fmt='x', mfc='b', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Infubinol")

#plotting the Ketapril line
tumorResponse_df.plot(kind='scatter', x='Timepoint', y='Ketapril', linestyle='--', color='blue', marker='x',  yerr = ketaprilYerr,  ax=ax);
ax.errorbar(x=tumorResponse_df['Timepoint'],y=tumorResponse_df['Ketapril'], yerr=ketaprilYerr, fmt='+', mfc='g', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Ketapril")

#plotting the Placebo line
tumorResponse_df.plot(kind='scatter', x='Timepoint', y='Placebo', linestyle='--', color='black', marker='s',  yerr = placeboYerr,  ax=ax);
ax.errorbar(x=tumorResponse_df['Timepoint'],y=tumorResponse_df['Placebo'], yerr=placeboYerr, fmt='s', mfc='y', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Placebo")

xlim = ax.get_xlim()
factor = 0.1
new_xlim = (xlim[0] + xlim[1])/2 + np.array((-0.5, 0.5)) * (xlim[1] - xlim[0]) * (1 + factor)
ax.set_xlim(new_xlim)
ax.grid()
ax.set_xlabel("Time(days)")
ax.set_ylabel("Tumor Volume (mm3)")
ax.set_title("Tumor response to treatment")
legend = ax.legend(loc='best', shadow=True)
handles, labels = ax.get_legend_handles_labels()
ax.legend(handles, labels )
plt.savefig("tumor_response_to_treatment.png")
plt.show()
```

![png](output_22_0.png)

# Metastic (Cancer Spreading) Response to Treatment

```
metastasisMean_df = pd.DataFrame(tumorGroup_df ["Metastatic Sites"] .mean())
metastasisMean_df.reset_index(inplace=True)
metastasisMean_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Metastatic Sites</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>0.160000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>0.320000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>0.652174</td>
    </tr>
  </tbody>
</table>
</div>

```
Capomulin_df1=metastasisMean_df.loc[metastasisMean_df["Drug"]=="Capomulin",:]
Capomulin_df1
rename_Capomulin_df1 = Capomulin_df1.rename(columns={"Metastatic Sites":"Capomulin"})
rename_Capomulin_df1.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>0.160000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>0.320000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>0.652174</td>
    </tr>
  </tbody>
</table>
</div>

```
Infubinol_df1=metastasisMean_df.loc[metastasisMean_df["Drug"]=="Infubinol",:]
Infubinol_df1
rename_Infubinol_df1 = Infubinol_df1.rename(columns={"Metastatic Sites":"Infubinol"})
rename_Infubinol_df1.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Infubinol</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Infubinol</td>
      <td>5</td>
      <td>0.280000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Infubinol</td>
      <td>10</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Infubinol</td>
      <td>15</td>
      <td>0.904762</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Infubinol</td>
      <td>20</td>
      <td>1.050000</td>
    </tr>
  </tbody>
</table>
</div>

```
Ketapril_df1=metastasisMean_df.loc[metastasisMean_df["Drug"]=="Ketapril",:]
Ketapril_df1
rename_Ketapril_df1 = Ketapril_df1.rename(columns={"Metastatic Sites":"Ketapril"})
rename_Ketapril_df1.head()

```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>0.304348</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>0.590909</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>0.842105</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>1.210526</td>
    </tr>
  </tbody>
</table>
</div>

```
Placebo_df1=metastasisMean_df.loc[metastasisMean_df["Drug"]=="Placebo",:]
Placebo_df1
rename_Placebo_df1 = Placebo_df1.rename(columns={"Metastatic Sites":"Placebo"})
rename_Placebo_df1.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>30</th>
      <td>Placebo</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Placebo</td>
      <td>5</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Placebo</td>
      <td>10</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Placebo</td>
      <td>15</td>
      <td>1.250000</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Placebo</td>
      <td>20</td>
      <td>1.526316</td>
    </tr>
  </tbody>
</table>
</div>

```
meger1_df1=pd.merge(rename_Capomulin_df1, rename_Infubinol_df1, on="Timepoint")
meger1_df1.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>0.000000</td>
      <td>Infubinol</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>0.160000</td>
      <td>Infubinol</td>
      <td>0.280000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>0.320000</td>
      <td>Infubinol</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>0.375000</td>
      <td>Infubinol</td>
      <td>0.904762</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>0.652174</td>
      <td>Infubinol</td>
      <td>1.050000</td>
    </tr>
  </tbody>
</table>
</div>

```
meger2_df1=pd.merge(rename_Ketapril_df1, rename_Placebo_df1, on="Timepoint")
meger2_df1.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
      <th>Drug_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>0.000000</td>
      <td>Placebo</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>0.304348</td>
      <td>Placebo</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>0.590909</td>
      <td>Placebo</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>0.842105</td>
      <td>Placebo</td>
      <td>1.250000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>1.210526</td>
      <td>Placebo</td>
      <td>1.526316</td>
    </tr>
  </tbody>
</table>
</div>

```
finalMerge = pd.merge(meger1_df1, meger2_df1, on="Timepoint")
finalMerge.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y_x</th>
      <th>Infubinol</th>
      <th>Drug_x_y</th>
      <th>Ketapril</th>
      <th>Drug_y_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>0.000000</td>
      <td>Infubinol</td>
      <td>0.000000</td>
      <td>Ketapril</td>
      <td>0.000000</td>
      <td>Placebo</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>0.160000</td>
      <td>Infubinol</td>
      <td>0.280000</td>
      <td>Ketapril</td>
      <td>0.304348</td>
      <td>Placebo</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>0.320000</td>
      <td>Infubinol</td>
      <td>0.666667</td>
      <td>Ketapril</td>
      <td>0.590909</td>
      <td>Placebo</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>0.375000</td>
      <td>Infubinol</td>
      <td>0.904762</td>
      <td>Ketapril</td>
      <td>0.842105</td>
      <td>Placebo</td>
      <td>1.250000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>0.652174</td>
      <td>Infubinol</td>
      <td>1.050000</td>
      <td>Ketapril</td>
      <td>1.210526</td>
      <td>Placebo</td>
      <td>1.526316</td>
    </tr>
  </tbody>
</table>
</div>

```
Metastatic_change_df=finalMerge[["Timepoint", "Capomulin", "Infubinol", "Ketapril", "Placebo"]]
Metastatic_change_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>0.160000</td>
      <td>0.280000</td>
      <td>0.304348</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>0.320000</td>
      <td>0.666667</td>
      <td>0.590909</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>0.375000</td>
      <td>0.904762</td>
      <td>0.842105</td>
      <td>1.250000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>0.652174</td>
      <td>1.050000</td>
      <td>1.210526</td>
      <td>1.526316</td>
    </tr>
  </tbody>
</table>
</div>

```
Metastatic_change_df['Timepoint'] = Metastatic_change_df['Timepoint'].astype(float)
Metastatic_change_df.dtypes
```

    /Users/samuelappiah/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.





    Timepoint    float64
    Capomulin    float64
    Infubinol    float64
    Ketapril     float64
    Placebo      float64
    dtype: object

```
Metastasis_sem_df = pd.DataFrame(tumorGroup_df ["Metastatic Sites"].sem())
Metastasis_sem_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Metastatic Sites</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Capomulin</th>
      <th>0</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.074833</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.125433</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.132048</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.161621</td>
    </tr>
  </tbody>
</table>
</div>

```
Capomulin_yerr_df1=Metastasis_sem_df.loc['Capomulin',["Metastatic Sites"]]
Capomulin_yerr1=Capomulin_yerr_df1.iloc[:, 0].values
Capomulin_yerr1
```

    array([0.        , 0.07483315, 0.12543258, 0.1320477 , 0.16162094,
           0.18181818, 0.17294359, 0.16949586, 0.17561037, 0.20259093])

```
Infubinol_yerr_df=Metastasis_sem_df.loc['Infubinol',["Metastatic Sites"]]
Infubinol_yerr1= Infubinol_yerr_df.iloc[:, 0].values
Infubinol_yerr1
```

    array([0.        , 0.09165151, 0.15936381, 0.19401475, 0.23480115,
           0.26575279, 0.22782255, 0.22473329, 0.31446604, 0.30932024])

```
Ketapril_yerr_df1=Metastasis_sem_df.loc['Ketapril',["Metastatic Sites"]]
Ketapril_yerr1=Ketapril_yerr_df1.iloc[:, 0].values
Ketapril_yerr1
```

    array([0.        , 0.09810019, 0.1420184 , 0.19138091, 0.23667961,
           0.28827503, 0.34746723, 0.36141782, 0.31572542, 0.27872199])

```
Placebo_yerr_df1=Metastasis_sem_df.loc['Placebo',["Metastatic Sites"]]
Placebo_yerr1=Placebo_yerr_df1.iloc[:, 0].values
Placebo_yerr1
```

    array([0.        , 0.10094661, 0.11526068, 0.19022148, 0.23406428,
           0.26388762, 0.30026443, 0.34141179, 0.2972942 , 0.30424001])

```
plt.figure(figsize=(20,3))
#Plotting metastic changes in capomullin
ax=Metastatic_change_df.plot(kind='scatter', x='Timepoint',y='Capomulin', linestyle='--', color=
'red', marker='o', yerr=Capomulin_yerr1);
ax.errorbar(x=Metastatic_change_df['Timepoint'],y=Metastatic_change_df['Capomulin'],
yerr=Capomulin_yerr1, fmt='o', mfc='r', mec='k', ms=6, mew=1, linestyle='--',alpha=0.5, label="Capomulin" )

#Plotting metastic changes in Infubinol
Metastatic_change_df.plot(kind='scatter', x='Timepoint', y='Infubinol', linestyle='--', color=
'DarkGreen', marker='d', yerr = Infubinol_yerr1, ax=ax);
ax.errorbar(x=Metastatic_change_df['Timepoint'],y=Metastatic_change_df['Infubinol'],
yerr=Infubinol_yerr1, fmt='x', mfc='b', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Infubinol")

#Plotting metastic changes in Ketapril
Metastatic_change_df.plot(kind='scatter', x='Timepoint', y='Ketapril', linestyle='--', color=
'blue', marker='x',  yerr = Ketapril_yerr1,  ax=ax);
ax.errorbar(x=Metastatic_change_df['Timepoint'],y=Metastatic_change_df['Ketapril'],
yerr=Ketapril_yerr1, fmt='+', mfc='g', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Ketapril")

#Plotting metastic changes in Placebo
Metastatic_change_df.plot(kind='scatter', x='Timepoint', y='Placebo', linestyle='--', color=
'black', marker='s',  yerr = Placebo_yerr1,  ax=ax);
ax.errorbar(x=Metastatic_change_df['Timepoint'],y=Metastatic_change_df['Placebo'],
yerr=Placebo_yerr1, fmt='s', mfc='y', mec='k', ms=6, mew=1, linestyle='--', alpha=0.5, label="Placebo")

#plotting them
xlim = ax.get_xlim()
factor = 0.1
new_xlim = (xlim[0] + xlim[1])/2 + np.array((-0.5, 0.5)) * (xlim[1] - xlim[0]) * (1 + factor)
ax.set_xlim(new_xlim)

ax.grid()
ax.set_xlabel("Treatment Duration(days)")
ax.set_ylabel("Metastatic sites")
ax.set_title("Metastatic spread during treatment")
legend = ax.legend(loc='best', shadow=True)
handles, labels = ax.get_legend_handles_labels()
ax.legend(handles, labels )
plt.savefig("Metastatic_spread_during_treatment.png")
plt.show()
```

    <matplotlib.figure.Figure at 0x1a165eb4a8>

![png](output_39_1.png)

# Survival Rate

```
mice_count_df=pd.DataFrame(tumorGroup_df["Mouse ID"].count())
mice_count_df.reset_index(inplace=True)
mice_count_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Mouse ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>

```
Capomulin_df2=mice_count_df.loc[mice_count_df["Drug"]=="Capomulin",:]
Capomulin_df2
rename_Capomulin_df2 = Capomulin_df2.rename(columns={"Mouse ID":"Capomulin"})
rename_Capomulin_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>

```
Infubinol_df2=mice_count_df.loc[mice_count_df["Drug"]=="Infubinol",:]
Infubinol_df2
rename_Infubinol_df2 = Infubinol_df2.rename(columns={"Mouse ID":"Infubinol"})
rename_Infubinol_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Infubinol</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Infubinol</td>
      <td>5</td>
      <td>25</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Infubinol</td>
      <td>10</td>
      <td>21</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Infubinol</td>
      <td>15</td>
      <td>21</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Infubinol</td>
      <td>20</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>

```
Ketapril_df2=mice_count_df.loc[mice_count_df["Drug"]=="Ketapril",:]
Ketapril_df2
rename_Ketapril_df2 = Ketapril_df2.rename(columns={"Mouse ID":"Ketapril"})
rename_Ketapril_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>23</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>22</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>19</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```
Placebo_df2=mice_count_df.loc[mice_count_df["Drug"]=="Placebo",:]
Placebo_df2
rename_Placebo_df2 = Placebo_df2.rename(columns={"Mouse ID":"Placebo"})
rename_Placebo_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug</th>
      <th>Timepoint</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>30</th>
      <td>Placebo</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Placebo</td>
      <td>5</td>
      <td>24</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Placebo</td>
      <td>10</td>
      <td>24</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Placebo</td>
      <td>15</td>
      <td>20</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Placebo</td>
      <td>20</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```
meger1_df2=pd.merge(rename_Capomulin_df2, rename_Infubinol_df2, on="Timepoint")
meger1_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y</th>
      <th>Infubinol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>24</td>
      <td>Infubinol</td>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>23</td>
      <td>Infubinol</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>

```
meger2_df2=pd.merge(rename_Ketapril_df2, rename_Placebo_df2, on="Timepoint")
meger2_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x</th>
      <th>Timepoint</th>
      <th>Ketapril</th>
      <th>Drug_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ketapril</td>
      <td>0</td>
      <td>25</td>
      <td>Placebo</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ketapril</td>
      <td>5</td>
      <td>23</td>
      <td>Placebo</td>
      <td>24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ketapril</td>
      <td>10</td>
      <td>22</td>
      <td>Placebo</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ketapril</td>
      <td>15</td>
      <td>19</td>
      <td>Placebo</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ketapril</td>
      <td>20</td>
      <td>19</td>
      <td>Placebo</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```
merge3_df2 = pd.merge(meger1_df2, meger2_df2, on="Timepoint")
merge3_df2.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Drug_x_x</th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Drug_y_x</th>
      <th>Infubinol</th>
      <th>Drug_x_y</th>
      <th>Ketapril</th>
      <th>Drug_y_y</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Capomulin</td>
      <td>0</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>25</td>
      <td>Ketapril</td>
      <td>25</td>
      <td>Placebo</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Capomulin</td>
      <td>5</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>25</td>
      <td>Ketapril</td>
      <td>23</td>
      <td>Placebo</td>
      <td>24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Capomulin</td>
      <td>10</td>
      <td>25</td>
      <td>Infubinol</td>
      <td>21</td>
      <td>Ketapril</td>
      <td>22</td>
      <td>Placebo</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Capomulin</td>
      <td>15</td>
      <td>24</td>
      <td>Infubinol</td>
      <td>21</td>
      <td>Ketapril</td>
      <td>19</td>
      <td>Placebo</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Capomulin</td>
      <td>20</td>
      <td>23</td>
      <td>Infubinol</td>
      <td>20</td>
      <td>Ketapril</td>
      <td>19</td>
      <td>Placebo</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```
survive_rate_df=merge3_df2[["Timepoint", "Capomulin", "Infubinol", "Ketapril", "Placebo"]]
survive_rate_df.head()
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Placebo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>25</td>
      <td>25</td>
      <td>25</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>25</td>
      <td>25</td>
      <td>23</td>
      <td>24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>25</td>
      <td>21</td>
      <td>22</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>24</td>
      <td>21</td>
      <td>19</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>23</td>
      <td>20</td>
      <td>19</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>

```
survive_rate_df = survive_rate_df.astype(float)
survive_rate_df.dtypes
```

    Timepoint    float64
    Capomulin    float64
    Infubinol    float64
    Ketapril     float64
    Placebo      float64
    dtype: object

```
survive_rate_df["Capomulin_percent"]=survive_rate_df["Capomulin"]/survive_rate_df["Capomulin"].iloc[0] * 100

survive_rate_df["Infubinol_percent"]=survive_rate_df["Infubinol"]/survive_rate_df["Infubinol"].iloc[0] * 100

survive_rate_df["Ketapril_percent"]=survive_rate_df["Ketapril"]/survive_rate_df["Ketapril"].iloc[0] * 100

survive_rate_df["Placebo_percent"]=survive_rate_df["Placebo"]/survive_rate_df["Placebo"].iloc[0] * 100

survive_rate_df
```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Timepoint</th>
      <th>Capomulin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Placebo</th>
      <th>Capomulin_percent</th>
      <th>Infubinol_percent</th>
      <th>Ketapril_percent</th>
      <th>Placebo_percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>23.0</td>
      <td>24.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>92.0</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10.0</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>22.0</td>
      <td>24.0</td>
      <td>100.0</td>
      <td>84.0</td>
      <td>88.0</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15.0</td>
      <td>24.0</td>
      <td>21.0</td>
      <td>19.0</td>
      <td>20.0</td>
      <td>96.0</td>
      <td>84.0</td>
      <td>76.0</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20.0</td>
      <td>23.0</td>
      <td>20.0</td>
      <td>19.0</td>
      <td>19.0</td>
      <td>92.0</td>
      <td>80.0</td>
      <td>76.0</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25.0</td>
      <td>22.0</td>
      <td>18.0</td>
      <td>19.0</td>
      <td>17.0</td>
      <td>88.0</td>
      <td>72.0</td>
      <td>76.0</td>
      <td>68.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>30.0</td>
      <td>22.0</td>
      <td>17.0</td>
      <td>18.0</td>
      <td>15.0</td>
      <td>88.0</td>
      <td>68.0</td>
      <td>72.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>35.0</td>
      <td>22.0</td>
      <td>12.0</td>
      <td>17.0</td>
      <td>14.0</td>
      <td>88.0</td>
      <td>48.0</td>
      <td>68.0</td>
      <td>56.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>40.0</td>
      <td>21.0</td>
      <td>10.0</td>
      <td>15.0</td>
      <td>12.0</td>
      <td>84.0</td>
      <td>40.0</td>
      <td>60.0</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>45.0</td>
      <td>21.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>11.0</td>
      <td>84.0</td>
      <td>36.0</td>
      <td>44.0</td>
      <td>44.0</td>
    </tr>
  </tbody>
</table>
</div>

```
ax=survive_rate_df.plot(kind='line', x='Timepoint',y='Capomulin_percent', linestyle='--', color=
'red', marker='o', alpha=0.5, label="Capomulin");

survive_rate_df.plot(kind='line', x='Timepoint', y='Infubinol_percent', linestyle='--', color=
'DarkGreen', marker='d', ax=ax, alpha=0.5, label="Infubinol");

survive_rate_df.plot(kind='line', x='Timepoint', y='Ketapril_percent', linestyle='--', color=
'blue', marker='x',  ax=ax,  alpha=0.5, label="Ketapril");

survive_rate_df.plot(kind='line', x='Timepoint', y='Placebo_percent', linestyle='--', color=
'black', marker='s', ax=ax,  alpha=0.5, label="Placebo");

ax.set_xlim(0, 45, 5)
ax.set_ylim(30, 110)
ax.grid()
ax.set_xlabel("Times(days)")
ax.set_ylabel("Survival Rate Percent(%)")
ax.set_title("Survival during Treatment")
legend = ax.legend(loc='best', shadow=True)
handles, labels = ax.get_legend_handles_labels()
ax.legend(handles, labels )
plt.savefig("Survival_during_treatment.png")
plt.show()
```

![png](output_52_0.png)

# Summary Bar Graph

```
Capomulin_tumorvolume_changepercent=(tumorResponse_df["Capomulin"].iloc[9]-tumorResponse_df
["Capomulin"].iloc[0])/tumorResponse_df["Capomulin"].iloc[0]*100

Capomulin_tumorvolume_changepercent
```

    -19.475302667894155

```
Infubinol_tumorvolume_changepercent=(tumorResponse_df["Infubinol"].iloc[9]-tumorResponse_df
["Infubinol"].iloc[0])/tumorResponse_df["Infubinol"].iloc[0]*100

Infubinol_tumorvolume_changepercent
```

    46.12347172785184

```
Ketapril_tumorvolume_changepercent=(tumorResponse_df["Ketapril"].iloc[9]-tumorResponse_df
["Ketapril"].iloc[0])/tumorResponse_df["Ketapril"].iloc[0]*100

Ketapril_tumorvolume_changepercent
```

    57.02879468660604

```
Placebo_tumorvolume_changepercent=(tumorResponse_df["Placebo"].iloc[9]-tumorResponse_df
["Placebo"].iloc[0])/tumorResponse_df["Placebo"].iloc[0]*100

Placebo_tumorvolume_changepercent
```

    51.29796048315153

```
d = {'Capomulin': Capomulin_tumorvolume_changepercent, 'Infubinol': Infubinol_tumorvolume_changepercent, 'Ketapril': Ketapril_tumorvolume_changepercent, 'Placebo': Placebo_tumorvolume_changepercent}
totaltumor_volume_change = pd.Series(d)
totaltumor_volume_change
```

    Capomulin    46.123472
    Infubinol    46.123472
    Ketapril     57.028795
    Placebo      51.297960
    dtype: float64

```
drug=totaltumor_volume_change.keys()
drug
```

    Index(['Capomulin', 'Infubinol', 'Ketapril', 'Placebo'], dtype='object')

```
ax = plt.subplot()
x_axis = np.arange(0, len(drug))
tick_locations = []
for x in x_axis:
    tick_locations.append(x + 0.4)

plt.title("Tumor Change Over 45 Days Treatment")
plt.ylabel("% Tumor Volume Change")

plt.xlim(-0.25, len(drug))
plt.ylim(-30, max(totaltumor_volume_change) + 10)
plt.grid(True, linestyle='dashed')

plt.xticks(tick_locations, drug)

width = 0.4
vals = [1,2,3,4,5]
colors = ['r','b','b','b','b']
colors = []
for value in totaltumor_volume_change:
    if value >= 0 :
        colors.append('y')
    else:
        colors.append('g')
percents=ax.bar(x_axis, totaltumor_volume_change, color=colors, alpha=0.75, align="edge")
def autolabel(percents, ax):

    (y_bottom, y_top) = ax.get_ylim()
    y_height = y_top - y_bottom
    for percent in percents:
        height = percent.get_height()

        ax.text(percent.get_x()+ percent.get_width()/2., 0.5*height, '%d' % int(height) +"%", ha='center', va='center')

autolabel(percents, ax)

plt.savefig("TumorChange_Over_45_Days_Treatment.png")
plt.show()
```

![png](output_60_0.png)
