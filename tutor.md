# Python 機器學習專案建立指南

## 目錄
1. [專案環境建立](#1-專案環境建立)
2. [虛擬環境設定](#2-虛擬環境設定)
3. [套件安裝](#3-套件安裝)
4. [Jupyter Notebook 設定](#4-jupyter-notebook-設定)
5. [資料載入與顯示](#5-資料載入與顯示)
6. [常見問題解決](#6-常見問題解決)

---

## 1. 專案環境建立

### 1.1 建立專案資料夾
```bash
# 建立專案目錄
mkdir bank-analysis
cd bank-analysis

# 檢查目錄結構
ls -la
```
j
### 1.2 準備資料檔案
確保您的 CSV 資料檔案放在專案根目錄下：
```
bank-analysis/
├── bank-full.csv          # 您的資料檔案
└── Bank(self).ipynb       # Jupyter Notebook 檔案
```

---

## 2. 虛擬環境設定

### 2.1 什麼是虛擬環境？
虛擬環境是 Python 的獨立工作空間，可以：
- 隔離不同專案的套件依賴
- 避免套件版本衝突
- 確保專案的可重現性

### 2.2 建立虛擬環境
```bash
# 使用 Python 內建的 venv 模組建立虛擬環境
python3 -m venv .venv

# 檢查虛擬環境是否建立成功
ls -la .venv/
```

輸出應該包含：
```
drwxr-xr-x  7 user  staff  224 Oct 21 XX:XX bin/
drwxr-xr-x  2 user  staff   64 Oct 21 XX:XX include/
drwxr-xr-x  3 user  staff   96 Oct 21 XX:XX lib/
-rw-r--r--  1 user  staff  115 Oct 21 XX:XX pyvenv.cfg
```

### 2.3 啟動虛擬環境
```bash
# macOS/Linux
source .venv/bin/activate

# Windows (如果使用 Windows)
# .venv\Scripts\activate

# 確認虛擬環境已啟動 (命令列前會出現 (.venv))
(.venv) $ which python
```

---

## 3. 套件安裝

### 3.1 更新 pip
```bash
# 更新 pip 到最新版本
pip install --upgrade pip
```

### 3.2 安裝基本套件
```bash
# 安裝 Jupyter 相關套件
pip install jupyter jupyterlab ipykernel

# 安裝資料分析套件
pip install pandas numpy matplotlib seaborn

# 安裝機器學習套件
pip install scikit-learn

# 檢查已安裝的套件
pip list
```

預期輸出範例：
```
Package            Version
------------------ -----------
appnope            0.1.4
asttokens          3.0.0
comm               0.2.3
debugpy            1.8.17
decorator          5.2.1
executing          2.2.1
ipykernel          6.31.0
ipython            8.18.1
jedi               0.19.2
jupyter_client     8.6.3
jupyter_core       5.8.1
matplotlib-inline  0.1.7
nest-asyncio       1.6.0
packaging          25.0
pandas             2.0.3
parso              0.8.5
pexpect            4.9.0
pip                21.2.4
...
```

### 3.3 建立 requirements.txt
```bash
# 產生套件需求檔案
pip freeze > requirements.txt

# 檢查檔案內容
cat requirements.txt
```

---

## 4. Jupyter Notebook 設定

### 4.1 在 VS Code 中開啟 Notebook

1. 開啟 VS Code
2. 開啟專案資料夾：`File` → `Open Folder` → 選擇 `bank-analysis`
3. 建立新的 Notebook：`File` → `New File` → 選擇 `Jupyter Notebook`
4. 儲存為 `Bank(self).ipynb`

### 4.2 選擇 Kernel

當您第一次執行 cell 時，VS Code 會要求您選擇 Kernel：

1. 點擊右上角的 "Select Kernel"
2. 選擇 "Python Environments..."
3. 選擇您剛建立的虛擬環境：`.venv (3.9.6)` 或類似名稱

### 4.3 自動設定（透過 VS Code 工具）

VS Code 的 Copilot 可以自動幫您：
- 偵測並啟動適當的 Kernel
- 安裝缺少的套件
- 重新啟動 Kernel

---

## 5. 資料載入與顯示

### 5.1 基本程式碼
在第一個 cell 中輸入：

```python
import pandas as pd

# 載入資料
data = pd.read_csv("bank-full.csv", sep=";")

# 顯示前 5 筆資料
data.head()
```

### 5.2 執行結果
成功執行後會看到類似以下的表格：

```
   age        job  marital   education default  balance housing loan   contact  day month  duration  campaign  pdays  previous poutcome   y
0   58 management  married    tertiary      no     2143     yes   no   unknown    5   may       261         1     -1         0  unknown  no
1   44 technician   single   secondary      no       29     yes   no   unknown    5   may       151         1     -1         0  unknown  no
2   33entrepreneur  married   secondary      no        2     yes  yes   unknown    5   may        76         1     -1         0  unknown  no
3   47 blue-collar  married     unknown      no     1506     yes   no   unknown    5   may        92         1     -1         0  unknown  no
4   33    unknown   single     unknown      no        1      no   no   unknown    5   may       198         1     -1         0  unknown  no
```

### 5.3 常用資料探索指令
```python
# 查看資料基本資訊
print("資料形狀:", data.shape)
print("\n欄位資訊:")
data.info()

# 查看統計摘要
print("\n數值欄位統計:")
data.describe()

# 查看分類欄位的分布
print("\n目標變數分布:")
data['y'].value_counts()
```

---

## 6. 常見問題解決

### 6.1 ModuleNotFoundError: No module named 'pandas'

**問題原因**: Notebook 使用的 Kernel 環境中沒有安裝 pandas

**解決方法**:
1. 確認 Kernel 是否正確選擇虛擬環境
2. 在 Notebook 中執行安裝指令：
   ```python
   !pip install pandas
   ```
3. 或在終端機中：
   ```bash
   pip install pandas
   ```

### 6.2 Kernel 無法啟動

**解決方法**:
1. 重新啟動 Kernel：在 VS Code 中按 `Ctrl+Shift+P` → 搜尋 "Jupyter: Restart Kernel"
2. 重新選擇 Kernel：點擊右上角 Kernel 名稱 → 選擇正確的 Python 環境
3. 重新安裝 ipykernel：
   ```bash
   pip install ipykernel
   ```

### 6.3 檔案路徑錯誤

**常見錯誤**: `FileNotFoundError: [Errno 2] No such file or directory: '/bank-full.csv'`

**解決方法**:
1. 確認檔案確實存在於專案根目錄
2. 使用相對路徑而非絕對路徑：
   ```python
   # 正確 ✅
   data = pd.read_csv("bank-full.csv", sep=";")
   
   # 錯誤 ❌  
   data = pd.read_csv("/bank-full.csv", sep=";")
   ```

### 6.4 虛擬環境未啟動

**檢查方法**:
```bash
# 檢查當前使用的 Python 路徑
which python

# 應該顯示類似：/Users/username/project/.venv/bin/python
```

**解決方法**:
```bash
# 重新啟動虛擬環境
source .venv/bin/activate
```

---

## 7. 專案結構建議

完整的專案結構：
```
bank-analysis/
├── .venv/                 # 虛擬環境 (自動產生)
├── data/                  # 資料檔案目錄
│   └── bank-full.csv
├── notebooks/             # Notebook 檔案目錄
│   └── Bank(self).ipynb
├── src/                   # 原始碼目錄
│   └── utils.py
├── requirements.txt       # 套件需求檔案
├── README.md             # 專案說明
└── tutor.md              # 學習筆記 (本檔案)
```

---

## 8. 下次建立專案的快速流程

```bash
# 1. 建立專案目錄
mkdir new-project && cd new-project

# 2. 建立虛擬環境
python3 -m venv .venv

# 3. 啟動虛擬環境
source .venv/bin/activate

# 4. 安裝套件
pip install pandas jupyter ipykernel

# 5. 啟動 VS Code
code .

# 6. 建立 Notebook 並選擇正確的 Kernel
```

---

## 9. 學習資源

- [Python 虛擬環境官方文檔](https://docs.python.org/3/tutorial/venv.html)
- [Pandas 官方教學](https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/)
- [Jupyter Notebook 基礎教學](https://jupyter.org/documentation)
- [VS Code Python 設定指南](https://code.visualstudio.com/docs/python/python-tutorial)

---

**注意事項**:
- 每次開始工作前記得啟動虛擬環境
- 定期更新 requirements.txt
- 使用版本控制 (Git) 管理專案，但記得將 `.venv/` 加入 `.gitignore`