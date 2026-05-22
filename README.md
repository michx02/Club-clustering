# Nightclub Customer Clustering

This project explores customer segments for a nightclub using survey data. The notebook cleans the data, combines related survey questions into broader scores, and compares clustering approaches for mixed numeric and categorical features.

The goal is not just to produce clusters, but to turn them into useful business insight: which customers feel pricing is fair, who is likely to come back, who would recommend the club, and where the nightclub may be losing trust.

## Project File

- `Night_club_clustering.ipynb` - main analysis notebook

## Dataset

The notebook expects a file named `Nightclub.csv` in the project directory.

The dataset is linked inside the notebook and contains customer survey responses, including:

- Customer type and nightclub visit frequency
- Pricing strategy experienced by the customer
- Fairness, ethics, and acceptability ratings
- Word-of-mouth intention
- Revisit intention
- Familiarity with the pricing strategy
- Demographic information such as age, gender, income, employment, education, and ethnicity

The CSV is not currently included in this repository, so download it from the notebook link before running the analysis locally.

## What The Notebook Does

The analysis follows a simple customer segmentation workflow:

1. Loads and inspects the nightclub survey data.
2. Removes the single missing age entry.
3. Combines related survey items into aggregate scores:
   - `fair_score`
   - `wom_score`
   - `ri_score`
   - `fam_score`
4. Groups age into categories.
5. Simplifies sparse visit-frequency values.
6. Drops highly skewed or less useful demographic columns.
7. Scales numeric features.
8. Runs K-Prototypes clustering for mixed categorical and numeric data.
9. Runs agglomerative clustering using Gower distance.
10. Interprets the resulting customer segments.

## Methods Used

### K-Prototypes Clustering

K-Prototypes is used because the dataset contains both categorical features, such as gender and pricing strategy, and numeric features, such as fairness and revisit scores.

The notebook tests several values of `k` using the cost curve, then fits a final model. If you want to experiment with the number of clusters, update the `optimal_k` value in the clustering section.

### Agglomerative Clustering

Hierarchical clustering is also tested using Gower distance, which works well for mixed data types. The dendrogram helps inspect cluster structure before assigning final cluster labels.

## Main Findings

The strongest signals across the clusters are pricing fairness, revisit intention, and word-of-mouth intention.

Some frequent student customers appear loyal even when they rate pricing fairness poorly. Other higher-income customers may understand or accept the pricing structure but still show weak emotional attachment to the nightclub. This suggests that fairness perception and actual loyalty do not always move together.

The analysis points to a few practical actions:

- Make pricing rules clearer, especially for frequent visitors.
- Consider student discounts, loyalty tiers, or targeted offers.
- Use weekday or first-time visitor promotions to convert curious customers into regulars.
- Collect more feedback from dissatisfied regulars before they stop coming back.
- Encourage referrals from segments with positive word-of-mouth scores.

## How To Run

Install the main Python dependencies:

```bash
pip install numpy pandas seaborn matplotlib scikit-learn kmodes gower scipy
```

Then open the notebook:

```bash
jupyter notebook Night_club_clustering.ipynb
```

You can also run it in Google Colab using the badge at the top of the notebook.

Make sure `Nightclub.csv` is in the same folder as the notebook before running the cells.

## Notes

The notebook is exploratory, so the cluster count and final interpretation can be refined. The current version is useful for understanding broad customer patterns, but a production-ready segmentation model would need more validation, cleaner experiment tracking, and a larger discussion of sampling bias in the survey data.
