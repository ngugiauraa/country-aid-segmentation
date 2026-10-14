# Where Should Aid Go First? Segmenting 167 Countries by Need

Unsupervised machine learning on 9 socio-economic and health indicators to group countries by development level, then turn the high-need group into a **ranked priority list** an aid organisation could act on.

## Approach

1. **Fix the skew first.** Income, GDP per capita, child mortality and inflation are heavily right-skewed. I log-transform them (sign-preserving for inflation) before standardising, so a few very rich countries don't dominate the distances.
2. **Pick the number of groups with three independent checks:** silhouette score, Gaussian-mixture BIC, and bootstrap stability, which asks whether the same groups come back when the data is resampled.
3. **Cluster with K-Means (k = 3)** and cross-check against a Gaussian mixture model (agreement ARI = 0.75).
4. **Rank within the high-need group** using a transparent need index: the mean percentile rank across child mortality, life expectancy, income, GDP per capita and health spending.

## Results

| Group | Countries | Median child mortality (per 1,000) | Median life expectancy | Median income |
|---|---|---|---|---|
| High need | 49 | 88 | 61 | 1,870 |
| Developing | 68 | 19 | 73 | 10,180 |
| Developed | 50 | 5 | 80 | 29,150 |

**Top 5 priority countries by need index:** Central African Republic, Niger, Mozambique, Guinea, Chad.

PCA shows one dominant "development" axis (55% of variance) that the three groups line up along, and a second "trade openness" axis (17%) that varies within groups.

## Project layout

```
data/country_data.csv                        167 countries × 9 indicators
notebook/country_aid_segmentation.ipynb      full analysis
```

## Run it

```bash
pip install -r requirements.txt
jupyter notebook notebook/country_aid_segmentation.ipynb
```

## Limitations

The indicators are a single snapshot. They don't capture conflict, natural disasters or existing aid flows, all of which a real allocation decision would weigh.

## Data

The public "Country Data" dataset for unsupervised learning (HELP International scenario), 167 countries.

## Author

Jesse Ngugi · [github.com/ngugiauraa](https://github.com/ngugiauraa)
