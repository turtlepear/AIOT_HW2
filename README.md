# AIOT_HW2  
# HeartRisk 多元線性回歸分析 (HW2)

## 📘 專案簡介
本專案使用心血管風險資料集 (`heartRisk.csv`)，以 **多元線性回歸 (Multiple Linear Regression)** 預測個人心血管風險分數（Risk），並完整遵循 **CRISP-DM 流程**進行資料分析、建模與評估。  

> **資料來源：** [ASCVD Heart Risk Dataset (Kaggle)](https://www.kaggle.com/datasets/mokar2001/ascvd-heart-risk)  
> **資料筆數：** 約 1000 筆  
> **特徵數量：** 10 個 (性別、年齡、血壓、膽固醇、糖尿病、吸菸狀態等)  

<img width="1490" height="1221" alt="image" src="https://github.com/user-attachments/assets/7e04ec4e-8a16-49a9-83de-240e26823448" />

---

## 🔄 CRISP-DM 流程與成果

### 1️⃣ Business Understanding
- **任務目標**：建立可解釋的回歸模型，預測心血管風險分數。  
- **應用價值**：
  - 提供醫療人員初步風險評估依據  
  - 幫助個人了解生活習慣（如吸菸、糖尿病）對健康的影響  
  - 為未來導入 AI 醫療決策支援系統奠基  

---

### 2️⃣ Data Understanding
- **資料來源：** Kaggle 公開心血管疾病風險資料集  
- **主要欄位：**
  - `isMale`: 是否為男性  
  - `isBlack`: 是否為黑人  
  - `isSmoker`: 是否吸菸  
  - `isDiabetic`: 是否糖尿病  
  - `isHypertensive`: 是否高血壓  
  - `Age`: 年齡  
  - `Systolic`: 收縮壓  
  - `Cholesterol`: 總膽固醇  
  - `HDL`: 高密度脂蛋白  
  - `Risk`: 預測目標（心血管風險指數）  

📊 **資料統計摘要：**

| 特徵 | count | mean | std | min | 25% | 50% | 75% | max |
|------|-------|------|-----|-----|-----|-----|-----|-----|
| isMale | 1000 | 0.490 | 0.500 | 0 | 0 | 0 | 1 | 1 |
| isBlack | 1000 | 0.530 | 0.499 | 0 | 0 | 1 | 1 | 1 |
| isSmoker | 1000 | 0.516 | 0.500 | 0 | 0 | 1 | 1 | 1 |
| isDiabetic | 1000 | 0.522 | 0.500 | 0 | 0 | 1 | 1 | 1 |
| isHypertensive | 1000 | 0.495 | 0.500 | 0 | 0 | 0 | 1 | 1 |
| Age | 1000 | 59.11 | 11.54 | 40 | 49 | 59 | 69 | 79 |
| Systolic | 1000 | 144.25 | 31.77 | 90 | 117 | 144 | 171 | 200 |
| Cholesterol | 1000 | 164.04 | 20.33 | 130 | 146 | 164 | 182 | 200 |
| HDL | 1000 | 59.60 | 23.86 | 20 | 39 | 59 | 81 | 100 |
| Risk | 1000 | 19.67 | 17.04 | 0.10 | 6.30 | 14.40 | 29.00 | 85.40 |

- 無缺失值，數據品質良好  
- 類別特徵已為 0/1 形式，方便直接使用於回歸模型  

📈 **相關性熱圖（Correlation Heatmap）**
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/ae70483d-3b39-436b-8de3-89dc98c6b4a7" />

觀察結果：
- `Age` 與 `Systolic` 對 `Risk` 具強相關性  
- 類別變數（isSmoker, isDiabetic）對風險有中等正向影響  

---

### 3️⃣ Data Preparation
- **特徵選擇 (Feature Selection)：**
  - 最終使用 4 個特徵：
    ```
    ['isSmoker', 'isDiabetic', 'Age', 'Systolic']
    ```
  - 選擇依據：特徵相關性 + 臨床意義（醫學上確定這些因子與心血管風險高度相關）

- **資料分割 (Train-Test Split)：**
  - 訓練集：80%
  - 測試集：20%

- **資料標準化 (Normalization)：**
  - 使用 `StandardScaler()` 對 `Age` 與 `Systolic` 進行 Z-score 標準化  
  - 類別特徵保持原始 0/1 型態  

---

### 4️⃣ Modeling
使用 `scikit-learn` 建立多元線性回歸模型：

```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train_scaled, y_train)


### 5️⃣ Model Evaluation
| 指標 | 數值 |
|------|------|
| MSE  | 82.1681 |
| RMSE | 9.0647 |
| MAE  | 7.1494 |
| R²   | 0.6952 |

🔹 **實際 vs 預測值散點圖**
<img width="698" height="547" alt="image" src="https://github.com/user-attachments/assets/c7994e4d-2c02-4715-b064-88d7b05d98f2" />

- 模型表現中上，解釋度 R² 約 0.70  
- 實際值 vs 預測值散點圖，顯示模型預測效果良好  
- 殘差分析：近似常態且均勻分布於 0 附近   
<img width="698" height="547" alt="image" src="https://github.com/user-attachments/assets/c7994e4d-2c02-4715-b064-88d7b05d98f2" />


---

## GPT 與 NotebookLM 輔助內容
- **GPT 輔助內容**：提供程式碼範例、流程規劃、特徵選擇與可視化建議  
- **NotebookLM 摘要**：透過網路研究，多元線性回歸需注意特徵標準化、類別型特徵轉換、殘差檢查，並可用 Lasso 進行特徵篩選  
https://notebooklm.google.com/notebook/2e63ffa5-33fd-49c4-a8eb-b20e13511c2d
---

## 程式碼結構
https://colab.research.google.com/drive/1rSGIUb3wJsD9FC_aXredYL0q2CjnLyxJ?usp=sharing
