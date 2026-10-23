# Weather Data Exploratory Analysis: Seattle, 2012–2015

Exploratory data analysis (EDA) of four years of daily Seattle weather using **Python, Pandas, NumPy and Matplotlib**. The project cleans and checks the data, summarises it statistically, and uses 17 figures to show seasonal cycles, rainfall patterns, wind behaviour and how the variables relate to each other.

## Key Findings

1. **Summers are warm and dry, winters cool and wet.** Average daily high is **24.9 °C in summer vs 8.7 °C in winter**. August is the warmest month (average high 26.1 °C) and December/January the coolest (about 8.2 °C).
2. **Rain is a winter story.** **73.7%** of all precipitation fell between October and March, and only **7.8%** in June–August. July is the driest month and November the wettest.
3. **Rain is rare but heavy.** 57.4% of days had no precipitation at all (median 0, mean 3.03), yet the maximum was 55.9 on 2015-03-15. By the IQR rule, 206 days (14.1%) are precipitation outliers.
4. **Rain and sun split the year almost evenly.** Rain 43.9% of days, sun 43.8%, fog 6.9%, drizzle 3.6%, snow 1.8% (26 days, from November to April).
5. **Weather type tracks temperature.** Average daily high: snow 5.6 °C, rain 13.5 °C, fog 16.8 °C, sun 19.9 °C.
6. **Highs and lows move together.** `temp_max` and `temp_min` have the strongest correlation in the data (r = 0.876).
7. **Windy days tend to be wetter.** Wind and precipitation correlate at r = 0.33. On the 51 days with precipitation ≥ 20, mean wind was 4.7 against 3.24 overall. February is the windiest month (3.79) and August the calmest (2.75).
8. **Extremes.** Hottest day 35.6 °C (2014-08-11); coldest night -7.1 °C (2013-12-07). Days with a high of 30 °C or more: 63, almost all in July and August. Days with a minimum below 0 °C: 72.
9. **Year to year.** Average high rose from 15.3 °C (2012) to 17.4 °C (2015), and 2013 was the driest year (828 vs 1,139–1,233 in the other years). Four years is far too short to call this a climate trend.

## Dataset

| Item | Value |
|---|---|
| Source | [vega-datasets `seattle-weather.csv`](https://raw.githubusercontent.com/vega/vega-datasets/main/data/seattle-weather.csv) |
| Location | Seattle (the file has no location column) |
| Period | 2012-01-01 to 2015-12-31 (1,461 daily rows, no gaps or duplicate dates) |
| Missing values | 0 of 8,766 cells |

| Column | Description |
|---|---|
| `date` | Observation date |
| `precipitation` | Daily precipitation (unit is not stated in the file) |
| `temp_max` | Daily maximum temperature (°C) |
| `temp_min` | Daily minimum temperature (°C) |
| `wind` | Daily wind speed (unit is not stated in the file) |
| `weather` | Category: `rain`, `sun`, `fog`, `drizzle`, `snow` |

### Data quality notes

- Every `temp_min` is below its `temp_max`; no impossible values were found.
- **Label vs measurement mismatch:** all `sun`, `fog` and `drizzle` days have precipitation of exactly 0, and 44 of the 641 `rain` days also have 0. The `weather` label therefore cannot be treated as a precise rain gauge.

### Descriptive statistics

| Variable | Mean | Median | Std | Min | Max | Skew |
|---|---|---|---|---|---|---|
| `temp_max` | 16.44 | 15.6 | 7.35 | -1.6 | 35.6 | 0.28 |
| `temp_min` | 8.23 | 8.3 | 5.02 | -7.1 | 18.3 | -0.25 |
| `precipitation` | 3.03 | 0.0 | 6.68 | 0.0 | 55.9 | 3.51 |
| `wind` | 3.24 | 3.0 | 1.44 | 0.4 | 9.5 | 0.89 |

## Visualizations

### Relationships between variables

**Correlation heatmap.** Highs and lows are strongly linked (0.88). Precipitation has a mild negative link with `temp_max` (-0.23) and a mild positive one with wind (0.33). Wind and temperature are only weakly related.

![Correlation Heatmap](figures/correlation_heatmap_annotated.png)

**Correlation matrix.** The same coefficients in table form (`tables/numeric_correlation_matrix.csv`).

![Correlation Matrix](figures/correlation_matrix.png)

**Minimum vs. maximum temperature (hexbin).** Days cluster where highs are 10–22 °C and lows 4–12 °C (the middle half of the data), along a clear upward diagonal.

![Minimum vs. Maximum Temperature](figures/minimum_vs_maximum_temperature_hexbin.png)

**Numeric scatter matrix.** Precipitation points pile up at zero with a long tail of heavy-rain days, while the two temperature variables form a tight diagonal band.

![Numeric Scatter Matrix](figures/numeric_scatter_matrix.png)

**3D feature space** (min temp, max temp, wind; colour = precipitation). The heaviest-rain days sit at moderate temperatures and above-average wind, and warm calm days (high above 20 °C, wind below 3) are mostly dry: only 13% of them had any precipitation, against 42.6% of all days.

![Three-Dimensional Weather Feature Space](figures/weather_feature_space_3d.png)

### Distributions

**Precipitation.** Extremely right-skewed (skew 3.5): most days are dry and a few very wet days stretch the tail up to 55.9.

![Distribution of Precipitation](figures/distribution_precipitation.png)

**Maximum temperature.** Roughly symmetric (mean 16.4, median 15.6 °C) with a range of -1.6 to 35.6 °C and no IQR outliers.

![Distribution of Maximum Temperature](figures/distribution_temp_max.png)

**Minimum temperature.** Centred near 8.3 °C with a slight tail towards cold nights, down to -7.1 °C.

![Distribution of Minimum Temperature](figures/distribution_temp_min.png)

**Wind.** Mostly 2–4, with a right tail up to 9.5. 34 days (2.3%) exceed the IQR upper fence of 6.7, and almost all of them fall between September and April.

![Distribution of Wind](figures/distribution_wind.png)

### Weather categories

**Category frequency.** Rain (641 days) and sun (640 days) dominate; snow is rare (26 days).

![Weather Category Frequency](figures/weather_category_frequency.png)

**Maximum temperature by category.** Snow days are clearly colder (median 5.6 °C) than rain (12.8 °C) and sun (21.1 °C). Sun has the widest spread among the common categories because it occurs in every season.

![Maximum Temperature by Weather Category](figures/maximum_temperature_by_weather_boxplot.png)

### Seasonal patterns

**Seasonal maximum temperature.** A smooth single peak: about 8 °C in December–January rising to 26 °C in July–August.

![Seasonal Maximum Temperature](figures/seasonal_temp_max.png)

**Seasonal minimum temperature.** The same shape, from 2.7 °C in January to 14.8 °C in August.

![Seasonal Minimum Temperature](figures/seasonal_temp_min.png)

### Time series

**Precipitation.** Spikes cluster in autumn and winter every year, with long flat stretches in summer. The largest spike is 55.9 on 2015-03-15.

![Precipitation Time Series](figures/timeseries_precipitation.png)

**Maximum temperature.** A repeating annual wave with a summer peak each year; the highest point is 35.6 °C on 2014-08-11.

![Maximum Temperature Time Series](figures/timeseries_temp_max.png)

**Minimum temperature.** Follows the same annual wave. The lowest night was -7.1 °C on 2013-12-07.

![Minimum Temperature Time Series](figures/timeseries_temp_min.png)

**Wind.** Noisier than temperature, with a weaker seasonal pattern: stronger gusts appear mostly in winter and early spring, and summers are calmer.

![Wind Time Series](figures/timeseries_wind.png)

## Project Structure

```text
├── data/                     # seattle_weather.csv
├── figures/                  # 17 PNG charts
├── tables/                   # statistics, quality and outlier reports (CSV)
├── dashboard/                # executive_summary.txt
├── weather_analysis_advanced.ipynb
├── requirements.txt
├── LICENSE
└── README.md
```

## How to Run

**Google Colab:** upload `weather_analysis_advanced.ipynb` and `data/seattle_weather.csv`, then run all cells.

**Locally:**

```bash
git clone <this-repository-url>
cd <repository-folder>
python -m venv .venv
source .venv/bin/activate          # Windows PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook weather_analysis_advanced.ipynb
```

## Limitations

- One location and only four years of data, so seasonal patterns are reliable but long-term trends are not.
- Correlation does not imply causation.
- The file does not state the units of `precipitation` and `wind`, so those values are reported as given.
- The `weather` label does not always agree with the precipitation measurement (see data quality notes).

## Possible Next Steps

- [ ] Compare monthly averages year by year with confidence intervals.
- [ ] Build a simple model that predicts the weather category and report its accuracy.
- [ ] Add a few more years of data to look for real trends.

## License

Released under the [MIT License](LICENSE). The data comes from the vega-datasets project; check its repository for its terms.

## Author

**Harpreet Singh** · [GitHub: harpreetsingh171190-cmyk](https://github.com/harpreetsingh171190-cmyk)
