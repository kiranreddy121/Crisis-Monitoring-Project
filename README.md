# Crisis-Monitoring-Project

The goal is to build a lightweight yet powerful pipeline to extract, analyze, and map crisis-related discussions from Reddit using Natural Language Processing (NLP).

---

##  Objectives

-  Extract Reddit posts related to mental health, substance use, or suicidality.
-  Analyze sentiment and detect high-risk phrases using NLP and clustering.
-  Visualize crisis-prone regions using geolocation and interactive heatmaps.

---

##  Project Structure

### Task 1: Social Media Data Extraction & Preprocessing
- Extracted 500+ posts from subreddits: `r/mentalhealth`, `r/SuicideWatch`, `r/depression`, `r/addiction`, and `r/offmychest`.
- Filtered posts using crisis-related keywords like “suicidal”, “help me”, “feeling empty”.
- Cleaned raw text by removing emojis, URLs, punctuation, and stopwords using `emoji`, `re`, and `nltk`.

 **Why?**  
Initial attempts with raw text led to messy downstream results. Preprocessing significantly improved classification accuracy.

---

### Task 2: Sentiment & Crisis Risk Classification
- Applied **TextBlob** to classify sentiment (Positive / Neutral / Negative).
- Used **TF-IDF vectorization** with crisis-related phrases to detect textual signals of distress.
- Enhanced with **KMeans clustering** to separate posts by semantic similarity to crisis terms.
- Risk Levels:
  -  **High Risk**: “I want to end it all”
  -  **Moderate Concern**: “I feel lost lately”
  -  **Low Concern**: General mental health conversations

 **Why?**  
Rule-based filtering missed semantic variations. TF-IDF + KMeans improved sensitivity and allowed for unsupervised discovery of patterns.

---

### Task 3: Geolocation & Crisis Mapping
- Extracted location mentions using **spaCy** (`GPE`, `LOC`) and **GeoText**.
- Validated true city/country names using **geopy's Nominatim**.
- Removed false positives (e.g., “Most”, “Same”) by checking if the name maps to a real-world place.
- Visualized top 5 mentioned locations using **Folium**:
  - Added **heatmap intensity** based on number of posts
  - Used labeled markers for clarity
  - Inline display in Google Colab supported via `/files/` iframe

 **Why?**  
Raw NLP models often misidentify common words as places. Cross-checking with real maps solved this.

---

##  Output Files

| File | Description |
|------|-------------|
| `reddit_crisis_posts.csv` | Scraped and cleaned Reddit posts |
| `reddit_crisis_labeled_combined.csv` | Sentiment + risk labels for each post |
| `top_5_clean_locations.csv` | Most mentioned real-world crisis locations |
| `crisis_heatmap.html` | Interactive heatmap + markers for distress regions |

---

## Requirements

```bash
pip install praw pandas emoji nltk textblob spacy sklearn geotext folium geopy matplotlib
python -m spacy download en_core_web_sm
