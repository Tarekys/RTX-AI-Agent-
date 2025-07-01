# 🧠 RTX 5070 Procurement AI Agents

This project is an AI-powered system made up of **4 collaborative agents**. Their main goal is to help the user find the **best place and price** to buy an **RTX 5070 graphics card** by searching, extracting, analyzing, and reporting product data from e-commerce websites.

---

## ✅ Project Idea

Automatically search for RTX 5070 listings online, compare product specifications and prices, and generate a professional procurement report.

---

## ⚙️ Technologies Used

- 🤖 [CrewAI](https://github.com/joaomdmoura/crewai) for multi-agent orchestration
- 🌐 Tavily for real-time web search
- 🕷️ Scrapegraph for smart web scraping
- 📊 AgentOps for agent performance tracking
- 🦙 Meta LLaMA-4 (17B) as the main language model

---

## 🤖 The Four Agents

### 1️⃣ Search Queries Recommendation Agent

- **Role**: Generates specific search queries about RTX 5070.
- **Output**: JSON with ~5 suggested search queries.
```json
{ "queries": ["Buy RTX 5070 Egypt", "NVIDIA RTX 5070 best price", ...] }
```

---

### 2️⃣ Search Engine Agent

- **Role**: Searches for RTX 5070 products using the suggested queries.
- **Output**: A list of product URLs with a confidence score.
```json
{
  "results": [
    {
      "title": "NVIDIA RTX 5070 on Amazon",
      "url": "https://www.amazon.eg/product...",
      "score": 0.87,
      ...
    }
  ]
}
```

---

### 3️⃣ Web Scraping Agent

- **Role**: Visits product URLs and extracts:
  - Title, price, image, discount
  - 3–5 main specifications (e.g., RAM, brand, cooling)
  - Agent recommendation score and notes
- **Output**: JSON with detailed info of the top products.
```json
{
  "products": [
    {
      "product_title": "ASUS RTX 5070 Dual",
      "product_current_price": 17999,
      "product_specs": [
        { "specification_name": "RAM", "specification_value": "12GB GDDR6X" }
      ],
      "agent_recommendation_rank": 1
    }
  ]
}
```

---

### 4️⃣ Procurement Report Author Agent

- **Role**: Writes a final **HTML procurement report** using all gathered data.
- **Output**: Clean Bootstrap-styled HTML page with:
  - Executive summary
  - Methodology
  - Price comparisons
  - Analysis & charts
  - Final recommendation

---

## 🚀 How to Run

1. Set the required API keys in environment variables.
2. Modify the input parameters like:
```python
inputs={
  "product_name": "RTX 5070",
  "websites_list": [...],
  "country_name": "Egypt",
  "no_keywords": 5,
  "language": "English",
  "score_th": 0.50,
  "top_recommendations_no": 5
}
```
3. Launch with:
```python
crew_results = rankyx_crew.kickoff(inputs=inputs)
```

---

## 📂 Outputs

Generated in the `Agents-output/` folder:
- Search queries JSON
- Search results JSON
- Scraped product info JSON
- Final HTML report