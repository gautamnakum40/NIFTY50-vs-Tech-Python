# NIFTY50 VS Technology Sector Analysis
## Overview
This project analyzes the impact of technological advancements on the NIFTY50 index and its individual components over the past 30 years, focusing on significant milestones, sector performance, and key players in the tech industry, particularly TCS. Utilizing historical data from the Yahoo Finance and investing.com, this analysis explores trends, cumulative returns, volatility, and the role of major technological breakthroughs in shaping market dynamics.

## Objective
 - To analyze the historical performance of NIFTY50 and its relationship with the tech sector.
 - To examine market volatility and trends over time.
 - To assess the impact of AI advancements on the stock market.
 - To derive data-driven insights for better investment decision-making.

## Data Sources
  - **Yahoo Finance (`yfinance`)**: Used to fetch historical data for NIFTY50, 
    Big Tech stocks.
  - **investing.com** : Due to the lack of extensive historical NIFTY50 data on Yahoo Finance, we obtained additional data for [NIFTY50](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/nifty_data.csv) and [NIFTY IT](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Nifty%20IT%20Historical%20Data.csv) from Investing.com and used it in .csv format for analysis.
  - Data from 1996–2025 was collected for a long-term analysis of market trends for last 30 years.

## Tools and Technologies Used
  - **Programming Language**: Python
  - **Development Environment**: Jupyter Notebook
  - **Code Editor**: Visual Studio Code
  - **Package Management**: Conda
  - **Data Retrieval**: yfinance (Yahoo Finance API)
  - **Data Analysis and Manipulation**:
       - Pandas
       - NumPy
  - **Data Visualization**:
       - Matplotlib
       - Seaborn
  - **Version Control**: Git and GitHub

## Skills Demonstrated
   - **Data Collection**: Automated fetching of historical stock market data using 
     Python. 
   - **Data Cleaning & Wrangling**: Cleaning and Preprocessing stock data for analysis.
   - **Visualization**: Advanced visualizations of trends, cumulative returns, and volatility using `matplotlib` and `seaborn`.
   - **Statistical Analysis**: Computing yearly returns, cumulative growth, volatility, and key financial insights.
   - **Storytelling**: Annotating visualizations with significant historical and technological events to provide meaningful context.

## Key Areas of Focus:
**1. NIFTY50 Long-Term Trend and Technological Impact:**

Analyze the historical performance of the NIFTY50 over the last 30 years, highlighting patterns during significant economic events and investigating how major technological milestones (e.g., the rise of the internet, smartphones, AI) have influenced the index's trajectory.

**2. Tech-Sector Performance Comparison:**

Compare the performance of the technology sector (represented by the NIFTY IT index) against the NIFTY50, with a focus on the contributions of IT BIG stocks.

**3. Volatility Analysis:**

Assess the volatility of key technology stocks, particularly Nvidia, in relation to the NIFTY50, exploring the implications for investment strategies and risk management.

**4. AI Revolution:**

Examine the correlation between significant AI breakthroughs and TCS stock performance, emphasizing its role as a leader in AI technology and its impact on the broader tech sector.

## Project Structure
### 1. NIFTY50 Long-Term Trend Analysis:
   
[Notebook link](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/1.%20Nifty50%20Market%20Trend%20Analysis.ipynb)

**Question**: What is the trend of the NIFTY50 over the last 30 years?

**Code Snippet:** 

```python
# Read Nifty50 historical data (last 30 years)

nifty50_df = pd.read_csv('nifty_data.csv')
nifty50_df

# change dtype of date
nifty50_df['Date'] = pd.to_datetime(nifty50_df['Date'], format='%d-%m-%Y', errors='coerce')
nifty50_df.dtypes

# Plot the Nifty50  last 30 year trend 
sns.set_theme(style='ticks')

fig, ax = plt.subplots(figsize = (12, 6))

# Plot the data
sns.lineplot(data=nifty50_df, x='Date',y='Close',ax=ax, linewidth=2, color='#007acc')

ax.set_title('Nifty50 Long-Term Trend (Last 30 Years)', fontsize=16,fontweight='bold')
ax.set_xlabel('Year',fontsize=12)
ax.set_ylabel('Nifty50 Close Price', fontsize=12)

# Format x-axis to show years only
ax.xaxis.set_major_formatter(plt.matplotlib.dates.DateFormatter('%Y'))  # Show year only
ax.xaxis.set_major_locator(plt.matplotlib.dates.YearLocator(5)) # 5 year range gap

# Rotate x-axis labels for better readability
plt.xticks(rotation=45)

# add $ sign to y axis
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'₹{x:,.0f}'))

# add gridlines
ax.grid(True, linestyle='--', alpha=0.7)

plt.tight_layout()
plt.show()
```

**Visualization:**

![Nifty50 Long-Term Trend (Last 30 Years)](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/Nifty50%20Market%20Trend%20Analysis.png)

**Insights:**
   - The NIFTY50 has exhibited an overall upward trend over the last 30 years.
   - Sharp declines are visible during major economic downturns, such as the Dot-com Bubble (2000) and the 2008 Financial Crisis, but recovery was steady. 
   
### 1.2 Yearly and Cumulative Returns of NIFTY50:

**Question:** What are the yearly returns of the NIFTY50, and how has cumulative growth evolved?

**Code Snippet:**
```python
# Extract the year from the 'Date' column
nifty50_df['Year'] = nifty50_df['Date'].dt.year

# Calculate yearly returns
nifty50_df['Yearly Return'] = nifty50_df['Close'].pct_change(252) * 100  # cause there are usually 252 trading days in a year

# Group by year and get the last closing price of each year
yearly_returns = nifty50_df.groupby('Year')['Yearly Return'].last()

# Create a df for returns
df_returns = yearly_returns.reset_index()
df_returns.columns = ['Year','Return']

# calculate cumulative returns
df_returns['Cumulative'] = (1 + df_returns['Return'] / 100).cumprod() - 1
```

**Visualization:**

![Nifty50 Yearly Returns and Cumulative Growth (Last 30 Years)](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/yearly%20return%20%20of%20the%20Nify50%20over%20last%2030%20years.png)

**Insights**

 - Best Year:: The highest annual return for the NIFTY50 was in 2009 with over 74% growth.
 - Worst Year:: In 2008, the market experienced a sharp decline of -48%.
 - Cumulative Growth:: Over the last 30 years, the NIFTY50's cumulative growth exceeded 3940%.

### 1.3 Technology Milestones and NIFTY50:

**Question:** How did the majot technological milestones such as rise of internet, smartphones, AI affected NIFTY50?

 Code Snippet:
 
 ```python
 # Defining major technological milestones

milestones = [
     (1999, 'Rise of the Internet', 'blue'),
     (2007,'iphone launch', 'black'),
     (2010, 'Smartphone Revolution', 'green'),
     (2020,'Upi Boom','orange'),
     (2021, 'Digital Transformation', 'brown'),
     (2023, 'Rise of AI', 'purple')
             
]


# Plotting technological milestones on the S&P 500 graph
for year, event, color in milestones:
    if year in nifty50_df['Date'].dt.year:
        price = nifty50_df.loc[nifty50_df['Date'].dt.year == year, 'Close'].values[0]
        plt.annotate(event, (mdates.date2num(pd.Timestamp(f'{year}-01-01')), price), xytext=(10, 10), 
                     textcoords='offset points', ha='left', va='bottom',
                     bbox=dict(boxstyle='round,pad=0.5', fc='yellow', alpha=0.5),
                     arrowprops=dict(arrowstyle='->', connectionstyle='arc3,rad=0', color=color),
                     fontsize=10, color=color)
```

**Visualization:**

![Nifty50 Performance and Major Technological Milestones (Last 30 Years)](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/Nifty50%20Performance%20and%20Major%20Technological%20Milestones%20(Last%2030%20Years).png)

**Insights:**

   - The introduction of the Rise of the Internet (1999) and Smartphone Revolution (2010) marked the beginning of significant market shifts.
   - The Upi Boom (2020) and Rise of AI (2023) caused even more rapid growth, particularly after 2016.  






