<!-- README.md for Stroke Prediction and Analysis -->

<h1 align="center">🧠 Stroke Prediction and Analysis</h1>

<p align="center">
  A machine learning and NLP pipeline for predicting stroke mortality rates in the U.S. by combining structured epidemiological data and unstructured news article sentiment.
</p>

<hr />

<h2>📌 Executive Summary</h2>
<p>
Strokes are a leading cause of disability and death globally, making prediction and prevention critical. This project aims to develop robust machine learning models for stroke incidence prediction using structured data from the CDC and unstructured article data from the New York Times. The goal is to uncover critical risk factors and provide insights for early detection and intervention. The project combines demographic, behavioral, and clinical data with NLP sentiment analysis and FastText word embeddings to enrich predictive performance.
</p>

<p>
Structured data includes county-level stroke death rates from the CDC Heart and Stroke Data, spanning 2000–2019. It is broken down by age (35–64, 65+), race/ethnicity, and gender. Unstructured data includes over 5.1K articles retrieved via the NYT API, searched by keywords like "stroke", "health", and "people". Data includes abstracts, lead paragraphs, word counts, publication years, states, and popularity hits.
</p>

<p>
Data preprocessing involved cleaning nulls and irrelevant columns, renaming for clarity, and filtering values. Sentiment analysis was done using VADER (NLTK), scoring negative and compound sentiments. FastText embeddings were generated and averaged for each article. Features were engineered using Spark's StringIndexer, OneHotEncoder, and VectorAssembler, and then modeled using Linear Regression, Random Forest, and Gradient Boosting Trees.
</p>

<hr />

<h2>📊 Data Sources</h2>
<ul>
  <li><strong>CDC Stroke Mortality Dataset:</strong> <a href="https://data.cdc.gov/Heart-Disease-Stroke-Prevention/Rates-and-Trends-in-Heart-Disease-and-Stroke-Morta/7b9s-s8ck/about_data" target="_blank">CDC Data</a></li>
  <li><strong>New York Times Articles:</strong> Retrieved via the NYT API, stored in MongoDB (temporary) and Databricks (final).</li>
</ul>

<hr />

<h2>📑 Reproduction Guide</h2>
<ol>
  <li>
    Download structured data from the <a href="https://data.cdc.gov/Heart-Disease-Stroke-Prevention/Rates-and-Trends-in-Heart-Disease-and-Stroke-Morta/7b9s-s8ck" target="_blank">CDC website</a>.
    <ul>
      <li>Filter for "Stroke" and years 2010–2019 (exclude "2010-2019").</li>
      <li>Export the data and upload to Databricks.</li>
    </ul>
  </li>
  <li>
    Run <code>stroke articles.ipynb</code> to scrape articles using 3 NYT API keys to avoid rate limits.
    <ul>
      <li>Run times vary (~6 hours), but MongoDB ensures persistence.</li>
    </ul>
  </li>
  <li>Export selected fields from MongoDB to CSV and upload to Databricks.</li>
  <li>Run <code>stroke.ipynb</code> for full processing, sentiment scoring, embeddings, and model training.</li>
  <li>Use <code>stroke_visuals.Rmd</code> in RStudio for visualizations.</li>
</ol>

<hr />

<h2>🛠️ Technologies Used</h2>
<ul>
  <li>Databricks (PySpark, Pandas)</li>
  <li>NLTK (VADER Sentiment)</li>
  <li>Gensim FastText</li>
  <li>MongoDB</li>
  <li>RStudio (visualizations)</li>
</ul>

<hr />

<h2>🧪 Modeling Overview</h2>
<p>
We trained three regression models to predict stroke mortality rates: Linear Regression (LR), Random Forest (RF), and Gradient Boosted Trees (GBT). The models were trained using demographic, behavioral, NLP, and text embedding features. Data was preprocessed using PySpark ML's StringIndexer, OneHotEncoder, and VectorAssembler.
</p>

<h3>📈 Performance</h3>
<table>
  <tr><th>Model</th><th>RMSE</th><th>R²</th></tr>
  <tr><td>Linear Regression</td><td>36.91</td><td>0.93</td></tr>
  <tr><td>Random Forest</td><td>39.53</td><td>0.92</td></tr>
  <tr><td>Gradient Boosting Trees</td><td><strong>33.58</strong></td><td><strong>0.94</strong></td></tr>
</table>

<h3>📊 Key Feature Insights (GBT)</h3>
<ul>
  <li><strong>Age 35–64</strong>: Most predictive feature</li>
  <li><strong>Year</strong>: Strong trend over time</li>
  <li><strong>Race</strong>: Black and Hispanic indicators are significant</li>
  <li><strong>average_embedding</strong>: Captures media narrative context</li>
  <li><strong>Sentiment</strong>: Negative and compound sentiment scores in lead and abstract contribute predictive value</li>
</ul>

<hr />

<h2>⚠️ Limitations</h2>
<ul>
  <li>Some scraped articles may not relate directly to stroke or healthcare.</li>
  <li>Short or image-heavy articles limit NLP processing.</li>
</ul>

<hr />

<h2>🚀 Conclusion & Future Work</h2>
<p>
The Gradient Boosted Tree model demonstrated the best performance with an RMSE of 33.6 and R² of 0.94. It captured complex interactions between features, particularly media sentiment and demographic attributes. Future directions include filtering irrelevant articles more effectively, exploring deeper embeddings or LLM-based models, and scaling the framework to near real-time prediction.
</p>
<p>
We believe that data-driven analytics like this can transform stroke prevention and policy planning by enabling early intervention, improving outcomes, and reducing strain on healthcare systems.
</p>

