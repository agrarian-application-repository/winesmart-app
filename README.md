## WINESMART   - AGRARIAN Project

## 1. Dataset
- Vineyard imagery (leaves, grapes, foliage)  
- Meteorological and weather forecast data  
- Historical climate and soil datasets (2015–2024)

## 2. Node Type
Edge or Cloud

## 3. Application Name
**WINESMART – Intelligent Pesticide Spraying Solution for Vineyards**

This repository contains multiple complementary applications that together support the WINESMART solution.

## 4. Application Objective
The objective of WINESMART is to develop a prototype rover capable of mapping vineyards and dynamically spraying pesticides at the required dosage, only in the areas that need treatment.

The system relies on AI-based perception and environmental intelligence to:
- Build 2D maps of vine foliage
- Detect diseases and infection risks
- Optimize pesticide usage
- Reduce product waste by spraying only where leaves or grapes are present

## 5. Use Case Description
WINESMART is designed for precision viticulture scenarios where automated or semi-automated vineyard monitoring and treatment are required.

The applications in this repository enable:
- Visual analysis of vine foliage and grapes
- Early detection of vine diseases
- Estimation of disease infection risk using weather forecasts
- Forecasting of rainfall and temperature requirements for healthy vine development

Together, these components support decision-making for intelligent pesticide spraying and vineyard management.

## 6. Organization
Axtron Systems, Lda

## 7. Use Instructions

This repository contains **four Dockerized applications**, each addressing a specific function within WINESMART.

### A. Required Inputs

#### 1. Grape Leaves & Grapes Segmentation
**Purpose:** Detect and segment vine elements (`cluster_leaves`, `leaf`, `grapes`).

```bash
docker run -it -p 8000:8000 grape_leaves_segmentation
```

**Endpoint**
```
POST /segment
```

**Example**
```bash
curl -X POST http://localhost:8000/segment   -F "file=@input_image.jpg"   -H "Content-Type: multipart/form-data"
```

---

#### 2. Vine Disease Detection
**Purpose:** Detect diseases on individual vine leaves.

```bash
docker run -it -p 8001:8001 disease_detection
```

**Endpoint**
```
POST /detect
```

**Example**
```bash
curl -X POST http://localhost:8001/detect   -F "file=@sample1.jpg"   -H "Content-Type: multipart/form-data"
```

> Performance is improved when running with `nvidia-container-toolkit`.

---

#### 3. Disease Risk Estimator
**Purpose:** Estimate primary infection risk based on weather forecasts.

```bash
docker run -it -p 8003:8003 disease_risk_estimator
```

**Endpoint**
```
GET /risk
```

**Example**
```bash
curl "http://localhost:8003/risk?lat=38.7&lon=-8.8&days=7"
```

---

#### 4. Rainfall Requirement Predictor
**Purpose:** Forecast temperature and estimate rainfall needed for vine water balance.

```bash
docker run -it -p 8002:8002 rainfall_requirement
```

**Endpoint**
```
GET /predict_required_rain
```

**Example**
```
http://localhost:8002/predict_required_rain?year=2023&lookback=12&months=12&parcel=Algeruz%202
```

---

### B. Expected Outputs

- **Segmentation:** JSON with detected classes and polygon coordinates  
- **Disease Detection:** JSON with detected diseases, confidence scores, and bounding boxes  
- **Disease Risk Estimator:** JSON with daily meteorological metrics and infection risk flags  
- **Rainfall Predictor:** JSON with predicted temperatures, rainfall requirements, soil features, and metadata

