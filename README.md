# Hybrid-model-for-assigning-constructive-characteristic---La-Iguan-micro-basin-exposure-model
## La Iguaná Micro-Basin Building Classification

This repository contains a hybrid methodology for assigning structural typologies to buildings within the La Iguaná micro-basin. The approach combines machine learning (K-Nearest Neighbors) and expert-based structural engineering rules to ensure reliable typology classification in contexts with incomplete or heterogeneous data.

---

## Method

### K-NN Algorithm Configuration

The model uses the **K-Nearest Neighbors algorithm** with the following configuration:

- **K = 5**: Number of nearest neighbors considered
- **Distance metric**: Euclidean distance
- **Weighting**: Distance-weighted voting (closer neighbors have more influence)

### Input Features

The classification uses four key features for each building:

1. **Built area** (m²)
2. **Socioeconomic stratum** (1-6 scale)
3. **Number of floors**
4. **Geographic coordinates** (latitude, longitude)

Geographic distance is computed using the **GeoPy** library for precise spatial proximity calculations.

### Classification Process

```
For each building:
  1. Identify the 5 nearest neighbors based on feature similarity
  2. Apply distance-weighted voting
  3. Check expert rules as constraints
  4. Assign final typology
```

---

## Expert Rules

Structural engineering thresholds act as safeguards to prevent physically impossible classifications:

```python
EXPERT_RULES = {
    'LIMITE_MAMPOSTERIA_NR': 4,      # Max floors for unreinforced masonry
    'LIMITE_MAMPOSTERIA_CONF': 5,    # Max floors for confined masonry
    'ALTURA_PAJARITO_MUROS': 5       # Height threshold for wall systems
}
```

These rules represent domain knowledge that prevents the algorithm from:
- Assigning unreinforced masonry to tall buildings
- Classifying structures with characteristics incompatible with their predicted typology

---
