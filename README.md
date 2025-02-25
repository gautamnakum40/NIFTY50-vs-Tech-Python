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

## Exploratory Data Analysis (EDA)
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

 **Code Snippet:**
 
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
   - The Digital Transformation (2021) and Rise of AI (2023) caused even more rapid growth, particularly after 2016.  

### 2. Impact of Technological Advancements on NIFTY50

[Notebook link](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/2.%20Impact%20of%20Technology.ipynb)

### 2.1 Technology Sector Outperformance

**Question**: How has the technology sector outperformed the NIFTY50? 

**Code Snippet:**

```python
# first we need to fetch data from csv file.
it_df = pd.read_csv("Nifty IT Historical Data.csv")

# Nifty 50 data from 2003-09-01 for comparison with Nifty IT index.
df = pd.read_csv('nifty_data.csv')

# for normilization divide the closing value with the starting close value of the index as it helps to compare percentage change of the closing price of both index over time.
nifty_df['Normalized_Close'] = nifty_df['Close'] / nifty_df['Close'].iloc[0]
it_df['Normalized_Close'] = it_df['Close'] / it_df['Close'].iloc[0]

# now we can graph the comparison
plt.figure(figsize=(12, 7))
sns.lineplot(data=nifty_df, x='Date', y='Normalized_Close', label='Nifty 50', color='royalblue')
sns.lineplot(data=it_df, x='Date', y='Normalized_Close', label='Nifty IT', color='darkorange')

plt.title('Nifty50 vs Nifty IT Sector Performance (Last 25 Years)', fontsize=16, fontweight='bold')
plt.xlabel('Year', fontsize=12)
plt.ylabel('Normalized Price', fontsize=12)

plt.legend(fontsize=10)

plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```
**Visualization:**

![Nifty50 vs Nifty IT Sector Performance (Last 25 Years)](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/Nifty50%20vs%20Nifty%20IT%20Sector%20Performance.png)

**Insights:**

  - From the graph we can clerly see that technology sector has dramatically outperformed Nifty50 especially since 2017-2018 which would be the start of the Rise of Digital Transformations and AI in Country.
    
### 2.2 IT BIG Stocks vs NIFTY50

**Question:** What is the impact of FAANG stocks on the market? 

**Code Snippet:**

```python 
import yfinance as yf # for fetch data from yahoo finance.

# created a fn to fetch data
def fetch_data(ticker, start_date, end_date):
    return yf.download(ticker, start=start_date, end=end_date)['Close']

# Set date range(Available Max data on yfinance )
start_date = '2007-10-01'
end_date = '2025-01-23'

# list of tech companies and their tickers
tech_companies = {
'TCS' : 'TCS.NS',
'Infosys' : 'INFY.NS',
'HCLTech' : 'HCLTECH.NS' ,
'Wipro' : 'WIPRO.NS',
'Tech Mahindra' : 'TECHM.NS'
}

# Download data
tiwht = pd.DataFrame()
for company, ticker in tech_companies.items():
    tiwht[company] = fetch_data(ticker, start_date, end_date)
tiwht['NIFTY50'] = fetch_data('^NSEI', start_date, end_date)    
  
# Calculate cumulative returns- because there are different satrt date for different companies so this is prefered for normalization
cumulative_returns = (1 + tiwht.pct_change()).cumprod()
```
**Visualization:**

![NIFTY50 vs IT Big Stocks Cumulative Return](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/NIFTY50%20vs%20IT%20Big%20Stocks%20Cumulative%20Returns.png)

**Insights:**

   - IT BIG Stocks have significantly outpaced the NIFTY50 in terms of cumulative returns.

### 3. Volatility Analysis of Tech Stocks:

[Notebook link](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/3.%20Volatility%20Analysis.ipynb)

**Question:** How volatile are tech stocks compared to the NIFTY50 ?

**Code Snippet:**

```python 
# Calculating daily returns
returns = tiwht.pct_change().dropna()

# Defining rolling window size (1 year = 252 trading days)
rolling_window = 252

# Calculating rolling volatility (annualized) for each company and nifty 50
rolling_volatility = returns.rolling(window=rolling_window).std() * np.sqrt(252)
```

**Visualization:**

![Distribution of Daily Returns: Tech Giants vs NIFTY50](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/Distribution%20of%20Daily%20Returns%20Tech%20Giants%20vs%20NIFTY50.png)

![Rolling Annualized Volatility (1-year Window)](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/Rolling%20Annualized%20Volatility%20(1-year%20Window).png)

**Insights:**

TCS & Tech Mahindra shows the widest spread, suggesting it has the highest volatility among the listed stocks. other tech companies are also more volitily as compared to NIFTY50 which is more smaller box and more closely spread.

### 4. AI Revolution and Nvidia’s Performance:

[Notebook link](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/4.%20AI%20Revolution%20and%20Its%20Impact.ipynb)

**Question:** How has the AI revolution affected TCS’s Stock ?

**Code Snippet:**

```pyhon
# Download TCS stock data from Yahoo Finance
tcs = yf.Ticker('TCS.NS')
tcs_data = tcs.history(start='2011-01-01')

# AI-related breakthrough dates
ai_breakthroughs = [    
    ('2012-10-01', 'Ignio AI Platform Introduced', 'orange'),
    ('2019-03-01', 'Machine First Delivery Model (MFDM) Unveiled', 'purple'),
    ('2020-09-01', 'TCS AI Cloud Partnership with Microsoft', 'green'),
    ('2023-07-01', 'TCS Expands AI-Driven Consulting with Google Cloud', 'yellow'),
    ('2024-01-01', 'TCS AI Lab Established for Generative AI Solutions', 'cyan')
]

# Ploting TCS stock price
plt.figure(figsize=(14, 7))
plt.plot(tcs_data.index, tcs_data['Close'], label='TCS Stock Price')

# Annotate AI breakthroughs

for date, event, c in ai_breakthroughs:
    plt.axvline(pd.to_datetime(date), color=c, linestyle='--', label=event)
    

plt.title('TCS Stock Performance with Key AI Breakthroughs')
plt.xlabel('Year')
plt.ylabel('Stock Price(INR)')
plt.grid(True)
plt.legend()
plt.show()
```

**Visualization:**

![TCS Stocks Performance](https://github.com/gautamnakum40/Python_NIFTY50vsTECH_Analysis/blob/master/Plots/TCS%20Stock%20Performance%20with%20Key%20AI%20Breakthroughs.png)

**Insights:** 
     - TCS's stock saw rapid growth following MFDM (2019) and TCS Expands AI Driven Consulting with Google Cloud (2023), highlighting its leading role in indian AI.

### Summary and Recommendations:

This analysis examines the influence of technological advancements on the NIFTY50 over the past 30 years, with a particular focus on the tech sector and companies like TCS. Below is the summary of the key findings, along with suggested actions:

#### NIFTY50 Long-Term Trends:

**Finidngs:** Over the past five decades, the NIFTY50 has shown steady growth, with cumulative gains surpassing 4000%. Significant drops occurred during the Dot-com Bubble (2000) and the 2008 Financial Crisis, but the index rebounded each time.

**Recommendation:** Long-term investors should remain invested through market downturns, as historical data indicates that markets recover and continue upward over time.

#### Technology Sector Outperformance

**Finidngs:** The technology sector, particularly through the XLK ETF, has outperformed the broader S&P 500 since 2016, driven by advancements in AI. FAANG stocks, in particular, have delivered significantly higher cumulative returns.

**Recommendation:** Consider allocating a portion of your investment portfolio to tech-focused ETFs or individual FAANG stocks, especially during periods of technological innovation, to capture potential superior long-term returns.

**Volatility in Tech Stocks**

**Findings:** Tech stocks, notably TCS, have exhibited greater volatility than the NIFTY50, with TCS experiencing annualized volatility of more than 50% during periods of AI-related advancements.

**Recommendation:** While Tech stocks offer higher growth potential, they also carry more risk. Investors should diversify their portfolios or use risk management techniques like stop-loss orders to manage potential Volatility.

**AI Revolution:**

**Finidngs:** TCS’s stock experienced substantial growth following major AI milestones, such as the MFDM (2019) and TCS Expands AI Driven Consulting with Google Cloud (2023), highlighting its leading role in indian AI., resulting in over a 300% increase in stock value from 2016 to 2023.

**Recommendation:** Investors seeking to capitalize on the AI revolution should focus on companies at the forefront of AI development, such as TCS. Given the volatility, it's important to carefully time entry and exit strategies to mitigate risks.













