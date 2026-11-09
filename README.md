# Multi-Sensor Satellite Yield Forecasting & PMFBY Parametric Risk Engine for Indian Paddy Clusters

An enterprise-grade remote sensing and machine learning system engineered for smallholder rice (*Oryza sativa*) monitoring across the Central/Eastern Indian Kharif belt (Chhattisgarh, Madhya Pradesh, Maharashtra, Odisha). The framework resolves persistent monsoon cloud contamination by fusing Synthetic Aperture Radar (Sentinel-1 C-Band SAR) with optical red-edge metrics (Sentinel-2), ERA5-Land agro-meteorology, and ISRIC SoilGrids to forecast parcel yields and automate parametric insurance claim settlement under the **Pradhan Mantri Fasal Bima Yojana (PMFBY)** framework.

---

## Executive Visual Deliverables

| Explainable AI: Agronomic SHAP Feature Attribution | QGIS Cartographic Risk Atlas: PMFBY Parametric Triggers | Power BI Executive Underwriting & Exposure Monitor |
| :---: | :---: | :---: |
| ![SHAP Feature Importance](paddy_yield_shap_importance.png) | ![PMFBY Spatial Risk Atlas](paddy_yield_insurance.png) | ![Power BI Underwriting Dashboard](powerbi_dashboard_preview.png) |
| *SHAP summary indicating primary yield drivers: SAR structural ratio, extreme anthesis heat days, and dry spells.* | *Spatial distribution of 300 test village clusters: Crimson Red markers denote PMFBY indemnity triggers; Steel Blue denotes normal yield.* | *Dynamic BI dashboard: village shortfall mapping, dry spell sensitivity scatter curves, and district-level indemnity exposure.* |

---

## Technical Architecture & Workflow

```text
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
[ Dual Geospatial & Business Intelligence Delivery ]
├── GeoJSON Spatial Atlas       ──> Thematic multi-layer GIS mapping & spatial liability layouts (QGIS LTR)
└── Power BI Underwriting Model ──> Dynamic district exposure, loss-ratio KPIs, and climate-stress scatter models
