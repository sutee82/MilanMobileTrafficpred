# Datasheet

## Motivation

* **For what purpose was the dataset created?**
    The main portion of the dataset was created to provide a multi-source view of urban life in Milan and Trentino. Its purpose is to support the study of socio-technical systems and enable research on a wide range of urban challenges, including energy consumption, mobility planning, event detection, and, as in this project, telecommunication demand.
    In addtion the public holiday portion of hte dataset was created using Generative AI . 

* **Who created the dataset and on behalf of which entity? Who funded the creation?**
    The dataset was created by Gianni Barlacchi, Marco De Nadai, Roberto Larcher, et al. It was published as part of a collaboration for the Telecom Italia Big Data Challenge, which involved Telecom Italia, EIT ICT Labs, SpazioDati, MIT Media Lab, Northeastern University, Polytechnic University of Milan, Fondazione Bruno Kessler, University of Trento, and Trento RISE. The funding sources are unkown. 

## Composition

* **What do the instances that comprise the dataset represent?**
    The instances represent aggregated measurements for specific geographic areas (grid squares) in Milan over 10-minute intervals. Each instance includes:
    * **Call Detail Records (CDRs):** Aggregated SMS, call, and internet activity.
    * **Meteorological Data:** Information on precipitation type (none, snow, rain) and intensity.
    * **National Holidays:** A list of public holidays for the Milan region.

* **How many instances of each type are there?**
    The original dataset uses 10000 grid squares of Milan (This project uses data from the central 2500 grid squares of Milan) over a two-month period, with records generated every 10 minutes. The total number of instances would be the result of `2500 (grids) * 6 (10-min intervals per hour) * 24 (hours) * 61 (days)`.

* **Is there any missing data?**
    The provided text does not explicitly mention missing data in the raw dataset but describes preprocessing steps to handle and clean the data, which would implicitly address any gaps.

* **Does the dataset contain data that might be considered confidential?**
    No. The Call Detail Records (CDRs) have been aggregated and anonymized to protect individual privacy. The data represents collective activity within a grid square, not the behavior of specific individuals.

## Collection process

* **How was the data acquired?**
    The Telecommunication data was originally collected and provided by Telecom Italia for the "Telecom Italia Big Data Challenge 2014." The weather data was collected by ARPA (http://www.arpa.piemonte.it/rischinaturali) and by Meteotrentino. The weather data was gereated by Gemini 2.5.

* **If the data is a sample of a larger subset, what was the sampling strategy?**
    The dataset used in this project is a spatial sample of the complete Milan dataset. The data was filtered to the central 2500 grid squares to focus on the most active urban core and improve computational efficiency.

* **Over what time frame was the data collected?**
    The data was collected from November 1, 2013, to December 31, 2013.

## Preprocessing/cleaning/labelling

* **Was any preprocessing/cleaning/labeling of the data done?**
    Yes, extensive preprocessing and feature engineering were performed:
    * **Initial Processing:** Timestamps were standardized to the 'Europe/Rome' timezone. `SMS-in/out` and `Call-in/out` records were merged into single `SMS activity` and `Call activity` features.
    * **Feature Engineering:**
        * **Temporal Features:** Cyclical features (`hour_sin`, `day_of_week_cos`), categorical time periods (`Morning`, `Evening`), and a boolean `is_weekend` flag were created.
        * **Spatial Features:** Grid coordinates (`grid_x`, `grid_y`) and a `grid_density` feature were engineered from the Grid ID.
        * **Target Variable Transformation:** The target variables (SMS, Call, Internet) were transformed using log, Box-Cox, or square root methods to normalize their distributions.

* **Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data?**
     Not the full data set. The datasets for the Telecommunication data and Precipitation data can be found on the Harward Dataverse 
     * Telecom Italia dataset : https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/QLCABU
     * Precipitation dataset https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/S2UGMD  
     * Public holidays dataset : https://github.com/sutee82/MilanMobileTrafficpred/blob/main/calendar.txt
* Smple processed data avaiable in the GitHub Repo 
## Uses

* **What other tasks could the dataset be used for?**
    Beyond mobile traffic prediction, the dataset could be used for:
    * Urban mobility and transportation planning.
    * Analyzing the impact of weather or public holidays on citizen behavior.
    * Identifying and predicting crowd formation during large events.
    * Retail and business site selection based on area activity levels.

* **Is there anything about the composition of the dataset or the way it was collected that might impact future uses?**
    Yes. The data is aggregated at the 235x235 meter grid level, making it unsuitable for any analysis requiring individual-level precision. The models trained on this dataset are highly specific to Milan's geography and the 2013 time period and may not generalize to other cities or times without retraining.

* **Are there tasks for which the dataset should not be used?**
    The dataset should not be used for:
    * Any form of individual surveillance or tracking.
    * Long-term historical analysis, as it only covers two months.
    * Direct application to other cities without careful validation and retraining.
    * Making assumptions about demographic groups, as no demographic data is included.

## Distribution

* **How has the dataset already been distributed?**
    The dataset was published in *Scientific Data*, a peer-reviewed, open-access journal from Nature Research. It is hosted on Harvard Dataverse.

* **Is it subject to any copyright or other intellectual property (IP) license?**
    The original paper states the data was released to research teams under the **Open Database License (ODbL)**. The paper itself is published under a Creative Commons license.

## Maintenance

* **Who maintains the dataset?**
    The provided text does not specify a current maintainer. The dataset is archived and available via Harvard Dataverse, but it is likely not being actively updated, as it corresponds to a specific historical period.
