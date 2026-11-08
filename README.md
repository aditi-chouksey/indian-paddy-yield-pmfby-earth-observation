# Multi-Sensor Satellite Yield Forecasting & PMFBY Parametric Risk Engine for Indian Paddy Clusters

An enterprise-grade remote sensing and machine learning system engineered for smallholder rice (*Oryza sativa*) monitoring across the Central/Eastern Indian Kharif belt (Chhattisgarh, Madhya Pradesh, Maharashtra, Odisha). The framework resolves persistent monsoon cloud contamination by fusing Synthetic Aperture Radar (Sentinel-1 C-Band SAR) with optical red-edge metrics (Sentinel-2), ERA5-Land agro-meteorology, and ISRIC SoilGrids to forecast parcel yields and automate parametric insurance claim settlement under the **Pradhan Mantri Fasal Bima Yojana (PMFBY)** framework.

---

## Executive Visual Deliverables

| Explainable AI: Agronomic SHAP Feature Attribution | QGIS Cartographic Risk Atlas: PMFBY Parametric Triggers |
| :---: | :---: |
| ![SHAP Feature Importance](paddy_yield_shap_importance.png) | ![PMFBY Spatial Risk Atlas](india_paddy_pmfby_risk_map.png) |
| *SHAP summary indicating primary yield drivers: SAR structural ratio, extreme anthesis heat days, and dry spells.* | *Spatial distribution of 300 test village clusters: Crimson Red markers denote verified PMFBY shortfall indemnity triggers; Steel Blue markers denote normal yield.* |

---

## Technical Architecture & Workflow
[ Multi-Source Earth Observation Stack ]
├── Sentinel-1 SAR (C-Band Radar) ──> Cloud-penetrating VV, VH backscatter & VH/VV structural cross-ratio
├── Sentinel-2 Multi-Spectral   ──> Cloud-free composite NDRE (chlorophyll) & NDWI (canopy moisture)
├── ERA5-Land Agro-Climatology  ──> Monsoon precipitation, consecutive dry spells, anthesis heat days (>35°C), VPD
└── ISRIC SoilGrids (250m)      ──> Topsoil clay fraction (%) and Soil Organic Carbon (SOC)
│
▼
[ Quantile Gradient Boosting Engine (LightGBM) ]
├── 50th Percentile (Median)    ──> Expected operational yield (t/ha)
├── 10th Percentile (Downside)  ──> Conservative downside floor for agricultural credit underwriting
└── 90th Percentile (Upside)    ──> Favorable seasonal yield boundary
│
▼
[ PMFBY Parametric Loss Settlement Engine ]
└── Threshold Yield (TY) Delta  ──> Automated Shortfall % calculation and ₹45,000/ha scaled indemnity payout
│
▼
[ Geospatial Vector & Risk Delivery ]
└── GeoJSON Spatial Atlas       ──> Thematic multi-layer GIS mapping & portfolio liability visualization (QGIS LTR)## Quantitative Validation & Portfolio Stress-Testing

Evaluated across an out-of-sample holdout of **300 independent village clusters**:

### 1. Regression Accuracy Metrics
* **Coefficient of Determination ($R^2$):** `0.660`
* **Root Mean Squared Error (RMSE):** `0.285 tonnes/ha`
* **Mean Absolute Error (MAE):** `0.228 tonnes/ha`

### 2. PMFBY Parametric Actuarial Results
* **Insurance Claim Threshold Trigger:** Yield shortfall $>10.0\%$ below historical 7-year Threshold Yield (TY).
* **Portfolio Loss Rate:** `7.0%` of clusters triggered parametric payouts (21 of 300 test villages).
* **Mean Indemnity Settlement:** `₹7,178.50 per hectare` across impacted administrative units.

---

## Repository Structure

```text
├── 01_India_Paddy_Yield_PMFBY_Engine.ipynb   # Complete data ingestion, quantile ML, and actuarial engine notebook
├── india_paddy_insurance_atlas.geojson       # WGS84 GeoDataFrame containing coordinates, yield estimates, & payouts
├── paddy_yield_shap_importance.png           # High-resolution (300 DPI) SHAP TreeExplainer feature attribution plot
├── india_paddy_pmfby_risk_map.png            # QGIS cartographic layout showing spatial claim distribution
└── README.md                                 # Comprehensive project documentation
Core Technologies
Earth Observation & Geospatial: geopandas, shapely, rasterio, QGIS Desktop (LTR 3.44)

Machine Learning & Uncertainty: lightgbm, scikit-learn, shap (TreeExplainer)

Data Stack & Visualization: python 3.10+, pandas, numpy, matplotlib, seaborn
