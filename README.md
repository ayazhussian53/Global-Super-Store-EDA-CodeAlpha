
# STEP 1: Import libraries
# ============================================
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

print("="*60)
print("📊 TASK 2 & 3: COMPLETE EDA WITH VISUALIZATIONS")
print("="*60)

# ============================================
# STEP 2: Load and CLEAN data properly
# ============================================
print("\n📂 Loading and cleaning data...")

df = pd.read_csv('c:/Users/786/Downloads/global_super_store_orders.csv')

# PROPER NUMBER CLEANING FUNCTION
def clean_number(value):
    if pd.isna(value):
        return 0.0
    # Convert to string
    val_str = str(value).strip()
    
    # Check if it has comma as decimal (like "4,506" means 4.506)
    if ',' in val_str:
        # If it has exactly one comma and no second comma after
        parts = val_str.split(',')
        if len(parts) == 2 and len(parts[1]) <= 3:
            # This is decimal comma (European format)
            val_str = val_str.replace(',', '.')
        else:
            # This is thousand separator (remove commas)
            val_str = val_str.replace(',', '')
    
    try:
        return float(val_str)
    except:
        return 0.0

# Clean all number columns
for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

print(f"✅ Data cleaned: {len(df)} rows")

# ============================================
# STEP 3: Basic EDA (No charts yet)
# ============================================
print("\n" + "="*60)
print("📊 EDA RESULTS")
print("="*60)

# Total sales and profit (now should be correct)
total_sales = df['Sales'].sum()
total_profit = df['Profit'].sum()

print(f"\n💰 TOTAL SALES: ${total_sales:,.2f}")
print(f"💰 TOTAL PROFIT: ${total_profit:,.2f}")
print(f"📈 PROFIT MARGIN: {(total_profit/total_sales)*100:.2f}%")

# Profit by category
print("\n📦 PROFIT BY CATEGORY:")
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
for cat, profit in category_profit.items():
    print(f"   {cat}: ${profit:,.2f}")

# Check loss making orders
loss_orders = df[df['Profit'] < 0]
print(f"\n⚠️ LOSS MAKING ORDERS: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)")

# Best countries
print("\n🌍 TOP 5 COUNTRIES BY SALES:")
top_countries = df.groupby('Country')['Sales'].sum().nlargest(5)
for country, sales in top_countries.items():
    print(f"   {country}: ${sales:,.2f}")

# ============================================
# STEP 4: VISUALIZATIONS (TASK 3)
# ============================================
print("\n" + "="*60)
print("📊 CREATING VISUALIZATIONS")
print("="*60)

# Create a figure with 4 subplots
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle('Global Super Store Analysis', fontsize=16, fontweight='bold')

# Chart 1: Profit by Category (Bar Chart)
ax1 = axes[0, 0]
category_profit = df.groupby('Category')['Profit'].sum()
colors = ['green' if x > 0 else 'red' for x in category_profit.values]
bars = ax1.bar(category_profit.index, category_profit.values, color=colors)
ax1.set_title('Profit by Category', fontsize=12, fontweight='bold')
ax1.set_ylabel('Profit ($)')
ax1.axhline(y=0, color='black', linestyle='-', linewidth=0.5)
for bar, profit in zip(bars, category_profit.values):
    ax1.text(bar.get_x() + bar.get_width()/2, bar.get_height(),
             f'${profit:,.0f}', ha='center', va='bottom' if profit > 0 else 'top')

# Chart 2: Sales by Category (Pie Chart)
ax2 = axes[0, 1]
category_sales = df.groupby('Category')['Sales'].sum()
ax2.pie(category_sales.values, labels=category_sales.index, autopct='%1.1f%%',
        startangle=90, colors=['#ff9999', '#66b3ff', '#99ff99'])
ax2.set_title('Sales Distribution by Category', fontsize=12, fontweight='bold')

# Chart 3: Top 10 Countries (Horizontal Bar)
ax3 = axes[1, 0]
top_countries = df.groupby('Country')['Sales'].sum().nlargest(10)
ax3.barh(range(len(top_countries)), top_countries.values, color='coral')
ax3.set_yticks(range(len(top_countries)))
ax3.set_yticklabels(top_countries.index)
ax3.set_title('Top 10 Countries by Sales', fontsize=12, fontweight='bold')
ax3.set_xlabel('Sales ($)')
for i, (country, val) in enumerate(top_countries.items()):
    ax3.text(val, i, f'${val:,.0f}', ha='left', va='center')

# Chart 4: Orders by Ship Mode
ax4 = axes[1, 1]
ship_mode = df['Ship Mode'].value_counts()
colors = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728']
bars = ax4.bar(ship_mode.index, ship_mode.values, color=colors)
ax4.set_title('Orders by Shipping Mode', fontsize=12, fontweight='bold')
ax4.set_xlabel('Ship Mode')
ax4.set_ylabel('Number of Orders')
ax4.tick_params(axis='x', rotation=15)
for bar, count in zip(bars, ship_mode.values):
    ax4.text(bar.get_x() + bar.get_width()/2, bar.get_height(),
             str(count), ha='center', va='bottom')

plt.tight_layout()
plt.show()

# ============================================
# STEP 5: Additional Charts
# ============================================

# Chart 5: Discount vs Profit (Scatter Plot)
plt.figure(figsize=(10, 6))
sample_df = df.sample(min(500, len(df)))
plt.scatter(sample_df['Discount'], sample_df['Profit'], alpha=0.5, c='green')
plt.axhline(y=0, color='red', linestyle='--', alpha=0.5)
plt.title('Discount vs Profit Relationship', fontsize=14, fontweight='bold')
plt.xlabel('Discount Rate')
plt.ylabel('Profit ($)')
plt.grid(True, alpha=0.3)
plt.show()

# Chart 6: Profit by Segment (Box Plot)
plt.figure(figsize=(10, 6))
df.boxplot(column='Profit', by='Segment')
plt.title('Profit Distribution by Customer Segment', fontsize=14, fontweight='bold')
plt.suptitle('')
plt.axhline(y=0, color='red', linestyle='--', alpha=0.5)
plt.show()

# Chart 7: Top 10 Products by Profit
plt.figure(figsize=(12, 8))
top_products = df.groupby('Product Name')['Profit'].sum().nlargest(10)
colors = ['green' if x > 0 else 'red' for x in top_products.values]
plt.barh(range(len(top_products)), top_products.values, color=colors)
plt.yticks(range(len(top_products)), [p[:40] + '...' if len(p) > 40 else p for p in top_products.index])
plt.title('Top 10 Products by Profit', fontsize=14, fontweight='bold')
plt.xlabel('Profit ($)')
plt.tight_layout()
plt.show()

# ============================================
# FINAL SUMMARY
# ============================================
print("\n" + "="*60)
print("📊 FINAL ANALYSIS SUMMARY")
print("="*60)

print(f"""
✅ DATA QUALITY:
   • Total Orders: {len(df):,}
   • Total Sales: ${total_sales:,.2f}
   • Total Profit: ${total_profit:,.2f}
   • Profit Margin: {(total_profit/total_sales)*100:.2f}%

📈 KEY INSIGHTS:
   • Best Category: {category_profit.idxmax()} (${category_profit.max():,.2f})
   • Worst Category: {category_profit.idxmin()} (${category_profit.min():,.2f})
   • Best Country: {top_countries.index[0]} (${top_countries.iloc[0]:,.2f})
   • Most Popular Ship Mode: {ship_mode.index[0]} ({ship_mode.iloc[0]} orders)

⚠️ WARNINGS:
   • Loss-making orders: {len(loss_orders)} ({len(loss_orders)/len(df)*100:.1f}%)
   • Check products with negative profit
""")

print("\n🎉 TASK 2 & 3 COMPLETED SUCCESSFULLY!")



import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
df = pd.read_csv('c:/Users/786/Downloads/global_super_store_orders.csv')

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

for col in ['Sales', 'Profit', 'Discount', 'Shipping Cost']:
    df[col] = df[col].apply(clean_number)

df['Order Date'] = pd.to_datetime(df['Order Date'])

print("="*60)
print("📊 REMAINING EDA: TRENDS & PATTERNS")
print("="*60)

# TREND 1: Seasonal Patterns (Month-wise performance)
print("\n📅 SEASONAL TREND ANALYSIS:")
df['Month'] = df['Order Date'].dt.month
monthly_performance = df.groupby('Month').agg({
    'Sales': 'sum',
    'Profit': 'sum',
    'Quantity': 'sum'
}).round(2)

print("Month-wise Performance:")
print(monthly_performance)

# Find best and worst months
best_month = monthly_performance['Profit'].idxmax()
worst_month = monthly_performance['Profit'].idxmin()
print(f"\n🏆 BEST MONTH: {best_month} (Profit: ${monthly_performance.loc[best_month, 'Profit']:,.2f})")
print(f"⚠️ WORST MONTH: {worst_month} (Profit: ${monthly_performance.loc[worst_month, 'Profit']:,.2f})")

# TREND 2: Day of Week Analysis
print("\n📆 DAY OF WEEK TREND:")
df['DayOfWeek'] = df['Order Date'].dt.dayofweek
day_names = {0:'Monday', 1:'Tuesday', 2:'Wednesday', 3:'Thursday', 4:'Friday', 5:'Saturday', 6:'Sunday'}
df['DayName'] = df['DayOfWeek'].map(day_names)

daily_performance = df.groupby('DayName')['Sales'].sum().sort_values(ascending=False)
print(daily_performance)

# PATTERN: Product Affinity (What sells together?)
print("\n🛒 PRODUCT CATEGORY PAIRING PATTERN:")
# Pivot table of categories
category_matrix = pd.crosstab(df['Order ID'], df['Category'])
print("Categories often bought together?")
print(category_matrix.corr())

# Visualize trends
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Monthly sales trend
axes[0].plot(monthly_performance.index, monthly_performance['Sales'], marker='o', linewidth=2)
axes[0].set_title('Monthly Sales Trend', fontsize=12, fontweight='bold')
axes[0].set_xlabel('Month')
axes[0].set_ylabel('Sales ($)')
axes[0].grid(True, alpha=0.3)

# Day of week sales
axes[1].bar(daily_performance.index, daily_performance.values, color='skyblue')
axes[1].set_title('Sales by Day of Week', fontsize=12, fontweight='bold')
axes[1].set_xlabel('Day')
axes[1].set_ylabel('Sales ($)')
axes[1].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()
