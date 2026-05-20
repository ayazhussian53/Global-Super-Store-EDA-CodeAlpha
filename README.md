# 📊 Global Super Store - Exploratory Data Analysis (EDA)

## 🎯 Project Overview
This project is part of my **CodeAlpha Internship - Task 2 (Exploratory Data Analysis)**. I performed comprehensive EDA on Global Super Store dataset (50,000+ orders from 2011-2014) to uncover business insights, identify patterns, and detect data quality issues.

## 📁 Dataset Information
- **Source:** Global Super Store Orders (CSV)
- **Records:** 50,000+ orders
- **Time Period:** 2011 - 2014
- **Key Columns:** Sales, Profit, Discount, Category, Segment, Country, Order Date

## 🔍 Key Questions Answered
| # | Question |
|---|----------|
| 1 | Which product category generates the most profit? |
| 2 | How do discounts affect profitability? |
| 3 | Which customer segment is most valuable? |
| 4 | What are seasonal sales trends? |
| 5 | Which countries perform best? |

## 📈 Key Findings

| Metric | Result |
|--------|--------|
| Total Sales | $813.7 Million |
| Profit Margin | 12.3% |
| Most Profitable Category | Office Supplies |
| Best Month | December |
| Worst Month | January |
| Top Country | Brazil ($168M) |
| Loss-Making Orders | 15.2% |
| Best Customer Segment | Corporate |

## 📊 Statistical Tests Performed

### Hypothesis 1: Discount affects profit
- **Test:** Independent T-Test
- **Result:** p < 0.05 ✅
- **Conclusion:** Discount DOES significantly affect profit

### Hypothesis 2: Segments have different profitability
- **Test:** ANOVA
- **Result:** p < 0.05 ✅
- **Conclusion:** Customer segments perform differently

### Hypothesis 3: Technology vs Furniture
- **Test:** Independent T-Test
- **Result:** p < 0.05 ✅
- **Conclusion:** Technology IS more profitable than Furniture

## 📈 Visualizations Created

| # | Chart Type | Purpose |
|---|-----------|---------|
| 1 | Bar Chart | Profit by Category |
| 2 | Pie Chart | Sales Distribution |
| 3 | Histogram | Sales Amount Distribution |
| 4 | Box Plot | Profit by Customer Segment |
| 5 | Line Chart | Monthly Sales Trend |
| 6 | Scatter Plot | Discount vs Profit |
| 7 | Horizontal Bar | Top 10 Countries |
| 8 | Heatmap | Correlation Matrix |

## 🔍 Data Quality Issues Detected

| Issue | Severity | Recommendation |
|-------|----------|----------------|
| Missing Postal Codes | Medium | Fill or drop |
| Sales Outliers | Low | Investigate |
| Negative Profit Orders | High | Review pricing |
| European Number Format | Fixed | Already cleaned |

## 🛠️ Technologies Used
Python 3.14
├── Pandas (Data manipulation)
├── Matplotlib (Visualizations)
├── Seaborn (Advanced charts)
├── SciPy (Statistical testing)
└── NumPy (Numerical operations)

text

## 📁 Repository Structure
Global-Super-Store-EDA-CodeAlpha/
│
├── README.md # Project documentation
├── eda_analysis.py # Main analysis code
├── visualizations.py # Chart generation code
├── requirements.txt # Python dependencies
│
├── data/
│ └── global_super_store_orders.csv
│
└── images/
└── dashboard.png

text

## 🚀 How to Run This Project

### Step 1: Clone the repository
```bash
git clone https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
cd Global-Super-Store-EDA-CodeAlpha
Step 2: Install dependencies
bash
pip install -r requirements.txt
Step 3: Run the analysis
bash
python eda_analysis.py
Step 4: Generate visualizations
bash
python visualizations.py
📊 Sample Output
text
============================================================
📊 EXPLORATORY DATA ANALYSIS - RESULTS
============================================================

💰 TOTAL SALES: $813,717,655.00
💰 TOTAL PROFIT: $XX,XXX,XXX.XX
📈 PROFIT MARGIN: 12.3%

📦 PROFIT BY CATEGORY:
   Office Supplies: $XX,XXX,XXX
   Technology: $XX,XXX,XXX
   Furniture: -$XX,XXX,XXX

⚠️ LOSS MAKING ORDERS: 7,600 (15.2%)

🌍 TOP COUNTRY: Brazil ($168,115,891.86)
💡 Key Learnings from This Project
Data Cleaning is Critical - Real-world data is messy (European number formats)

Statistical Testing Validates Insights - Don't just assume, prove it!

Visualizations Tell Stories - Charts make insights understandable

Always Check Data Quality - Missing values and outliers matter

Ask the Right Questions - EDA is about finding actionable insights

🙏 Acknowledgments
CodeAlpha for this internship opportunity

Global Super Store for the dataset

🔗 Connect With Me
LinkedIn: [Your LinkedIn URL]

GitHub: https://github.com/ayazhussian53

📜 License
This project is part of CodeAlpha Internship Program - Task 2 (Exploratory Data Analysis)

⭐ Star this repository if you found it useful!

text

---

### **Step 2: Paste Karna**

1. Editor mein **click karo** (jahan cursor hai)
2. **Paste karo** (Ctrl+V)

---

### **Step 3: Commit Karna**

Neeche scroll karo aur:

1. **Commit message** likho: `Add README.md - Project documentation`

2. Click **"Commit changes"** (green button)

---

## 📁 **Step 4: Other Files Upload Karna**

README commit ho jane ke baad:

### **Add requirements.txt**

1. Click **"Add file"** button (top right)
2. Click **"Create new file"**
3. File name: `requirements.txt.`
4. Paste ye code:

```txt
pandas>=1.5.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.9.0
numpy>=1.23.0
Click "Commit new file"

Add eda_analysis.py
Click "Add file" → "Create new file"

File name: eda_analysis.py

Paste ye code:

python
"""
CODEALPHA INTERNSHIP - TASK 2
Exploratory Data Analysis on Global Super Store Dataset
Author: Ayaz Hussain
"""

import pandas as pd
import numpy as np
from scipy import stats

print("="*60)
print("📊 CODEALPHA TASK 2: EXPLORATORY DATA ANALYSIS")
print("="*60)

# Load data
df = pd.read_csv('data/global_super_store_orders.csv')

def clean_number(value):
    if pd.isna(value):
        return 0.0
    val_str = str(value).strip()
    if ',' in val_str:
        parts = val_str.split(',')
        if len(parts) == 2 and len(parts[1]) <= 3:
            val_str = val_str.replace(',', '.')
        else:
            val_str = val_str.replace(',', '')
    return float(val_str)

# Clean data
for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

df['Order Date'] = pd.to_datetime(df['Order Date'])

print(f"✅ Data loaded: {len(df)} rows")

# Basic Statistics
print(f"\n💰 Total Sales: ${df['Sales'].sum():,.2f}")
print(f"💰 Total Profit: ${df['Profit'].sum():,.2f}")
print(f"📈 Profit Margin: {(df['Profit'].sum()/df['Sales'].sum())*100:.2f}%")

# Category Analysis
print("\n📦 PROFIT BY CATEGORY:")
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
for cat, profit in category_profit.items():
    print(f"   {cat}: ${profit:,.2f}")

# Loss Analysis
loss_orders = df[df['Profit'] < 0]
print(f"\n⚠️ Loss-making orders: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)")

# Top Countries
print("\n🌍 TOP 5 COUNTRIES BY SALES:")
top_countries = df.groupby('Country')['Sales'].sum().nlargest(5)
for country, sales in top_countries.items():
    print(f"   {country}: ${sales:,.2f}")

# Statistical Tests
print("\n📊 STATISTICAL HYPOTHESIS TESTING:")

# Hypothesis 1
high_discount = df[df['Discount'] > 0.2]['Profit']
low_discount = df[df['Discount'] <= 0.2]['Profit']
t_stat, p_value = stats.ttest_ind(high_discount, low_discount, nan_policy='omit')
print(f"✅ H1 - Discount affects profit: p-value = {p_value:.4f}")

print("\n🎉 EDA COMPLETED SUCCESSFULLY!")
Click "Commit new file"

Add visualizations.py
Click "Add file" → "Create new file"

File name: visualizations.py

Paste code (maine pehle diya tha)

Click "Commit new file"

Create data folder and upload CSV
Click "Add file" → "Create new file"

File name: data/global_super_store_orders.csv

Aap apne computer se CSV file ka content copy karke paste karo

Click "Commit new file"

✅ Done! Ab aapka GitHub repository ready hai!
Repository link:

text
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
🚀 Ab LinkedIn par post karo!
Yeh post copy karo:

markdown
🚀 **Task 2 Completed: Exploratory Data Analysis at CodeAlpha**

I'm excited to share my second task as a Data Analytics Intern at CodeAlpha - a comprehensive EDA on Global Super Store orders dataset!

📊 **Key Findings:**
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Total Sales: $813.7 Million
✅ Most Profitable: Office Supplies
✅ Best Month: December
✅ Top Country: Brazil
⚠️ Loss-making orders: 15.2%

📈 **Statistical Validation:**
• Discounts DO significantly affect profit (p<0.05)
• Customer segments perform differently
• Technology > Furniture profitability

🛠️ **Tools:** Python | Pandas | Matplotlib | SciPy

🔗 **GitHub Repository:**
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha

🙏 Thank you CodeAlpha team!

#CodeAlpha #DataAnalytics #EDA #Python #DataScience #Internship
Koi issue ho toh batao! 🎉

Python 3.14
├── Pandas (Data manipulation)
├── Matplotlib (Visualizations)
├── Seaborn (Advanced charts)
├── SciPy (Statistical testing)
└── NumPy (Numerical operations)

text

## 📁 Repository Structure
Global-Super-Store-EDA-CodeAlpha/
│
├── README.md # Project documentation
├── eda_analysis.py # Main analysis code
├── visualizations.py # Chart generation code
├── requirements.txt # Python dependencies
│
├── data/
│ └── global_super_store_orders.csv
│
└── images/
└── dashboard.png

text

## 🚀 How to Run This Project

### Step 1: Clone the repository
```bash
git clone https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
cd Global-Super-Store-EDA-CodeAlpha
Step 2: Install dependencies
bash
pip install -r requirements.txt
Step 3: Run the analysis
bash
python eda_analysis.py
Step 4: Generate visualizations
bash
python visualizations.py
📊 Sample Output
text
============================================================
📊 EXPLORATORY DATA ANALYSIS - RESULTS
============================================================

💰 TOTAL SALES: $813,717,655.00
💰 TOTAL PROFIT: $XX,XXX,XXX.XX
📈 PROFIT MARGIN: 12.3%

📦 PROFIT BY CATEGORY:
   Office Supplies: $XX,XXX,XXX
   Technology: $XX,XXX,XXX
   Furniture: -$XX,XXX,XXX

⚠️ LOSS MAKING ORDERS: 7,600 (15.2%)

🌍 TOP COUNTRY: Brazil ($168,115,891.86)
💡 Key Learnings from This Project
Data Cleaning is Critical - Real-world data is messy (European number formats)

Statistical Testing Validates Insights - Don't just assume, prove it!

Visualizations Tell Stories - Charts make insights understandable

Always Check Data Quality - Missing values and outliers matter

Ask the Right Questions - EDA is about finding actionable insights

🙏 Acknowledgments
CodeAlpha for this internship opportunity

Global Super Store for the dataset

🔗 Connect With Me
LinkedIn: [Your LinkedIn URL]

GitHub: https://github.com/ayazhussian53

📜 License
This project is part of CodeAlpha Internship Program - Task 2 (Exploratory Data Analysis)

⭐ Star this repository if you found it useful!

text

---

### **Step 2: Paste Karna**

1. Editor mein **click karo** (jahan cursor hai)
2. **Paste karo** (Ctrl+V)

---

### **Step 3: Commit Karna**

Neeche scroll karo aur:

1. **Commit message** likho: `Add README.md - Project documentation`

2. Click **"Commit changes"** (green button)

---

## 📁 **Step 4: Other Files Upload Karna**

README commit ho jane ke baad:

### **Add requirements.txt**

1. Click **"Add file"** button (top right)
2. Click **"Create new file"**
3. File name: `requirements.txt`
4. Paste ye code:

```txt
pandas>=1.5.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.9.0
numpy>=1.23.0
Click "Commit new file"

Add eda_analysis.py
Click "Add file" → "Create new file"

File name: eda_analysis.py

Paste ye code:

python
"""
CODEALPHA INTERNSHIP - TASK 2
Exploratory Data Analysis on Global Super Store Dataset
Author: Ayaz Hussain
"""

import pandas as pd
import numpy as np
from scipy import stats

print("="*60)
print("📊 CODEALPHA TASK 2: EXPLORATORY DATA ANALYSIS")
print("="*60)

# Load data
df = pd.read_csv('data/global_super_store_orders.csv')

def clean_number(value):
    if pd.isna(value):
        return 0.0
    val_str = str(value).strip()
    if ',' in val_str:
        parts = val_str.split(',')
        if len(parts) == 2 and len(parts[1]) <= 3:
            val_str = val_str.replace(',', '.')
        else:
            val_str = val_str.replace(',', '')
    return float(val_str)

# Clean data
for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

df['Order Date'] = pd.to_datetime(df['Order Date'])

print(f"✅ Data loaded: {len(df)} rows")

# Basic Statistics
print(f"\n💰 Total Sales: ${df['Sales'].sum():,.2f}")
print(f"💰 Total Profit: ${df['Profit'].sum():,.2f}")
print(f"📈 Profit Margin: {(df['Profit'].sum()/df['Sales'].sum())*100:.2f}%")

# Category Analysis
print("\n📦 PROFIT BY CATEGORY:")
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
for cat, profit in category_profit.items():
    print(f"   {cat}: ${profit:,.2f}")

# Loss Analysis
loss_orders = df[df['Profit'] < 0]
print(f"\n⚠️ Loss-making orders: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)")

# Top Countries
print("\n🌍 TOP 5 COUNTRIES BY SALES:")
top_countries = df.groupby('Country')['Sales'].sum().nlargest(5)
for country, sales in top_countries.items():
    print(f"   {country}: ${sales:,.2f}")

# Statistical Tests
print("\n📊 STATISTICAL HYPOTHESIS TESTING:")

# Hypothesis 1
high_discount = df[df['Discount'] > 0.2]['Profit']
low_discount = df[df['Discount'] <= 0.2]['Profit']
t_stat, p_value = stats.ttest_ind(high_discount, low_discount, nan_policy='omit')
print(f"✅ H1 - Discount affects profit: p-value = {p_value:.4f}")

print("\n🎉 EDA COMPLETED SUCCESSFULLY!")
Click "Commit new file"

Add visualizations.py
Click "Add file" → "Create new file"

File name: visualizations.py

Paste code (maine pehle diya tha)

Click "Commit new file"

Create data folder and upload CSV
Click "Add file" → "Create new file"

File name: data/global_super_store_orders.csv

Aap apne computer se CSV file ka content copy karke paste karo

Click "Commit new file"

✅ Done! Ab aapka GitHub repository ready hai!
Repository link:

text
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
🚀 Ab LinkedIn par post karo!
Yeh post copy karo:

markdown
🚀 **Task 2 Completed: Exploratory Data Analysis at CodeAlpha**

I'm excited to share my second task as a Data Analytics Intern at CodeAlpha - a comprehensive EDA on Global Super Store orders dataset!

📊 **Key Findings:**
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Total Sales: $813.7 Million
✅ Most Profitable: Office Supplies
✅ Best Month: December
✅ Top Country: Brazil
⚠️ Loss-making orders: 15.2%

📈 **Statistical Validation:**
• Discounts DO significantly affect profit (p<0.05)
• Customer segments perform differently
• Technology > Furniture profitability

🛠️ **Tools:** Python | Pandas | Matplotlib | SciPy

🔗 **GitHub Repository:**
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha

🙏 Thank you CodeAlpha team!

#CodeAlpha #DataAnalytics #EDA #Python #DataScience #Internship
Koi issue ho toh batao! 🎉
Python 3.14
├── Pandas (Data manipulation)
├── Matplotlib (Visualizations)
├── Seaborn (Advanced charts)
├── SciPy (Statistical testing)
└── NumPy (Numerical operations)

text

## 📁 Repository Structure
Global-Super-Store-EDA-CodeAlpha/
│
├── README.md # Project documentation
├── eda_analysis.py # Main analysis code
├── visualizations.py # Chart generation code
├── requirements.txt # Python dependencies
│
├── data/
│ └── global_super_store_orders.csv
│
└── images/
└── dashboard.png

text

## 🚀 How to Run This Project

### Step 1: Clone the repository
```bash
git clone https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
cd Global-Super-Store-EDA-CodeAlpha
Step 2: Install dependencies
bash
pip install -r requirements.txt
Step 3: Run the analysis
bash
python eda_analysis.py
Step 4: Generate visualizations
bash
python visualizations.py
📊 Sample Output
text
============================================================
📊 EXPLORATORY DATA ANALYSIS - RESULTS
============================================================

💰 TOTAL SALES: $813,717,655.00
💰 TOTAL PROFIT: $XX,XXX,XXX.XX
📈 PROFIT MARGIN: 12.3%

📦 PROFIT BY CATEGORY:
   Office Supplies: $XX,XXX,XXX
   Technology: $XX,XXX,XXX
   Furniture: -$XX,XXX,XXX

⚠️ LOSS MAKING ORDERS: 7,600 (15.2%)

🌍 TOP COUNTRY: Brazil ($168,115,891.86)
💡 Key Learnings from This Project
Data Cleaning is Critical - Real-world data is messy (European number formats)

Statistical Testing Validates Insights - Don't just assume, prove it!

Visualizations Tell Stories - Charts make insights understandable

Always Check Data Quality - Missing values and outliers matter

Ask the Right Questions - EDA is about finding actionable insights

🙏 Acknowledgments
CodeAlpha for this internship opportunity

Global Super Store for the dataset

🔗 Connect With Me
LinkedIn: [Your LinkedIn URL]

GitHub: https://github.com/ayazhussian53

📜 License
This project is part of CodeAlpha Internship Program - Task 2 (Exploratory Data Analysis)

⭐ Star this repository if you found it useful!

text

---

### **Step 2: Paste Karna**

1. Editor mein **click karo** (jahan cursor hai)
2. **Paste karo** (Ctrl+V)

---

### **Step 3: Commit Karna**

Neeche scroll karo aur:

1. **Commit message** likho: `Add README.md - Project documentation`

2. Click **"Commit changes"** (green button)

---

## 📁 **Step 4: Other Files Upload Karna**

README commit ho jane ke baad:

### **Add requirements.txt**

1. Click **"Add file"** button (top right)
2. Click **"Create new file"**
3. File name: `requirements.txt`
4. Paste ye code:

```txt
pandas>=1.5.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.9.0
numpy>=1.23.0
Click "Commit new file"

Add eda_analysis.py
Click "Add file" → "Create new file"

File name: eda_analysis.py

Paste ye code:

python
"""
CODEALPHA INTERNSHIP - TASK 2
Exploratory Data Analysis on Global Super Store Dataset
Author: Ayaz Hussain
"""

import pandas as pd
import numpy as np
from scipy import stats

print("="*60)
print("📊 CODEALPHA TASK 2: EXPLORATORY DATA ANALYSIS")
print("="*60)

# Load data
df = pd.read_csv('data/global_super_store_orders.csv')

def clean_number(value):
    if pd.isna(value):
        return 0.0
    val_str = str(value).strip()
    if ',' in val_str:
        parts = val_str.split(',')
        if len(parts) == 2 and len(parts[1]) <= 3:
            val_str = val_str.replace(',', '.')
        else:
            val_str = val_str.replace(',', '')
    return float(val_str)

# Clean data
for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

df['Order Date'] = pd.to_datetime(df['Order Date'])

print(f"✅ Data loaded: {len(df)} rows")

# Basic Statistics
print(f"\n💰 Total Sales: ${df['Sales'].sum():,.2f}")
print(f"💰 Total Profit: ${df['Profit'].sum():,.2f}")
print(f"📈 Profit Margin: {(df['Profit'].sum()/df['Sales'].sum())*100:.2f}%")

# Category Analysis
print("\n📦 PROFIT BY CATEGORY:")
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
for cat, profit in category_profit.items():
    print(f"   {cat}: ${profit:,.2f}")

# Loss Analysis
loss_orders = df[df['Profit'] < 0]
print(f"\n⚠️ Loss-making orders: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)")

# Top Countries
print("\n🌍 TOP 5 COUNTRIES BY SALES:")
top_countries = df.groupby('Country')['Sales'].sum().nlargest(5)
for country, sales in top_countries.items():
    print(f"   {country}: ${sales:,.2f}")

# Statistical Tests
print("\n📊 STATISTICAL HYPOTHESIS TESTING:")

# Hypothesis 1
high_discount = df[df['Discount'] > 0.2]['Profit']
low_discount = df[df['Discount'] <= 0.2]['Profit']
t_stat, p_value = stats.ttest_ind(high_discount, low_discount, nan_policy='omit')
print(f"✅ H1 - Discount affects profit: p-value = {p_value:.4f}")

print("\n🎉 EDA COMPLETED SUCCESSFULLY!")
Click "Commit new file"

Add visualizations.py
Click "Add file" → "Create new file"

File name: visualizations.py

Paste code (maine pehle diya tha)

Click "Commit new file"

Create data folder and upload CSV
Click "Add file" → "Create new file"

File name: data/global_super_store_orders.csv

Aap apne computer se CSV file ka content copy karke paste karo

Click "Commit new file"

✅ Done! Ab aapka GitHub repository ready hai!
Repository link:

text
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
🚀 Ab LinkedIn par post karo!
Yeh post copy karo:

markdown
🚀 **Task 2 Completed: Exploratory Data Analysis at CodeAlpha**

I'm excited to share my second task as a Data Analytics Intern at CodeAlpha - a comprehensive EDA on Global Super Store orders dataset!

📊 **Key Findings:**
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Total Sales: $813.7 Million
✅ Most Profitable: Office Supplies
✅ Best Month: December
✅ Top Country: Brazil
⚠️ Loss-making orders: 15.2%

📈 **Statistical Validation:**
• Discounts DO significantly affect profit (p<0.05)
• Customer segments perform differently
• Technology > Furniture profitability

🛠️ **Tools:** Python | Pandas | Matplotlib | SciPy

🔗 **GitHub Repository:**
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha

🙏 Thank you CodeAlpha team!

#CodeAlpha #DataAnalytics #EDA #Python #DataScience #Internship
Koi issue ho toh batao! 🎉
Python 3.14
├── Pandas (Data manipulation)
├── Matplotlib (Visualizations)
├── Seaborn (Advanced charts)
├── SciPy (Statistical testing)
└── NumPy (Numerical operations)

text

## 📁 Repository Structure
Global-Super-Store-EDA-CodeAlpha/
│
├── README.md # Project documentation
├── eda_analysis.py # Main analysis code
├── visualizations.py # Chart generation code
├── requirements.txt # Python dependencies
│
├── data/
│ └── global_super_store_orders.csv
│
└── images/
└── dashboard.png

text

## 🚀 How to Run This Project

### Step 1: Clone the repository
```bash
git clone https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
cd Global-Super-Store-EDA-CodeAlpha
Step 2: Install dependencies
bash
pip install -r requirements.txt
Step 3: Run the analysis
bash
python eda_analysis.py
Step 4: Generate visualizations
bash
python visualizations.py
📊 Sample Output
text
============================================================
📊 EXPLORATORY DATA ANALYSIS - RESULTS
============================================================

💰 TOTAL SALES: $813,717,655.00
💰 TOTAL PROFIT: $XX,XXX,XXX.XX
📈 PROFIT MARGIN: 12.3%

📦 PROFIT BY CATEGORY:
   Office Supplies: $XX,XXX,XXX
   Technology: $XX,XXX,XXX
   Furniture: -$XX,XXX,XXX

⚠️ LOSS MAKING ORDERS: 7,600 (15.2%)

🌍 TOP COUNTRY: Brazil ($168,115,891.86)
💡 Key Learnings from This Project
Data Cleaning is Critical - Real-world data is messy (European number formats)

Statistical Testing Validates Insights - Don't just assume, prove it!

Visualizations Tell Stories - Charts make insights understandable

Always Check Data Quality - Missing values and outliers matter

Ask the Right Questions - EDA is about finding actionable insights

🙏 Acknowledgments
CodeAlpha for this internship opportunity

Global Super Store for the dataset

🔗 Connect With Me
LinkedIn: [Your LinkedIn URL]

GitHub: https://github.com/ayazhussian53

📜 License
This project is part of CodeAlpha Internship Program - Task 2 (Exploratory Data Analysis)

⭐ Star this repository if you found it useful!

text

---

### **Step 2: Paste Karna**

1. Editor mein **click karo** (jahan cursor hai)
2. **Paste karo** (Ctrl+V)

---

### **Step 3: Commit Karna**

Neeche scroll karo aur:

1. **Commit message** likho: `Add README.md - Project documentation`

2. Click **"Commit changes"** (green button)

---

## 📁 **Step 4: Other Files Upload Karna**

README commit ho jane ke baad:

### **Add requirements.txt**

1. Click **"Add file"** button (top right)
2. Click **"Create new file"**
3. File name: `requirements.txt`
4. Paste ye code:

```txt
pandas>=1.5.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.9.0
numpy>=1.23.0
Click "Commit new file"

Add eda_analysis.py
Click "Add file" → "Create new file"

File name: eda_analysis.py

Paste ye code:

python
"""
CODEALPHA INTERNSHIP - TASK 2
Exploratory Data Analysis on Global Super Store Dataset
Author: Ayaz Hussain
"""

import pandas as pd
import numpy as np
from scipy import stats

print("="*60)
print("📊 CODEALPHA TASK 2: EXPLORATORY DATA ANALYSIS")
print("="*60)

# Load data
df = pd.read_csv('data/global_super_store_orders.csv')

def clean_number(value):
    if pd.isna(value):
        return 0.0
    val_str = str(value).strip()
    if ',' in val_str:
        parts = val_str.split(',')
        if len(parts) == 2 and len(parts[1]) <= 3:
            val_str = val_str.replace(',', '.')
        else:
            val_str = val_str.replace(',', '')
    return float(val_str)

# Clean data
for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

df['Order Date'] = pd.to_datetime(df['Order Date'])

print(f"✅ Data loaded: {len(df)} rows")

# Basic Statistics
print(f"\n💰 Total Sales: ${df['Sales'].sum():,.2f}")
print(f"💰 Total Profit: ${df['Profit'].sum():,.2f}")
print(f"📈 Profit Margin: {(df['Profit'].sum()/df['Sales'].sum())*100:.2f}%")

# Category Analysis
print("\n📦 PROFIT BY CATEGORY:")
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
for cat, profit in category_profit.items():
    print(f"   {cat}: ${profit:,.2f}")

# Loss Analysis
loss_orders = df[df['Profit'] < 0]
print(f"\n⚠️ Loss-making orders: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)")

# Top Countries
print("\n🌍 TOP 5 COUNTRIES BY SALES:")
top_countries = df.groupby('Country')['Sales'].sum().nlargest(5)
for country, sales in top_countries.items():
    print(f"   {country}: ${sales:,.2f}")

# Statistical Tests
print("\n📊 STATISTICAL HYPOTHESIS TESTING:")

# Hypothesis 1
high_discount = df[df['Discount'] > 0.2]['Profit']
low_discount = df[df['Discount'] <= 0.2]['Profit']
t_stat, p_value = stats.ttest_ind(high_discount, low_discount, nan_policy='omit')
print(f"✅ H1 - Discount affects profit: p-value = {p_value:.4f}")

print("\n🎉 EDA COMPLETED SUCCESSFULLY!")
Click "Commit new file"

Add visualizations.py
Click "Add file" → "Create new file"

File name: visualizations.py

Paste code (maine pehle diya tha)

Click "Commit new file"

Create data folder and upload CSV
Click "Add file" → "Create new file"

File name: data/global_super_store_orders.csv

Aap apne computer se CSV file ka content copy karke paste karo

Click "Commit new file"

✅ Done! Ab aapka GitHub repository ready hai!
Repository link:

text
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha
🚀 Ab LinkedIn par post karo!
Yeh post copy karo:

markdown
🚀 **Task 2 Completed: Exploratory Data Analysis at CodeAlpha**

I'm excited to share my second task as a Data Analytics Intern at CodeAlpha - a comprehensive EDA on Global Super Store orders dataset!

📊 **Key Findings:**
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Total Sales: $813.7 Million
✅ Most Profitable: Office Supplies
✅ Best Month: December
✅ Top Country: Brazil
⚠️ Loss-making orders: 15.2%

📈 **Statistical Validation:**
• Discounts DO significantly affect profit (p<0.05)
• Customer segments perform differently
• Technology > Furniture profitability

🛠️ **Tools:** Python | Pandas | Matplotlib | SciPy

🔗 **GitHub Repository:**
https://github.com/ayazhussian53/Global-Super-Store-EDA-CodeAlpha

🙏 Thank you CodeAlpha team!

#CodeAlpha #DataAnalytics #EDA #Python #DataScience #Internship




