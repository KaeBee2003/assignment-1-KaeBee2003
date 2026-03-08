
# 📌 **Formulating the Hypothesis**

### I hypothesize that:

1. **Higher popularity leads to more vote counts.**
   As a movie becomes more popular, it garners more public attention and social media presence, which in turn encourages more people to watch and rate it—thereby increasing the vote count.

2. **Higher budgets result in higher revenue and greater popularity.**
   Larger budgets often enable better production quality, wider distribution, and larger marketing efforts, which are expected to contribute to box office success and public interest.

3. **Movies with larger casts and longer runtimes tend to receive better audience ratings.**
   A larger cast and extended runtime may indicate more complex stories and broader appeal, potentially leading to better audience reception.

---

# 🧹 **Data Preprocessing**

### ✅ Merging Datasets

The `movies` and `credits` datasets were merged using an **inner join** on the primary keys `id` (from movies) and `movie_id` (from credits). The result was a unified dataset with **4803 rows and 24 columns**.

### ✅ Genre Processing

* The `genres` column was originally in JSON format.
* Extracted the **primary**, **secondary**, and **tertiary** genres for each movie to simplify analysis.

### ✅ Release Year Extraction

* Only the **year** was extracted from the release date, as daily granularity isn’t relevant for this study.

### ✅ Cast Information

* The `cast` column contained a list of actors in JSON format.
* Extracted the **top lead actors** and the **total number of cast members** for each film.

### ✅ Column Cleanup

* Removed duplicate columns (e.g., duplicate `id` columns post-merge).
* Dropped irrelevant columns like `homepage` and `overview`.

### ✅ Country & Language Processing

* From the `production_countries` and `spoken_languages` columns (both JSON), extracted the **primary country/language** and **count** of countries/languages per film.

### ✅ Filtering Unreleased Movies

* Removed movies without a release date as they don’t contain post-release data like revenue.

### ✅ Handling Nulls

* **Dropped rows** with missing or zero values in crucial fields such as `budget` and `revenue`. These attributes are essential for analysis and can't be imputed reliably.

### ✅ Crew Information

* From the `crew` column (JSON), extracted the **director**—a key individual influencing a film’s style and reception.

---

# 📊 **Data Visualization**

### 1. **Distribution of Success**

* A pairwise scatter plot revealed a strong **positive correlation** between **budget** and **revenue**, validating one of the hypothesized relationships.
* However, **budget vs. ratings** showed **weak correlation**, suggesting that higher spending doesn’t necessarily result in better audience reception.

### 2. **Time-Series Analysis**

* A line plot shows a significant increase in movie production **post-2000**, likely due to global industry growth and digital distribution platforms.
* **Action** consistently ranks as the top genre, followed by **adventure** and **drama**—a trend that has remained stable over decades.

### 3. **Revenue & Ratings Breakdown**

* A violin plot displayed the **ratings distribution** of films from the top 5 most prolific directors.

  * **Martin Scorsese** stands out with **no movie rating below 6**.
  * **Steven Spielberg** achieved the **highest individual ratings**, albeit inconsistently.
* Among genres, **Animation** surprisingly leads in **profitability**, likely due to low production costs and wide appeal to children and families.

### 4. **Highly Correlated Attributes (Pearson Correlation)**

Here are the top correlated attribute pairs:

| Attribute Pair           | Correlation Coefficient |
| ------------------------ | ----------------------- |
| Vote Count vs Revenue    | **0.7562**              |
| Vote Count vs Popularity | **0.7490**              |
| Budget vs Revenue        | **0.7054**              |
| Popularity vs Revenue    | **0.6022**              |
| Vote Count vs Budget     | **0.5401**              |

> ⚠️ However, scatter plots indicate **heteroscedasticity**, so these correlations should be interpreted with caution.

### 5. **Audience Ratings vs Runtime vs Cast Count**

A bubble chart was created where:

* X-axis: **Runtime**
* Y-axis: **Vote Average**
* Bubble size: **Cast Count**

Observations:

* Higher-rated and longer films often had more cast members.
* However, the overlap with smaller bubbles suggests the relationship is not strong or consistent.

---

# 🧪 **Hypothesis Testing**

### ✅ Hypothesis 1: *More Popular the movie, more people hype the movie, which increases vote count.*

* Supported by **strong correlation (0.749)** between **vote count and popularity**.
* But due to **heteroscedasticity**, the result is **partially valid**.

### ❌ Hypothesis 2: *Higher budgets lead to higher revenues and greater popularity.*

* **Budget and revenue** are **strongly correlated (0.7054)**.
* However, **budget and popularity** show **weak correlation**, and the data is **heteroscedastic**.
* Therefore, this hypothesis is **not valid**.

### ✅ Hypothesis 3: *Movies with larger casts and longer runtimes get better ratings.*

* Bubble plot shows **some correlation** between runtime, cast count, and higher ratings.
* Yet, due to significant overlap with lower cast/runtimes, this hypothesis is also **partially valid**.

---

# ✅ Summary

* **Correlation exists** between vote count, revenue, and popularity, but the data's **heteroscedastic nature** limits strong conclusions.
* **Budget alone doesn’t guarantee popularity or higher ratings.**
* **Larger casts and longer runtimes** might contribute to better audience ratings, but the effect is not consistent.

> This README summarizes the key preprocessing and analytical steps. Additional code and visualizations can be found in the accompanying `.ipynb` notebook.

---

