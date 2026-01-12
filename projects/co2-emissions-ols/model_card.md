## Model Card

*Following Google's Model Cards framework for transparent ML documentation*

### Model Details
- **Model Type**: Regression (Ordinary Least Squares)
- **Version**: 1.0
- **Date**: December 2024
- **Developers**: Lillian Elek
- **License**: MIT (Educational/Non-commercial)
- **Framework**: statsmodels + scikit-learn

### Intended Use
- **Primary Use**: State-level CO₂ emissions prediction analysis
- **Primary Users**: Environmental scientists, policy analysts, energy planners, data scientists
- **Out-of-Scope Uses**: 
  - ❌ Precise facility-level emissions (model is state-aggregated)
  - ❌ Real-time emissions monitoring (data from 2009)
  - ❌ Causal inference (correlational analysis only)
  - ❌ Regulatory compliance (not certified for official reporting)

### Training Data
- **Sources**: [Net Electricity Generation](https://www.eia.gov/electricity/data/browser/) | [Energy-Related Carbon Dioxide Emissions by State, 2005-2016](https://www.eia.gov/environment/emissions/state/analysis/) | [Population](https://www.census.gov/)
- **Size**: 50 U.S. states (40 train, 10 test after 80/20 split)
- **Time Period**: 2009 (single year snapshot)
- **Geographic Coverage**: All 50 U.S. states
- **Features**: 11 energy generation sources + population
- **Target**: CO₂ emissions (million metric tons)

### Evaluation Data
- **Split Method**: Random split (80/20)
- **Test Set Size**: 10 states
- **Same Source**: Training and test from same 2009 dataset

### Metrics
| Metric | Training | Testing | Interpretation |
|--------|----------|---------|----------------|
| **R²** | 0.899 | 0.705 | Explains 70.5% of emissions variance on unseen data |
| **RMSE** | 0.331 | 0.466 | ~30-50% prediction error on original scale |
| **MAE** | 0.243 | 0.413 | Average error of 0.4 log-units |
| **Selected Features** | 3 | - | population, Coal, Wind |

### Ethical Considerations
- **Bias**: 
  - Dataset represents 2009 energy landscape (may not reflect current mix)
  - No demographic or economic justice variables included
  - May not capture environmental justice impacts on communities
- **Fairness**: 
  - Treats all states equally (no weighting by population or GDP)
  - Does not account for historical emissions or per-capita fairness
- **Transparency**: 
  - Fully interpretable linear model
  - All coefficients and diagnostics documented
- **Accountability**:
  - Not suitable for punitive policy decisions
  - Should inform, not dictate, energy policy

### Limitations
1. **Data Limitations**:
   - Single year (2009) - no temporal dynamics
   - State-level only (no sub-state resolution)
   - Missing variables: transportation, industrial processes, economic factors
   - Pre-shale revolution (natural gas boom post-2010)

2. **Model Limitations**:
   - Linear assumptions may miss threshold effects
   - Cannot predict emissions outside observed ranges
   - No uncertainty quantification (confidence intervals)
   - Test set errors larger than training (expected but notable)

3. **Deployment Considerations**:
   - Requires domain expertise for interpretation
   - Should not be sole basis for policy decisions
   - Needs updating with current data for relevance
   - Log-scale predictions may confuse non-technical stakeholders

### Recommendations
- **Use for**: Exploratory analysis, baseline predictions, educational purposes
- **Combine with**: Expert judgment, updated data, economic models
- **Monitor**: Model drift if applied to post-2009 data
- **Retrain**: Annually or when energy mix substantially changes
- **Validate**: Against independent emissions datasets (EPA, EIA)

### References
- [Net Electricity Generation](https://www.eia.gov/electricity/data/browser/) 
- [Energy-Related Carbon Dioxide Emissions by State, 2005-2016](https://www.eia.gov/environment/emissions/state/analysis/) 
- [Population](https://www.census.gov/)