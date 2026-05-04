# Project Brief: The "Sugar Trap" Market Gap Analysis

**Client:** Helix CPG Partners (Strategic Food & Beverage Consultancy)  
**Deliverable:** Interactive Dashboard, Code Notebook & Insight Presentation

---

## A. The Executive Summary
* I analysed a randomised sample of 200,000 records from the Open Food Facts dataset to find a Blue Ocean for Helix CPG Partners. Most traditional snacks have 30% of their weight as pure sugar. My analysis shows that Plant-based snacks are the most efficient category for delivering high protein with low sugar. However, my ingredient mining found that these current products rely heavily on salt and wheat as fillers. The biggest opportunity is to create a high-protein, low-sugar plant-based snack targeting people who would take in little sodium.

## B. Project Links
* **Code Notebook:** [GitHub](https://github.com/blip-cmd/The-Market-Gap-Analysis/blob/main/notebook_v2.ipynb) 
* **Interactive Dashboard:** [Data Studio](https://datastudio.google.com/reporting/34881442-2f4f-48c8-a6eb-f5186f5a4d28)
* **Presentation:** [Live Strategy](https://the-market-gap-analysis.vercel.app/) 
* **Executive Summary Video:** [YouTube-pending](https://youtu.be/)



## C. Technical Explanation
* **Memory-Efficient Data Engineering**: To ingest the massive **12GB dataset** within local RAM constraints, I implemented a **chunked streaming architecture**. By utilizing the `chunksize` parameter in Pandas, I processed the first 500,000 rows in batches of 50,000, immediately downcasting nutritional columns to `float32` to optimize memory overhead. I then performed a **randomized shuffle** to extract a representative **200,000-row sample**, ensuring a **99% statistical confidence interval** for the subsequent market analysis[cite: 2, 3].
* **Data Validation & Schema Alignment**: I enforced strict **biological boundary constraints**, filtering for records where sugars and proteins fell within a realistic $0-100g$ range per 100g. Any records with missing product names or null nutritional values were purged rather than imputed; in a **CPG Market Gap Analysis**, imputing "fake" nutrition data would introduce unacceptable bias into the strategic findings. To ensure high-fidelity mapping, I cross-referenced the raw schema with official field guides before categorizing the data into five high-level **business buckets**: Snacks, Beverages, Dairy, Plant-based, and Cereals. This keyword-matching approach on `categories_tags` allowed me to eliminate "market noise"—such as pet food or raw commodities—and isolate the competitive landscape relevant to the client.
* **Feature Engineering & Natural Language Processing (NLP)**: I engineered two primary features to drive executive decision-making:
    *   **Nutrient Density Score**: Calculated as $\frac{Proteins}{(Sugars + 1)}$, this metric quantifies "nutritional value for money" by identifying which categories deliver the highest protein payload per gram of sugar overhead[cite: 2, 3].
    *   **Unstructured Ingredient Mining**: I developed a flexible NLP function using **Regular Expressions (Regex)** to parse the `ingredients_text` field. By ranking recurring terms naturally, the analysis revealed a critical **Strategic Discovery**: **78.0% of market leaders** in the target quadrant rely on **added salt/sodium** for flavor maintenance. 
* **Strategic Market Discovery**: While flour and wheat represent the category baseline, the natural emergence of "salt" as a top-4 recurring ingredient uncovered a "Hidden Gem" gap. This identifies a clear opportunity for the client to disrupt the market with a **High-Protein, Low-Sugar, and Low-Sodium** alternative—addressing a technical compromise that current leaders have failed to solve[cite: 2, 3].

## D. Bonus Analysis & Challenges

### 5. Bonus User Story: The "Hidden Gem"
*   **Analysis**: I interrogated the unstructured `ingredients_text` column for the "Blue Ocean" cluster (High-Protein/Low-Sugar leaders).
*   **Extraction**: By ranking term frequency naturally via Python's `Counter`, I bypassed category norms (like flour) to identify specific technical ingredients.
*   **Result**: The Top 3 protein-driving sources identified are **Soy**, **Wheat**, and **Peanuts**.

### 6. The "Candidate's Choice" Challenge
*   **Feature Added**: I implemented a **Hexagonal Binning (Hexbin) Plot** in the technical notebook.
*   **Justification**: While standard scatter plots are effective for identifying outliers, they often suffer from "overplotting" in dense datasets. The Hexbin plot provides a clearer representation of **market density**, allowing Helix CPG to see exactly where the majority of current product inventory is concentrated (the "Red Ocean") versus the sparsely populated "Blue Ocean". It transforms a cluttered visual into a clear heat map of market competition.
