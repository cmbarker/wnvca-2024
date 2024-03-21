### Locations

This folder contains a comma-separated file `locations.csv` that contains location-specific data for all California counties included in the forecasting challenge. California Department of Finance (DOF) population estimates were retrieved from [dof.ca.gov](https://dof.ca.gov/forecasting/demographics/estimates-e1/).

Columns:

- `county` is the state name as a character string and is the variable that should be included in forecast submissions. For example, “Los Angeles” or “Tulare”. Forecast submissions will be checked to ensure that location names match those found in this csv file.
- `population` is the county population size from the DOF estimates as of January 1, 2023.
