# AIOT_HW2

# HeartRisk 多元線性回歸分析 (HW2)

## 專案簡介
本專案使用心血管風險資料集 (`heartRisk.csv`)，以 **多元線性回歸 (Multiple Linear Regression)** 預測個人心血管風險分數（Risk），並完整遵循 **CRISP-DM 流程**進行資料分析、建模與評估。  

資料來源：自訂模擬心血管資料集（10 個特徵）  

---

## CRISP-DM 流程與成果

### 1. Business Understanding
- **目標**：預測心血管風險分數，協助醫療風險評估與健康管理  
- **使用場景**：醫療決策、個人健康風險管理  

### 2. Data Understanding
- 讀取 CSV 資料，檢查缺失值、欄位型態  
- 探索資料統計特性與特徵相關性  
- 可視化相關性熱圖發現 `Age`、`Systolic` 與 Risk 相關性較高  

### 3. Data Preparation
- 選擇特徵：`isSmoker`, `isDiabetic`, `Age`, `Systolic`  
- 數值型特徵（Age, Systolic）進行標準化  
- 訓練集 / 測試集比例：80/20  

### 4. Modeling
- 使用 `scikit-learn` 線性回歸建立模型  
- 查看模型係數：判斷特徵對 Risk 的影響方向與大小  

### 5. Model Evaluation
- 指標：
  - MSE: 17.35  
  - RMSE: 4.17  
  - MAE: 3.25  
  - R²: 0.78  
- 實際值 vs 預測值散點圖，顯示模型預測效果良好  
- 殘差分析：近似常態且均勻分布於 0 附近  

### 6. Confidence Interval
- 使用 `statsmodels.OLS()` 計算 95% 信賴區間  
- 預測圖加上灰色誤差線表示信賴區間  

### 7. Deployment
- 模型可儲存為 `heartRisk_model.pkl`，用於後續部署或即時預測  

---

## GPT 與 NotebookLM 輔助內容
- **GPT 輔助內容**：提供程式碼範例、流程規劃、特徵選擇與可視化建議  
- **NotebookLM 摘要**：透過網路研究，多元線性回歸需注意特徵標準化、類別型特徵轉換、殘差檢查，並可用 Lasso 進行特徵篩選  

---

## 程式碼結構
