<h1>🧠 Stroke Prediction and Analysis</h1>

<blockquote>
  <strong>Leveraging Structured + Unstructured Data for Predictive Modeling in Healthcare</strong>
</blockquote>

<h2>📌 Overview</h2>

<p>Strokes are one of the leading causes of death and disability globally. This project applies machine learning techniques to predict stroke mortality rates by combining structured epidemiological data with unstructured news content. Our goal is to identify key risk factors and improve early detection strategies, ultimately reducing healthcare burdens.</p>

<hr />

<h2>📊 Data Sources</h2>

<h3>🗃️ Structured Data</h3>
<ul>
  <li><strong>Source:</strong> CDC Heart and Stroke Data (2000–2019)</li>
  <li><strong>Description:</strong> County-level stroke and heart disease death rates per 100,000 people</li>
  <li><strong>Features:</strong>
    <ul>
      <li>Time Periods: 2000–2010 and 2010–2019</li>
      <li>Demographics: Age groups (35–64, 65+), race/ethnicity, and gender</li>
    </ul>
  </li>
</ul>

<h3>📰 Unstructured Data</h3>
<ul>
  <li><strong>Source:</strong> <a href="https://developer.nytimes.com/">New York Times API</a></li>
  <li><strong>Articles Collected:</strong> 5,100+ articles (2010–2019)</li>
  <li><strong>Search Terms:</strong> "stroke", "health", "people"</li>
  <li><strong>Article Fields:</strong>
    <ul>
      <li>Abstracts and lead paragraphs</li>
      <li>Word count, state, publication year</li>
      <li>Hit count (relevance/popularity)</li>
    </ul>
  </li>
</ul>

<hr />

<h2>⚙️ Methodology</h2>

<h3>🧼 Data Preprocessing</h3>
<ul>
  <li><strong>Structured Data:</strong> Cleaned using PySpark and Pandas (NA removal, filtering, transformation)</li>
  <li><strong>Unstructured Data:</strong>
    <ul>
      <li>Sentiment analysis using <code>NLTK</code> and <code>VADER</code></li>
      <li>FastText for word embeddings</li>
      <li>Feature extraction: average sentiment & embedding scores</li>
    </ul>
  </li>
</ul>

<h3>🧠 Machine Learning Models</h3>
<p>All models used <code>VectorAssembler</code>, <code>StringIndexer</code>, and <code>OneHotEncoder</code> for preprocessing:</p>

<ul>
  <li><strong>Linear Regression</strong>
    <ul>
      <li>RMSE: 36.9 | R²: 0.93</li>
      <li>Advantages: Interpretable, efficient</li>
      <li>Limitations: Assumes linearity, sensitive to outliers</li>
    </ul>
  </li>
  <li><strong>Random Forest Regression</strong>
    <ul>
      <li>RMSE: 39.5 | R²: 0.92</li>
      <li>Advantages: Captures non-linear relationships</li>
      <li>Limitations: Less interpretable</li>
    </ul>
  </li>
  <li><strong>Gradient Boosted Tree (GBT) Regression</strong>
    <ul>
      <li>RMSE: 33.6 | R²: 0.94</li>
      <li>Advantages: High accuracy, feature importance</li>
      <li>Limitations: Slower training, harder to interpret</li>
    </ul>
  </li>
</ul>

<hr />

<h2>💡 Key Findings</h2>

<ul>
  <li><strong>Top Predictors:</strong> Age, race, year, state, and sentiment scores from media coverage</li>
  <li><strong>Model Performance:</strong> GBT Regression yielded the best results overall</li>
  <li><strong>Insight:</strong> Unstructured text data (e.g., sentiment) provides additional predictive value</li>
</ul>

<hr />

<h2>🧪 Challenges</h2>

<ul>
  <li>Some web-scraped articles were not directly healthcare-related</li>
  <li>Short-form or visual-only articles limited NLP usefulness</li>
  <li>Interpretability vs. performance trade-offs in model selection</li>
</ul>

<hr />

<h2>🚀 Future Work</h2>

<ul>
  <li>Expand to other health outcomes (e.g., heart attacks, diabetes)</li>
  <li>Incorporate geospatial and socio-economic data</li>
  <li>Improve article relevance filtering and topic modeling</li>
  <li>Deploy a predictive dashboard for public health agencies</li>
</ul>



