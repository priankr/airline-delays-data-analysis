# U.S. Airline Delays Analysis (2003-2016)

An in-depth analysis of 13 years of flight delay data from major U.S. airports, revealing patterns in airline performance, seasonal trends, delay causes, and airport-specific performance.

## Interactive Dashboard

**[View the live interactive dashboard](https://priankr.github.io/airline-delays-data-analysis/)**

Explore the data through interactive visualizations showing trends over time, seasonality heatmaps, delay cause breakdowns, and airport performance comparisons.

## Key Findings

### Overall Performance
- **77.8%** of flights departed on time (2003-2016 average)
- **20.2%** were delayed
- **~2%** were cancelled or diverted

### The Industry Improved Dramatically
- **Worst year**: 2007-2008 (only 75% on-time during the financial crisis)
- **Best year**: 2013 (85% on-time)
- **10+ percentage point improvement** from 2007 to 2013 that held through 2016

### Seasonality Matters
- **Best month to fly**: September (consistently lowest delays)
- **Worst month**: December (holiday crowds + winter weather)
- Pattern is remarkably consistent across all 14 years

### Delay Causes (by frequency)
1. **National Aviation System (NAS)**: 38.2% - Air traffic control, airport congestion
2. **Late Aircraft**: 32.8% - Cascading delays from previous flights
3. **Carrier**: 21.6% - Airline maintenance, crew issues
4. **Weather**: 7.2% - Actual meteorological conditions
5. **Security**: 0.2% - Terminal evacuations, security breaches

### Airport Performance Gap
- **Best airports**: 84-85% on-time (Phoenix, Salt Lake City, San Diego)
- **Worst airports**: 72-73% on-time (Newark, JFK, LaGuardia)
- **12-15 percentage point difference** between best and worst

## Repository Contents

### Analysis Files
- **`airline-delays-data-analysis.ipynb`** - Comprehensive Python analysis with visualizations, statistical modeling, and detailed insights
- **`airport_delays.Rmd`** - Original R Markdown analysis (2021)
- **`ANALYSIS_IMPROVEMENT_SUGGESTIONS.md`** - Detailed recommendations for enhancing the analysis

### Data
- **`airlines.csv`** - 2MB dataset with monthly statistics from 30-50+ major U.S. airports (June 2003 - December 2016)

### Web Dashboard
- **`docs/index.html`** - Interactive GitHub Pages dashboard with Chart.js visualizations

## Dataset Details

**Source**: Bureau of Transportation Statistics via [CORGIS Dataset Project](https://think.cs.vt.edu/corgis/csv/airlines/)

**Coverage**:
- Time period: June 2003 - December 2016 (162 months)
- Airports: 30-50+ major U.S. airports per year
- Structure: One record per airport per month

**Key Metrics**:
- Flight counts (on-time, delayed, cancelled, diverted, total)
- Delay causes (5 types with counts and total minutes)
- Carrier information (names and count per airport)

## Tools & Technologies

- **Python** - pandas, NumPy, scikit-learn, matplotlib, seaborn
- **Jupyter Notebook** - Interactive analysis and documentation
- **Chart.js** - Interactive web visualizations
- **GitHub Pages** - Dashboard hosting
- **R** (legacy) - Original 2021 analysis

## Key Insights by Audience

### For Travelers
- Book flights in September for lowest delay risk
- Avoid December if possible (holiday peak)
- Choose connections through top-performing airports (PHX, SLC, SAN)
- West Coast and Southwest airports generally more reliable

### For Airlines
- Late Aircraft delays create longest passenger disruptions (cascading effect)
- Schedule padding and spare aircraft can break delay cascades
- Carrier-controlled delays have improved over time (modernization works)
- Best airports achieve 10-15 points better performance than average

### For Policymakers
- NAS delays (40% of all delays) indicate infrastructure underinvestment
- Air traffic control modernization could address nearly half of all delays
- 10-point improvement from 2007 to 2013 proves system can improve
- Airport quality affects economic competitiveness

## Viewing the Analysis

### Option 1: Interactive Dashboard (Recommended)
Visit the [live dashboard](https://priankr.github.io/airline-delays-data-analysis/) for an interactive experience with charts you can explore.

### Option 2: Jupyter Notebook
```bash
jupyter notebook airline-delays-data-analysis.ipynb
```

### Option 3: Local Dashboard
Open `docs/index.html` in any modern web browser.

## Analysis Highlights

The Python notebook includes:
- Weighted metrics accounting for airport size
- Frequency vs. severity analysis
- Airport-level performance profiles
- Time-series trend analysis with seasonality
- Delay cause composition over time
- Predictive modeling with ElasticNet and HistGradientBoosting
- Comprehensive visualizations and statistical insights

## License & Attribution

Data provided by the Bureau of Transportation Statistics. Analysis and visualizations created for educational and informational purposes.

---

**Questions or suggestions?** Open an issue or submit a pull request.
