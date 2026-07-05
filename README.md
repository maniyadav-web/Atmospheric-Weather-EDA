☆☆ **Global Weather Repository** ☆☆

▷ **What this project does**
An exploratory data analysis of the [Global Weather Repository](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) dataset from Kaggle — 145,785 rows across 41 columns covering weather, atmospheric, and air-quality readings for locations worldwide.

▷ **Pipeline:**

**1. Load & Inspect** — Read the CSV, checked shape, dtypes, and summary statistics (`.info()`, `.describe()`, `.isnull().sum()`).

**2. Clean**
- Removed duplicate rows.
- Filled missing numeric values with the column median and missing categorical values with the column mode — scoped only to columns that actually had gaps, with identifying columns (`country`, `location_name`) flagged rather than auto-filled to avoid distorting the geography.
- Converted `last_updated` to a proper datetime type.
- Verified zero remaining nulls after cleaning.

**3. Explore & Visualize**
- Bar chart: top 10 countries by maximum recorded temperature.
- Histogram: global distribution of wind speed (kph).
- Scatter plots: humidity vs. precipitation, and UV index vs. visibility.
- Correlation heatmap across 13 meteorological and air-quality features.
- Boxplots for outlier detection across temperature, humidity, wind, UV index, and pressure.

**4. Geospatial visualization**
- An interactive Folium map with color-coded markers (blue/green/orange/red by temperature band) for every location's latest reading.
- A Plotly choropleth showing average temperature by country, based on each location's most recent reading.

▷ **Key findings:**

- **Temperature vs. feels-like temperature are near-perfectly correlated** (r ≈ 0.98), as expected physically.
- **Humidity is negatively correlated with UV index** (r ≈ -0.55) and moderately positively correlated with cloud cover (r ≈ 0.51) — consistent with cloudier, more humid conditions blocking UV.
- **Air pollutants cluster together**: carbon monoxide, nitrogen dioxide, and sulphur dioxide show moderate positive correlation with each other (r ≈ 0.3–0.6), suggesting shared sources (e.g., traffic/industrial activity) rather than independent phenomena.
- **The hottest-recorded-temperature ranking is dominated by Gulf and equatorial nations** (Kuwait, Iraq, UAE, Qatar, Saudi Arabia, Djibouti, Chad), which lines up with known climate patterns — except for one outlier (see below).

▷ **Data quality caveats:**
A few sentinel/erroneous values survived cleaning because they aren't technically `NaN`:
- `air_quality_Carbon_Monoxide` and `air_quality_Sulphur_dioxide` contain **-9999 placeholder values** mixed into otherwise valid readings.
- `air_quality_PM10` has a **minimum of -1848**, which is physically impossible for a particulate concentration.
- `wind_kph` has a max of **2963 kph** — far beyond any recorded wind speed on Earth, almost certainly a sensor/unit error.
- The top-temperature chart lists **Fiji Islands at ~79°C**, which is not physically plausible for that climate and is likely a data artifact rather than a real reading.

These don't invalidate the overall trends (correlations and typical ranges look sound), but a rigorous next step would be to filter or cap these sentinel/out-of-range values before drawing quantitative conclusions from extremes.

▷ **Tools used**
 ⇒ Python Libraries Used (The Tech Stack)
  These are the specialized data science packages we imported into your code cells:
  - pandas: Used for data manipulation, cleaning duplicate rows, and handling missing numbers or text using statistical median/mode imputation.
  - matplotlib.pyplot: The foundational plotting library used to construct our figure windows and multi-plot layout grids.
  - seaborn: Built on top of matplotlib, this was used to render the polished statistical visuals (the bar chart, histogram, scatter plots,
             correlation heatmap, and boxplots).
  - folium: A powerful geospatial library used to generate the interactive JavaScript world map and handle location marker clustering.
  - plotly.express: Used to build the high-quality interactive Choropleth map that shades whole countries based on regional climate data averages.

 ⇒ Applications & Environments Used
  These are the software tools you physically used on your Mac to write, run, and host the analysis:
  - Visual Studio Code (VS Code): Your primary Integrated Development Environment (IDE) where you wrote your code blocks and markdown.
  - Jupyter Notebook Extension: The interactive computational environment running inside VS Code that allowed you to execute your code cells               individually and view charts instantly.
  - Git / Mac Terminal: The command-line interface tools used to track your file versions and push your progress directly to the cloud.
  - GitHub: The cloud platform where your code repository is hosted publicly for reviewers and teams to look over.
  - Web Browser (Chrome/Safari): Used to launch, test, and interactively click through your compiled .html geospatial map files.
