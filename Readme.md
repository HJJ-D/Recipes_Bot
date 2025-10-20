# 🍳 Recipe Assistant – Your Personal Chinese Chef

**Team Members:** Xiaochuan Ai, Lan Xiao, Junjie Hu  
**Date:** October 2025  
**University:** Uppsala University  

---

## 🧠 Project Overview

This project builds an **intelligent Chinese recipe chatbot** based on **Retrieval-Augmented Generation (RAG)** and **Gemini (gemini-2.5-flash-lite)**.  
The chatbot allows users to input ingredients, desired flavor, cooking time, and difficulty level — and automatically generates authentic **Chinese-style recipes** with detailed steps through an interactive **Gradio interface**.

The motivation comes from the real experience of **Chinese students abroad** who often struggle to find Chinese recipes suited to local ingredients.  
Our goal is to create a culturally aware system that makes **home cooking simple, personalized, and meaningful** — helping users reconnect with Chinese food traditions even while overseas.

---

## 📂 Project Structure

```plaintext
├── .gitignore
├── crawel.ipynb
├── final_version_LLM.ipynb
├── initial_vector_database.ipynb
├── otherstaff_test_prompt.csv
├── outputs
│   ├── baseline
│   │   └── baseline_metrics_results.csv
│   └── metrics_results.csv
├── recipes-final.csv
├── recipes_prompt_label.csv
├── test.ipynb
├── test_baseline.ipynb
└── test_prompt_label.csv
```

## ⚙️ Components Description

### 🔹 Code Files

| File                            | Description                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| `crawel.ipynb`                  | Web scraping notebook used to collect ~11,400 raw recipes from *Xiachufang.com*. |
| `initial_vector_database.ipynb` | Preprocesses and stores the cleaned recipes into a **ChromaDB** vector database using `BAAI/bge-m3` embeddings. |
| `final_version_LLM.ipynb`       | Main chatbot code integrating **RAG**, **Gemini**, **safety filters**, and **Gradio UI** for interaction. |
| `test.ipynb`                    | Tests model performance with RAG-enabled retrieval.          |
| `test_baseline.ipynb`           | Baseline comparison: Gemini-only responses (no RAG).         |

### 🔹 Data Files

| File                         | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| `recipes-final.csv`          | Final cleaned dataset (~4,000 recipes) after filtering, deduplication, and AI-assisted translation. |
| `recipes_prompt_label.csv`   | Test dataset with prompts and expected outputs for evaluating recipe generation. |
| `otherstaff_test_prompt.csv` | Dataset containing unrelated (non-cooking) prompts for robustness and safety testing. |
| `test_prompt_label.csv`      | Additional labeled prompts for final evaluation.             |

### 🔹 Output Files

| File                                            | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- |
| `outputs/metrics_results.csv`                   | Evaluation results of the RAG-enhanced model.   |
| `outputs/baseline/baseline_metrics_results.csv` | Baseline results from Gemini without retrieval. |

------

## 🧩 System Architecture

The chatbot architecture integrates **retrieval, generation, safety, and memory** components to ensure accurate and safe recipe outputs.

### Workflow Summary

```
User Input  
   v  
check_input_safe()          <- Filters unsafe or harmful inputs  
   v  
get_memory_from_history()   <- Retrieves recent conversation context from chat history  
   v  
should_use_rag()            <- Determines whether the query requires recipe retrieval (RAG)  
   v  
retrieve_recipes()          <- Performs vector-based retrieval from the recipe database if needed  
   v  
Prompt Construction          <- Combines history, retrieved data, and user query
   v  
Gemini model.generate_content(stream=True)  
                              <- Generates the response in a streaming manner  
   v  
sanitize_output()            <- Scans and removes unsafe or toxic phrases from the model’s output  
   v  
Display to User (streamed response)

```

## 📊 Experimental Results

### Quantitative Evaluation

| Model              | Recall | Precision | F1-score |
| ------------------ | ------ | --------- | -------- |
| Baseline (no RAG)  | 0.916  | 0.390     | 0.523    |
| RAG-enhanced Model | 0.903  | 0.410     | 0.541    |

- Both models achieved **>90% recall**, meaning broad ingredient coverage.
- The **RAG model** showed **higher precision and F1**, reducing hallucinated or irrelevant ingredients.

### Qualitative Findings

- The RAG version produces recipes that better match **authentic Chinese styles**.
- The baseline Gemini model, while creative, sometimes generated unrealistic ingredient combinations.
- Overall, RAG grounding improves factual accuracy and cultural realism.

------

## 💬 Societal Impact

### 1. Everyday Life, Culture, and Connection

The chatbot helps students and workers abroad cook Chinese food with local ingredients.
 Cooking becomes a way to **reconnect with culture and reduce homesickness**, while promoting cultural exchange in shared kitchens or international student communities.

### 2. Ethical and Social Considerations

- **Bias**: Popular cuisines (e.g., Sichuan, Cantonese) may dominate the dataset, underrepresenting minority cuisines.
- **Privacy**: User data (dietary habits, allergies, religious preferences) must be protected transparently.
- **Cultural Representation**: The system should avoid stereotyping Chinese food and instead reflect its **diversity and flexibility**.

------

## 🤖 Use of AI During Development

- Debugging logic errors in memory–UI integration (Gradio).
- Cleaning and normalizing recipe metadata.
- Grammar and language correction in the report and dataset.

------

## 🚀 Future Work

- Expand recipe coverage (regional and minority cuisines).
- Improve retrieval ranking and personalization.
- Add image-based recipe recognition and multimodal input.
- Conduct real-time performance and latency analysis.

------

## 📄 License

This project is for **educational and research purposes only**.
 Data scraped from *Xiachufang.com* was used responsibly for academic study.