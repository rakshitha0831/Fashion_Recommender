# Fashion Search-to-Recommendation System

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![NLP](https://img.shields.io/badge/NLP-SentenceTransformers-green)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data--Analysis-yellow)
![Visualization](https://img.shields.io/badge/Visualization-Matplotlib%20%7C%20Seaborn-purple)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## Problem Statement

At FakeFashionCorp, the goal is to improve how fashion products are recommended to users. Two datasets are provided: one that shows a specific user’s Google search history, and another that contains details about 100,000 fashion items in the catalog. The task is to understand the user’s interests based on their search history and suggest products they might like.

## What Was Given as the Dummy Approach

The dummy (basic) approach suggested by the team was:

* Turn the user’s searches into vectors (numbers that represent the meaning of the text).
* Compare those searches to a generic “fashion-related” reference.
* If a search seemed related to fashion, recommend just one similar product.

### Why That Has Limitations:

* It uses one fixed idea of what “fashion” is, which might miss useful searches.
* It only picks one product per relevant search.
* It can ignore searches that are loosely connected but still relevant.
* It doesn't really understand the full meaning of what the user is looking for.

## The Proposed Approach

Instead of comparing to one fixed fashion reference, this solution compares the user’s searches directly to all the products in the catalog. This allows matching based on the actual meaning behind each search and the descriptions of the products.

### Why This Makes More Sense:

* It is more flexible and doesn’t depend on fixed rules.
* It works even if the searches are noisy or unexpected.
* It considers all possible matches and selects the top few.

## How the Approach Works

1. **Read the data** : The user’s search history and the fashion product catalog are loaded.
2. **Clean the text** : Important fields from the product catalog (category, short and long descriptions) are combined to describe each item.
3. **Understand the meaning** : A model called `SentenceTransformer` is used to turn each search and product into a vector — a special format that allows comparison between texts.
4. **Find the best matches** : For each search, the solution compares it to every product and selects the top 5 that are most similar.
5. **Show the results** : The top matching products are printed, and bar charts are created to show their similarity scores.
6. **Extra** : A histogram is also included to show the overall strength of matches for each query.

## Base Approach vs. Enhanced Approach

### Base Approach: TF-IDF Matching

An additional analysis was included using TF-IDF (Term Frequency-Inverse Document Frequency) to match search queries to products. This method represents both the queries and product descriptions as vectors based on word frequencies and calculates similarity using cosine distance.

**Strengths of TF-IDF:**

* Easy to understand and fast to compute
* Works well for short, specific queries with clear keywords
* Interpretable (can see which terms contributed to similarity)

**Limitations of TF-IDF:**

* Does not understand context or synonyms
* May miss connections in vague or indirect queries

### Enhanced Approach: Sentence Transformers

The main approach uses a pre-trained language model (`all-MiniLM-L6-v2`) to create semantic embeddings of both queries and products. This method captures deeper meaning and context beyond just word overlap.

**Strengths of Sentence Transformers:**

* Understands context and semantics, not just keywords
* Matches products even when queries are indirect or noisy
* Returns richer and more accurate recommendations

### Why the Enhanced Approach Is Better

In real-world scenarios, users may not search using product-specific words. The enhanced approach captures their intent better, leading to smarter and more flexible product recommendations.

## What Makes This Different from the Dummy Approach

| What it Does               | Dummy Approach    | Proposed Approach     |
| -------------------------- | ----------------- | --------------------- |
| Uses fixed rules           | Yes               | No                    |
| Compares to all products   | No                | Yes                   |
| Returns top few matches    | No (only 1 match) | Yes (top 5 per query) |
| Understands vague searches | Not really        | Yes                   |
| Easy to extend in future   | No                | Yes                   |

## Example from the Results

Here is one example from the output. For the query:

```
Visited https://www.businessinsider.com/shivon-zilis-reported-mother-elon-musk-twins-2022-7?amp
```

Even though it’s not a fashion search directly, the model found some relevant matches like:

* Round Neck (topwear)
* Skinny (jeans)
* Fm1G085L0041 Mother Of Pearl Leather Watch

This demonstrates that the model is capable of finding meaningful product suggestions even from indirect or non-obvious queries.

## How This Could Be Improved Further

* **Clean up noisy queries** : Skip searches that are clearly unrelated using a simple filter.
* **Make results smarter** : Re-rank the best products based on what other users liked or clicked on.
* **Add personalization** : Use more information about the user if available.
* **Save time** : Store the product vectors so they don’t need to be calculated every time.
* **Make it interactive** : Build a simple web app to allow users to input their search and view recommendations live.

## Technologies Used

* **Python** : Used as the primary programming language for data handling, analysis, and visualization.
* **Pandas & NumPy** : For structured data manipulation and numerical computations.
* **SentenceTransformers (MiniLM)** : A pre-trained NLP model used to convert search queries and product descriptions into dense vector representations.
* **Scikit-learn** : Used for calculating cosine similarity and for implementing TF-IDF vectorization in the baseline approach.
* **TF-IDF (Term Frequency-Inverse Document Frequency)** : Used as a keyword-based method to match user queries with products based on term importance.
* **Matplotlib & Seaborn** : For creating bar charts and histograms to visualize recommendation scores and similarity distributions.
* **JSON** : Both datasets were provided in JSON format and handled using Python’s built-in `json` library.

## Summary

This solution avoids relying on fixed ideas of what counts as fashion-related. Instead, it uses a language model to compare what the user is searching for with product descriptions in the catalog. The result is more relevant, adaptable, and insightful recommendations with room for future improvement.

## Author

**Rakshitha Kamarathi Venkatesh**
📧 Email: [rakshitha0897@gmail.com](mailto:rakshitha0897@gmail.com)
🔗 [LinkedIn](https://www.linkedin.com/in/rakshitha-venkatesh-6824b7306/)
