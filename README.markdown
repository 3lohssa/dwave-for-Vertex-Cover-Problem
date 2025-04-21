# 使用 QUBO 和 D-Wave 解決 Vertex Cover 問題

本儲存庫包含使用二次無約束二元優化（QUBO）和 D-Wave 量子退火求解器實現 Vertex Cover 問題的程式碼。本專案主要針對 `keller4.mis` 資料集以及 ee-class 平台上的其他資料集，作為計算優化作業的一部分。

## 專案概述

Vertex Cover 問題旨在找到一個無向圖中最小的頂點集合，使得每條邊至少有一個端點在該集合中。本專案將問題轉為 QUBO 模型，並使用 D-Wave 的 `DWaveSampler`（量子退火）和 `LeapHybridSampler`（量子-經典混合求解器）進行求解。

## 檔案結構

```
VCP.zip/
│
├── datasets/                   # 存放測資的資料夾
│   ├── keller4.mis             # 主要資料集
│   ├── keller5.mis             # 主要資料集
│   ├── keller6.mis             # 主要資料集
│   ├── p_hat300-1.mis             # 主要資料集
│   ├── p_hat700-1.mis             # 主要資料集
│   ├── p_hat1500-1.mis             # 主要資料集
│
├── main.py                       # 原始碼  
│
├── report.pdf                    # 文件資料夾
│ 
├── result                           # 圖片資料夾
│   
└── README.md               # 本檔案
```

## 如何執行程式

### 1. 準備資料集

- 將 DIMACS 資料集（例如 `keller4.mis`）放入 `datasets/` 資料夾。
- 如需更改檔案路徑，請在程式碼中更新（預設為 `datasets/keller4.mis`）。

### 2. 執行主程式

使用 `DWaveSampler` 求解 `keller4.mis`：

```bash
python main.py
```

- 輸出包含 Vertex Cover 的大小、能量值和驗證結果。
- 注意：由於 `keller4.mis` 規模較大，`DWaveSampler` 可能因嵌入問題失敗。

對於大型資料集或嵌入失敗的情況，使用 `LeapHybridSampler`：

```bash
python main.py
```

### 3. 範例輸出

使用 `LeapHybridSampler` 對 `keller4.mis` 的輸出：

```
Vertex Cover: [1, 3, 5, ..., 171]  # 選中的頂點清單
Size of Vertex Cover: 156
Energy: -4503.0
Valid Vertex Cover: True
```

### 4. 視覺化結果

 資料視覺化圖並使 Vertex Cover 頂點醒目：

- 在程式碼中加入以下內容：

  ```python
  import matplotlib.pyplot as plt
  pos = nx.spring_layout(G)
  nx.draw(G, pos, with_labels=True, node_color=['red' if i in vertex_cover else 'lightblue' for i in G.nodes()])
  plt.show()
  ```
- 執行程式以顯示圖形。

## 參考資料

- D-Wave Ocean SDK：https://docs.ocean.dwavesys.com/
- PyQUBO 文件：https://pyqubo.readthedocs.io/
- DIMACS 圖格式：http://dimacs.rutgers.edu/
- 報告：`report.pdf`，包含 QUBO 公式和實驗結果。

## 聯繫方式

如有問題或疑問，請聯繫 wesley767378@gmail.com。
