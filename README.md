# smart-product-comparison
## **Project Overview: Smart Product Comparison Web App**

### **Project Title:**

**Smart Multi-Site Product Comparison Web Application**

### **Objective:**

The goal of this project is to enable users to **view products from multiple e-commerce websites side by side**, compare their attributes (price, specs, rating, images), and make an informed decision on the product they want to purchase. Unlike traditional comparison tools, this project allows users to **choose the best product themselves** instead of automatically calculating “best value” or “best price.”

---

### **Architecture Overview:**

1. **Frontend:**

   * Can be a web interface or mobile app that takes a **product URL** from the user.
   * Displays **side-by-side product details** (name, price, specs, images, rating) from multiple e-commerce platforms.
   * Users can visually compare and decide which product fits their needs.

2. **Backend (Flask API):**

   * **Endpoints:**

     * `/api/compare` → Given a product URL, returns matching products from other sites with all details.
     * `/api/history` → Retrieves past searches.
     * `/api/history/<id>` → Get or delete a specific search.
     * `/api/recheck/<id>` → Re-fetch products for a previous search.
   * Handles **scraping, matching, and response formatting**.

3. **Scrapers:**

   * Individual scrapers for each site (`FlipkartScraper`, `SnapdealScraper`, `TataCliqScraper`, `CromaScraper`, `RelianceDigitalScraper`).
   * Capabilities:

     * **Extract product details from a URL** (name, price, specs, rating, image).
     * **Search products** on the platform using a keyword-based query.
     * Handle multiple CSS classes and structure changes (robust selectors).

4. **Product Matching (matching.py):**

   * Uses **fuzzy string matching** (RapidFuzz) to identify the same product across different platforms.
   * Extracts **key features** like brand, model, and specs.
   * Deduplicates results to avoid showing duplicates.

5. **Database:**

   * Stores **search history**, including source URL, returned products, and timestamps.
   * Allows re-checking or deleting past searches.

---

### **Workflow (Step by Step):**

1. User enters a **product URL** on the frontend.
2. Backend detects the **site of origin** (Flipkart, Snapdeal, etc.).
3. **Scraper** extracts product details from the URL.
4. Keywords are extracted from the product name to form a **search query**.
5. Scrapers for other platforms **search for similar products** using the query.
6. **Matching module** finds the top matching products across platforms using fuzzy matching.
7. Backend **returns all matched products** with their details (name, price, specs, rating, image) in JSON.
8. Frontend displays products **side by side**, allowing the user to manually select the best one.

---

### **Key Features:**

* Supports **multiple e-commerce platforms**.
* Robust scraping logic for site layout changes.
* **Side-by-side comparison** with all relevant product attributes.
* Maintains **search history** for future reference.
* Uses **fuzzy matching** to identify the same product across different platforms.

---

### **Technologies Used:**

* **Python** for backend logic.
* **Flask** for API development.
* **BeautifulSoup / Requests** for scraping (optionally Selenium if needed for dynamic content).
* **RapidFuzz** for fuzzy string matching.
* **SQLite / PostgreSQL** (or any preferred database) for storing search history.
* **Frontend:** HTML/CSS/JS, React, or any web framework for displaying results.

---

### **Future Enhancements:**

* Integrate **dynamic scraping with Selenium** for JavaScript-heavy websites.
* Add **price alerts** and notifications when products drop in price.
* Add **filters** for attributes like RAM, storage, or ratings.
* Enhance the **frontend UX** with sorting, comparison charts, and image previews.
* Add **user accounts** to save and track favorite products.

---

### **Conclusion:**

This project demonstrates a **complete pipeline** from URL-based product extraction, cross-platform searching, matching similar products, and presenting a **side-by-side comparison** for end-users. By removing automatic “best value” computation, the app empowers users to **make informed purchasing decisions** while ensuring flexibility and adaptability to website changes.
