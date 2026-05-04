# Project Brief: The "Sugar Trap" Market Gap Analysis

**Client:** Helix CPG Partners (Strategic Food & Beverage Consultancy)  
**Deliverable:** Interactive Dashboard, Code Notebook & Insight Presentation

---

## 1. Business Context
**Helix CPG Partners** advises major food manufacturers on new product development. Our newest client, a global snack manufacturer, wants to launch a "Healthy Snacking" line. They believe the market is oversaturated with sugary treats, but they lack the data to prove where the specific gaps are.

They have hired us to answer one question: **"Where is the 'Blue Ocean' in the snack aisle?"**

Specifically, they are looking for product categories that are currently under-served—areas where consumer demand for health (e.g., High Protein, High Fiber) is not being met by current product offerings (which are mostly High Sugar, High Fat).

## 2. The Data
You will use the **Open Food Facts** dataset, a free, open, and massive database of food products from around the world.

* **Source:** [Open Food Facts Data](https://world.openfoodfacts.org/data)
* **Format:** CSV (Comma Separated Values)
* **Warning:** The full dataset is massive (over 3GB). You are **not** expected to process the entire file. You should filter the data early or work with a manageable subset (e.g., the first 500,000 rows or specific categories).

## 3. Tooling Requirements
You have the flexibility to choose your development environment:

* **Option A (Recommended):** Use a cloud-hosted notebook like **Google Colab**, or **Deepnote**, etc.
* **Option B:** Use a local **Jupyter Notebook** or **VS Code**.
    * *Condition:* If you choose this, you must ensure your code is reproducible. Do not reference local file paths (e.g., `C:/Downloads/...`). Assume the dataset is in the same folder as your notebook.
* **Dashboarding:** The final output must be a **publicly accessible link** (e.g., Tableau Public, Google Looker Studio, Streamlit Cloud, or PowerBI Web).

---

## 4. User Stories & Acceptance Criteria

### Story 1: Data Ingestion & "The Clean Up"
**As a** Strategy Director,  
**I want** a clean dataset that removes products with erroneous nutritional information,  
**So that** my analysis is not skewed by bad data entry.

* **Acceptance Criteria:**
    * Handle missing values: Decide what to do with rows that have `null` or empty `sugars_100g`, `proteins_100g`, or `product_name`.
    * Handle outliers: Filter out biologically impossible values.
    * **Deliverable:** A cleaned Pandas DataFrame or SQL table export.

### Story 2: The Category Wrangler
**As a** Product Manager,  
**I want** to group products into readable high-level categories,  
**So that** I don't have to look at 10,000 unique, messy tags like `en:chocolate-chip-cookies-with-nuts`.

* **Acceptance Criteria:**
    * The `categories_tags` column is a comma-separated string (e.g., `en:snacks, en:sweet-snacks, en:biscuits`). You must parse this string.
    * Create a logic to assign a "Primary Category" to each product based on keywords.
    * Create at least 5 distinct high-level buckets.

### Story 3: The "Nutrient Matrix" Visualization
**As a** Marketing Lead,  
**I want** to see a Scatter Plot comparing Sugar (X-axis) vs. Protein (Y-axis) for different categories,  
**So that** I can visually spot where the products are clustered.

* **Acceptance Criteria:**
    * Create a dashboard (PowerBI, Tableau, Streamlit, or Python-based charts) displaying this relationship.
    * Allow the user to filter the chart by the "High Level Categories" you created in Story 2.
    * **Key Visual:** Identify the "Empty Quadrant" (e.g., High Protein + Low Sugar).

### Story 4: The Recommendation
**As a** Client,  
**I want** a clear text recommendation on what product we should build,  
**So that** I can take this to the R&D team.

* **Acceptance Criteria:**
    * On the dashboard, include a "Key Insight" box.
    * Complete this sentence: *"Based on the data, the biggest market opportunity is in [Category Name], specifically targeting products with [X]g of protein and less than [Y]g of sugar."*

---

## 5. Bonus User Story: The "Hidden Gem"
**As a** Health Conscious Consumer,  
**I want** to know which specific ingredients are driving the high protein content in the "good" products,  
**So that** I can replicate this in our new recipe.

* **Acceptance Criteria:**
    * Analyze the `ingredients_text` column for products in your "High Protein" cluster.
    * Extract and list the Top 3 most common protein sources (e.g., "Whey", "Peanuts", "Soy").

---

## 6. The "Candidate's Choice" Challenge
**As a** Creative Analyst,  
**I want** to add one additional feature or analysis to this project that I believe provides massive value,  
**So that** I can show off my business acumen.

* **Instructions:**
    * Add one more chart, filter, or metric that wasn't asked for.
    * Explain **why** you added it.
    * **There is no wrong answer, but you must justify your choice.**

---

## 7. Submission Guidelines
Please edit this `README.md` file in your forked repository to include the following three sections at the top:

### A. The Executive Summary
* I analysed a randomised sample of 200,000 records from the Open Food Facts dataset to find a Blue Ocean for Helix CPG Partners. Most traditional snacks have 30% of their weight as pure sugar. My analysis shows that Plant-based snacks are the most efficient category for delivering high protein with low sugar. However, my ingredient mining found that these current products rely heavily on salt and wheat as fillers. The biggest opportunity is to create a high-protein, low-sugar plant-based snack targeting people who would take in little sodium.

### B. Project Links
* **Link to Notebook:** [https://colab.research.google.com/drive/1g9IOUvxUD-vbHrOmTxIRqhmQD_6wKxuP?usp=sharing](https://colab.research.google.com/drive/1g9IOUvxUD-vbHrOmTxIRqhmQD_6wKxuP?usp=sharing) 
* **Link to Dashboard:** [https://datastudio.google.com/reporting/34881442-2f4f-48c8-a6eb-f5186f5a4d28](https://datastudio.google.com/reporting/34881442-2f4f-48c8-a6eb-f5186f5a4d28)
* **Link to Presentation:** [https://the-market-gap-analysis.vercel.app/](https://the-market-gap-analysis.vercel.app/) ; [Video walkthrough](https://youtu.be/Y-y_pUaB_H8)

### C. Technical Explanation
* To handle the massive 12GB dataset efficiently, I streamed the first 500,000 rows directly from the source URL using the nrows parameter in Pandas. This allowed me to perform a randomised shuffle to extract a representative 200,000-row subset without exceeding memory limits. I cleaned the data by enforcing biological boundaries where sugars and proteins must be between $0$ and $100$ grams per 100g. I also dropped any records missing critical names or nutritional values because imputing that data would introduce bias into a gap analysis. To ensure I understood the schema before filtering, I consulted the official field descriptions. Comparing this to the project user stories which require a focused "Market Gap" study for the snack aisle, I selected five high-level business buckets (Snacks, Beverages, Dairy, Plant-based, and Cereals) using keyword matching on the categories_tags. This approach allowed me to ignore "noise" like pet food or raw commodities and focus strictly on the consumer packaged goods relevant to the client.
* I added two specific features to differentiate my analysis and provide deeper value to the stakeholders. I created a Nutrient Density Score calculated as $Protein/(Sugar + 1)$ to help the client identify which categories are the most efficient at delivering nutrition without the typical sugar overhead found in processed foods. Additionally, I built a variable ingredient mining function using Regular Expressions to parse the unstructured ingredients_text field. By setting the Top N count as a variable, the analysis can be easily adjusted to different depths of research. This process revealed that salt is the most common ingredient in high-protein plant-based clusters. This provides a critical business insight by showing that even healthy snacks have a hidden sodium problem that the client can solve to further differentiate their product.

**Important Note on Code Submission:**
* Upload your `.ipynb` notebook file to the repo.
* **Crucial:** Also upload an **HTML or PDF export** of your notebook so we can see your charts even if GitHub fails to render the notebook code.
* Once you are ready, please fill out the [Official Submission Form Here](https://forms.office.com/e/heitZ9PP7y) with your links

---

## 🛑 CRITICAL: Pre-Submission Checklist

**Before you submit your form, you MUST complete this checklist.**

> ⚠️ **WARNING:** If you miss any of these items, your submission will be flagged as "Incomplete" and you will **NOT** be invited to an interview. 
>
> **We do not accept "permission error" excuses. Test your links in Incognito Mode.**

### 1. Repository & Code Checks
- [ ] **My GitHub Repo is Public.** (Open the link in a Private/Incognito window to verify).
- [ ] **I have uploaded the `.ipynb` notebook file.**
- [ ] **I have ALSO uploaded an HTML or PDF export** of the notebook.
- [ ] **I have NOT uploaded the massive raw dataset.** (Use `.gitignore` or just don't commit the CSV).
- [ ] **My code uses Relative Paths.** 

### 2. Deliverable Checks
- [ ] **My Dashboard link is publicly accessible.** (No login required).
- [ ] **My Presentation link is publicly accessible.** (Permissions set to "Anyone with the link can view").
- [ ] **I have updated this `README.md` file** with my Executive Summary and technical notes.

### 3. Completeness
- [ ] I have completed **User Stories 1-4**.
- [ ] I have completed the **"Candidate's Choice"** challenge and explained it in the README.

**✅ Only when you have checked every box above, proceed to the submission form.**

---
