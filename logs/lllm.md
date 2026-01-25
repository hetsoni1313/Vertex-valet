# LLMs

This document explains the **LLM (Large Language Model) integration** in the book project.

> Allow users to search for books using natural language queries (e.g., *"a story about a lonely robot in space"*) and retrieve relevant results even when exact keywords are not present.

---

## Q1. How can I scrape book descriptions using the Google Books API, and then fetch missing descriptions from the Open Library API for rows that remain blank?

### Answer

This is implemented using a **fallback-based ingestion strategy**.

### Approach

1. Fetch book data (including descriptions) from the **Google Books API**.
2. Store results in a DataFrame.
3. Identify rows where the `description` field is null or empty.
4. Fetch missing descriptions from the **Open Library API** using ISBN.
5. Update only the missing values.

#### ChatGPT provides the code snippets and we used it for reference.
---

## Q2. After fetching data from APIs, how can I re-fetch descriptions from the Google Books API for rows that are still blank?

### Answer

This step acts as a **retry mechanism** to improve data completeness.

### Logic

* Filter rows where `description` is still missing
* Call the Google Books API again
* Update only rows where a valid description is returned

#### ChatGPT provides the code snippets and we used it for reference.
---

## Q3. How can I connect my transformed dataset to a SQLite database using sqlite3 in Python?

### Answer

This step transitions the project from **flat files (CSV)** to **relational storage**, ensuring schema integrity and structured querying.

#### ChatGPT provides the code snippets and we used it for reference.
---

## Q4. How can I create a FastAPI service that allows searching books by ISBN, author name, or title name?

### Answer

This forms the **serving layer** of the project and enables downstream access to curated data.

#### ChatGPT provides the code snippets and we used it for reference.
---

## Summary

* Ingestion uses **multi-source API fallback and retry logic**
* Storage uses **SQLite relational schema**
* Serving uses **FastAPI keyword search APIs**
