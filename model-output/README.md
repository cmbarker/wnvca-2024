# Model outputs folder


This folder contains a set of subdirectories, one for each model, that contains submitted model output files for that model. The structure of these directories and their contents follows [the model output guidelines in the hubverse's documentation](https://hubdocs.readthedocs.io/en/latest/user-guide/model-output.html). 

# Data submission instructions

All forecasts should be submitted directly to the [model-output](../model-output) folder. Data in this directory should be added to the repository through a pull request so that automatic [validation checks](../.github/workflows/model-output-pull.yml) are run (although teams are highly encouraged to do [local validations](#Local-Validation) before submitting).

These instructions provide detail about the [data format](#Data-formatting) as well as [validation](#Forecast-validation) that you can do prior to this pull request. In addition, we describe [metadata](https://github.com/Infectious-Disease-Modeling-Hubs/hubTemplate/blob/master/model-metadata/README.md) that each model should provide in the model-metadata folder.

*Table of Contents*

-   [What is a forecast](#What-is-a-forecast)
-   [Target data](#Target-data)
-   [Data formatting](#Data-formatting)
-   [Forecast file format](#Forecast-file-format)
-   [Forecast data validation](#Forecast-validation)
-   [Monthly ensemble build](#Weekly-ensemble-build)
-   [Policy on late submissions](#policy-on-late-or-updated-submissions)

## What is a forecast 

Models are asked to make specific quantitative forecasts about data that will be observed in the future. These forecasts are interpreted as "unconditional" predictions about the future. That is, they are not predictions only for a limited set of possible future scenarios in which a certain set of conditions (e.g. vaccination uptake is strong, or new social-distancing mandates are put in place) hold about the future -- rather, they should characterize uncertainty across all reasonable future scenarios. In practice, all forecasting models make some assumptions about how current trends in data may change and impact the forecasted outcome; some teams select a "most likely" scenario or combine predictions across multiple scenarios that may occur. Forecasts submitted to this repository will be evaluated against observed data.


## Target Data 

County-level forecasts for total WNV diseases cases in each remaining calendar month of 2024 through December should be produced and submitted by their respective monthly due dates, beginning on April 30, 2024. Please note that these monthly county-level forecasts differ from previous national WNV forecasting challenge targets. This page includes information on how to submit forecasts. These instructions have been adapted from the prior challenges and the most up-to-date [hubverse structure](https://hubdocs.readthedocs.io/en/latest/). 

All forecasts should be submitted directly to the model-output folder in this repository (more information on the submission folders is available here). Forecast data should be added to the repository through a pull request so that automatic [data validation checks](../.github/workflows/model-output-pull.yml) are run. 

These instructions provide detail about the data format as well as validation that you can do prior to this pull request. In addition, we describe the [metadata](#Metadata) that each model should provide. 


## Data formatting 

The automatic checks in place for forecast files submitted to this repository validates both the filename and file contents to ensure the file can be used in the visualization and ensemble forecasting.

### Subdirectory

Each model that submits forecasts for this project will have a unique subdirectory within the [model-output/](model-output/) directory in this GitHub repository where forecasts will be submitted. Each subdirectory must be named

    team-model

where

-   `team` is the team name and
-   `model` is the name of your model.

Both team and model should be less than 15 characters and not include
hyphens or other special characters, with the exception of "\_".

The combination of `team` and `model` should be unique from any other model in the project.

Within each team subdirectory a set of forecasts should be submitted in CSV format. The name of these files should follow this convention:  

  * *round1-id*.csv 
  * *round2-id*.csv 
  * ... 

where the round id corresponds to the target date of the forecast and the id to the *team-model* identifier. More information on these folders structures' is found in [this document](https://hubdocs.readthedocs.io/en/stable/format/model-output.html). And examples for one of our baseline models can be found in [this folder](./model-output/CDPH-AZO/).


### Metadata

A metadata file should be provided by each team. This file should be placed in the model-metadata folder of the repository, and should have the following naming convention: `team-model.yml`; and its contents should adhere to [hubverse’s standards](https://hubdocs.readthedocs.io/en/stable/format/model-metadata.html). Where the fields required in our challenge are: `schema_version`, `team_name`, `team_abbr`, `model_name`, `model_abbr`, `model_contributors`, `license`, and `model_details`. An example metadata file can be found [here](./model-metadata/CDPH-AZO.yml).


### License (optional) 

By default, forecasts are released under a [CC-BY 4.0 license](https://creativecommons.org/licenses/by/4.0/legalcode.en). If you would like to release your forecasts under a different license, please specify a standard license in the license field of your metadata file. Alternatively, if you wish to use a license that is not in the list of standard licenses, you may include a `LICENSE.txt` file in the metadata folder, and refer to it in the license field of your model’s yaml file. 

### Forecasts

Each forecast file should have the following format:

    YYYY-MM-DD-team-model.csv

where

-   `YYYY` is the 4 digit year,
-   `MM` is the 2 digit month,
-   `DD` is the 2 digit day,
-   `team` is the team name, and
-   `model` is the name of your model.

The date YYYY-MM-DD is the [`reference_date`](#reference_date). This should be the Saturday following the submission date.

The `team` and `model` in this file must match the `team` and `model` in
the directory this file is in. Both `team` and `model` should be less
than 15 characters, alpha-numeric and underscores only, with no spaces
or hyphens. 

## Forecast file format 

The file must be a comma-separated value (csv) file with the following
columns (in any order):


-   [`location`](#location)
-   [`origin_date`](#origin_date)
-   [`target_date`](#target_date)
-   [`output_type_id`](#output_type_id)
-   [`value`](#value)
-   [`type`](#type)
-   [`unit`](#unit)

No additional columns are allowed.


### `location`

Values in the `location` column must be one of the California counties in the following list:

```
Fresno, Kern, Los Angeles, Merced, Orange, Placer, Riverside, Sacramento, 
San Bernardino, San Joaquin, Solano, Stanislaus, Tulare
```

### `origin_date` 

Values in the `reference_date` column must be a date in the ISO format

    YYYY-MM-DD

This is the date from which all forecasts should be considered. This date must be equal or lower to the submission date for each of the challenge's deadlines. 

### `target_date`

Values in the `target_date` column must be a date in the format

    YYYY-MM-DD
    
This is the last date of the forecast target for each month. This date should match the submission target date.


### `output_type_id`

Upper, inclusive, bound on the standardized bin interval as defined in:

* `0`: [0]
* `1`: (0, 1]
* `2`: (1, 2]
* `3`: (2, 3]
* `4`: (3, 4]
* `5`: (4, 5]
* `6`: (5, 6]
* `8`: (6, 8]
* `10`: (8, 10]
* `15`: (10, 15]
* `200`: (15, 200]


### `type`

As we will only be predicting the binned probabilities of cases as defined in [`output_type_id`](#output_type_id), we are requesting these are submitted as CDF to adhere to [hubverse's latest standards](https://hubdocs.readthedocs.io/en/latest/user-guide/model-output.html#formats-of-model-output). As such, this column should be a constant `cdf`.


### `value`

Bins probabilities are requested in CDF form for each of the intervals as defined in [`output_type_id`](#output_type_id), where the last value in the prediction should be 1 for `hubverse`'s validation to succeed in our github CI pull request.

### `unit`

String constant with value `WNV cases`, as it is the standard unit for this challenge.


### Example tables

Example of a CSV submission file):



```csv
location, origin_date,  target_date,  output_type_id, value,    output_type,  target
Merced,   2024-05-31,   2024-05-31,   0,              0.09091,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   1,              0.18182,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   2,              0.27273,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   3,              0.36364,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   4,              0.45455,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   5,              0.54545,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   6,              0.63636,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   8,              0.72727,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   10,             0.81818,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   15,             0.90909,  cdf,          WNV cases
Merced,   2024-05-31,   2024-05-31,   200,            1.0,      cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   0,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   1,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   2,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   3,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   4,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   5,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   6,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   8,              1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   10,             1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   15,             1,        cdf,          WNV cases
Placer,   2024-05-31,   2024-05-31,   200,            1,        cdf,          WNV cases
...
```

## Forecast validation 

To ensure proper data formatting, pull requests for new data in `model-output/` will be automatically run. Optionally, you may also run these validations locally.

### Pull request forecast validation

When a pull request is submitted, the data are validated through [Github Actions](https://docs.github.com/en/actions) which runs the tests present in [the hubValidations
package](https://github.com/Infectious-Disease-Modeling-Hubs/hubValidations). The intent for these tests are to validate the requirements above. Please [let us know](https://github.com/Chipdelmal/WNVCA-2024) if you are facing issues while running the tests.

### Local forecast validation

Optionally, you may validate a forecast file locally before submitting it to the hub in a pull request. 


## Monthly ensemble build 

Every month, we will generate a  *WNV California Forecasting Challenge* ensemble using valid forecast submissions in the current week by the deadline. Some or all participant forecasts may be combined into an ensemble forecast to be published in real-time along with the participant forecasts. In addition, some or all forecasts may be displayed alongside the output of a baseline model for comparison.


## Policy on late or updated submissions 

To ensure that forecasting is done in real-time, all forecasts are required to be submitted to this repository by the listed deadlines. Late forecasts may be accepted on a case-by-case basis. 

## Evaluation criteria

When reported data for 2024 are available, an analysis will be conducted using multiple scoring metrics, including the logarithmic score and the multibin logarithmic score, to assess and compare forecasts across all counties at each time point. A joint manuscript will be prepared to disseminate findings on this comparison and the general performance of submitted forecasts. Participants may publish their own forecasts and results at any time. 

## Local Validation

Teams are highly encouraged to validate their data locally before doing their pull request. To do this, install the `hubValidations` package:

```R
remotes::install_github("Infectious-Disease-Modeling-Hubs/hubValidations")
```

then set your working directory to the base repository path, and run:

```R
require(hubValidations)
hubValidations::validate_submission(
  file_path='CDPH-AZO/2024-05-31-CDPH-AZO.csv',
  hub_path='.'
)
```

where the `file_path` should be replaced with your submission file.
