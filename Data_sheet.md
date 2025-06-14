# Datasheet

## Motivation

* **For what purpose was the dataset created?** The dataset was created to provide a multi-source view of urban life and mobility patterns in Milan. This project uses it to predict mobile network demand to help operators allocate resources and prevent service disruptions.
* **Who created the dataset?** Barlacchi, G., De Nadai, M., Larcher, R., et al.
* **Who funded the creation of the dataset?** (Information not available in the provided text)

## Composition

* **What do the instances that comprise the dataset represent?** The instances represent aggregated mobile phone activity (calls, texts, internet), meteorological conditions, and public holidays for specific grid squares in Milan.
* **How many instances of each type are there?** The dataset contains Call Detail Records (CDRs) aggregated every 10 minutes for the central 2500 grid squares of Milan. It also includes meteorological data and a list of national holidays for the region.
* **Is there any missing data?** No
* **Does the dataset contain data that might be considered confidential?** The data consists of aggregated Call Detail Records. While anonymized and aggregated, generally location-based data can still be sensitive. Due to the age and the publicly avaiable nature of the data it is considered non Confidential . 

## Collection process

* **How was the data acquired?** The data is a multi-source collection, with the primary mobile usage data coming from Call Detail Records (CDRs).
* **If the data is a sample of a larger subset, what was the sampling strategy?** The dataset was filtered to focus on the central 2500 grid squares of Milan to capture the most active urban core.
* **Over what time frame was the data collected?** November 1, 2013, to December 31, 2013.

## Preprocessing/cleaning/labelling

* **Was any preprocessing/cleaning/labeling of the data done?** Yes.
    * Timestamps were converted to the `Europe/Rome` timezone.
    * SMS and Call data for "in" and "out" were merged into single activity features.
    * **Feature Engineering**:
        * **Temporal Features**: Cyclical features for time (`hour_sin`, `day_of_week_cos`), categorical time periods (`Morning`, `Evening`), and an `is_weekend` flag were created.
        * **Spatial Features**: Grid coordinates (`grid_x`, `grid_y`) and a `grid_density` feature were engineered.
        * **Target Variable Transformation**: The target variables (SMS, Call, Internet) were transformed using log, Box-Cox, or square root methods to normalize their distributions.
* **Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data?** Yes 

## Uses

* **What other tasks could the dataset be used for?** The dataset is valuable for urban planners studying city mobility patterns.
* **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** The data is aggregated and filtered to the Milan city center. Therefore, models trained on it will be specific to this geographic area and may not generalize well to suburban or rural areas.
* **Are there tasks for which the dataset should not be used?** Yes, it is specifically designed for short-term forecasting within Milan. It should not be used for long-term planning or for predicting traffic in other cities.

## Distribution

* **How has the dataset already been distributed?** It was published as part of a paper in the journal *Scientific Data*.
* **Is it subject to any copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?** 

## Maintenance

* **Who maintains the dataset?** (Information not available in the provided text)
