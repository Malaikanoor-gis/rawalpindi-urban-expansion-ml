# Urban Expansion in Rawalpindi District (2019-2025): ML Land-Cover Mapping

Google Earth Engine + scikit-learn. Sentinel-2 (January-April composites), no manual sampling or downloads.

## Methods
1. Classifier benchmark: Random Forest, Gradient Boosting and SVM were trained on Sentinel-2 bands and indices (NDVI, NDBI, MNDWI), with ESA WorldCover (2021) as automatic labels. Random and spatial-block (about 5 km) cross-validation were compared.
2. Change mapping: a Random Forest was trained separately for 2019 and 2025 using Dynamic World labels, then applied to each year's composite.
3. Area statistics and a transition matrix were computed from the two maps.

## Results
- Benchmark (agreement with WorldCover labels): SVM-RBF 0.78 accuracy (spatial CV), Random Forest 0.75, Gradient Boosting 0.75.
- Random and spatial CV gave nearly the same accuracy (gap 0.002-0.004), so spatial autocorrelation did not noticeably inflate the scores in this setup.
- Built-up area increased by about 22% between 2019 and 2025 (about 680 to 827 km2).

## Lessons / first attempt
My first approach produced an implausible decrease in built-up land (about -24%). On review, this was traced to using a classifier trained on 2021 for other years, and the method was changed to per-year training.

## Limitations
- Labels are automatic (WorldCover, Dynamic World) and contain errors; there is no field validation.
- Accuracy in the benchmark measures agreement with these labels, not true accuracy, and the final maps were not independently validated.
- Absolute areas depend on method choices. Changes in cropland and bare land are likely affected by seasonal and label noise.
- Only January-April imagery was used.

## Future work
Independent validation points from high-resolution imagery, seasonal composites, deep-learning segmentation, and urban growth projection.
