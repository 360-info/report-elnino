# `/data`

## [Berkeley Earth](https://berkeleyearth.org/data/): global and national temperature time series

`berkeley-monthly-tavg-*.txt`: monthly temperature anomalies (and annual, 5- and 10-year smoothed monthly anomalies) for various regions. The global file here is part of BE's regular dataset, while the national ones come from BE's early-access high-resolution dataset.

## Indian crops and rainfall

`india-crops-by-district.csv`: raw crop data by crop and by areal, from [ICRISAT](http://data.icrisat.org).

`india-allcrops-peninsular.csv`, `india-ricemaize-peninsular.csv`: crop data aggregated down for Peninsular India (as defined by IMD), for both all crops combined and for rice and maize combined. Also joined with ENSO phase data, calculated using both Nino3.4 and SOI.

`india-rainfall-raw.csv`: monthly rainfall for Indian rainfall regions over June–September, supplied by the [Indian Meteorological Department].

## ENSO phases

`nasa-nino34-anomaly-monthly.txt`: monthly Nino3.4 (also known as ONI) from [NASA Physical Sciences Laboratory](https://psl.noaa.gov/gcos_wgsp/Timeseries/Nino34/)

`soi-monthly-raw.csv`: raw monthly SOI data from the [Bureau of Meteorology](http://www.bom.gov.au/climate/enso/soi)

`enso-indicators-jjas.csv`, `enso-indicators-monthly.csv`: derived ENSO classifications based on Nino3.4 and SOI. `monthly` is monthly classifications; `jjas` is an annual figure based on the average over June–September.