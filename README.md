# Vegetation Cover in Padova

Quantification of urban vegetation cover in three districts of Padova (city center, university area, industrial area) from aerial imagery, using pixel classification in [Ilastik](https://www.ilastik.org/) and automated pixel counting in ImageJ. Project for the **Image Based Learning** course (MSc in Quantitative and Computational Bioscience, University of Padova).

📄 Full report: [`De Rossi Lisa - report.pdf`](report.pdf)

## Results

Mean vegetation cover from five samples per district:

| District | Mean vegetation (%) | Std. deviation |
|---|---|---|
| University area | 28.14 | 8.07 |
| City center | 21.02 | 13.28 |
| Industrial area | 8.13 | 5.30 |

The university area (Portello and Piovego) is the greenest, the industrial area has the lowest cover and the most uniform pattern, and the city center is the most heterogeneous.

## Data

- **Source:** Google Earth Pro, 2D view with the "3D Buildings" layer off and North at the top
- **Acquisition:** June 2025 (peak vegetation), constant eye altitude of 1150 ft, 300 ft scale bar in every image
- **Sampling:** 5 images per district, placed on a spatial grid to avoid observer bias, with placemarks to prevent overlap
- **Naming:** `pd_{district}_{image_number}`

## Method

1. **Pixel classification (Ilastik):** Random Forest classifier with color/intensity, edge and texture features at sigma 1.6–5.0. Two classes: *vegetation* (canopies, grass, shrubs, and also canals and rivers) and *anthropic* (roofs, roads, concrete, vehicles). Trained on one representative image, then refined on the others where shadows or dark roofs were misclassified. Exported as "simple segmentation" PNG maps.
2. **Quantification (ImageJ):** a macro counts the pixels of each class for every image and exports a CSV.
3. **Statistics and plots (Python):** pandas and Matplotlib.

## Limitations

- Low resolution makes some surfaces ambiguous even for a human observer
- Arid patches were labeled as anthropic, so only active green cover is counted
- Shadows were the main source of misclassification
- Moss-covered roofs look like low vegetation and slightly inflate the estimate
- Rivers and canals were included in the vegetation class
- Only five samples per district

A possible improvement is Ilastik's Autocontext workflow, which adds spatial context to the pixel classifier.

## Tools

Ilastik, ImageJ/Fiji, Python (pandas, Matplotlib), Google Earth Pro
