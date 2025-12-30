# ReAct-Based PC Building & Hardware Agent

This project implements an autonomous AI agent specialized in **PC Hardware Compatibility and System Building**, developed to solve complex technical queries.

Instead of just reciting memorized information, this agent uses the **ReAct (Reasoning + Acting)** architecture. It works like a smart hardware engineer: it searches a technical knowledge base (RAG), analyzes compatibility rules (e.g., TDP, Socket types), and provides accurate build suggestions without hallucinating specs.

## Project Goal

To analyze user requirements for PC builds (e.g., gaming, rendering, streaming), detect bottlenecks, ensure compatibility between components, and answer technical legacy hardware questions. The agent operates on a **"Thought -> Action -> Observation"** loop to ensure every response is grounded in technical facts.



* **Core LLMs:**
    * **Llama-3.3 70B Versatile (via Groq):** The primary orchestrator for complex reasoning tasks. Selected for its high accuracy in logic-based queries and cost-efficiency.
    * **GPT-4o (via OpenAI):** Used as the "Gold Standard" for benchmark comparison and validation.
* **Methodology:** Retrieval-Augmented Generation (RAG) + ReAct Agent.
* **Custom Tools:**
    * `donanim_arama`: Performs semantic search on the hardware specification database.
    * `SimpleRAG`: A custom lightweight vector search engine using Cosine Similarity.
* **Dataset:** A structured JSON-based knowledge base covering modern and legacy PC components (`hardware_database_FULL.json`).

## Benchmark & Performance Analysis

The agent was evaluated against a rigorous **50-question benchmark set** (40 In-Domain, 10 Out-of-Domain).

| Metric | Llama-3.3 70B (Groq) | GPT-4o (OpenAI) |
| :--- | :--- | :--- |
| **Latency (Avg)** | Moderate (~6s) | Fast (~3.3s) |
| **Cost** | Free (Tier) | High |
| **Technical Accuracy** | ~88% (High) | ~94% (Very High) |
| **Hallucination Rate** | Low (<5%) | Very Low (~0%) |
| **Complex Reasoning** | Excellent | Excellent |

**Conclusion:** Although **GPT-4o** achieved the highest raw accuracy (~94%), **Llama-3.3 70B** followed closely (~88%) and was selected as the optimal production model.

This decision is driven by three key factors:
1. **Cost-Efficiency:** Llama-3.3 (via Groq) offers a significantly lower operational cost compared to proprietary models like GPT-4o.
2. **Speed:** The Groq inference engine provides ultra-low latency per token, ensuring the agent remains responsive during complex reasoning loops.
3. **Accessibility:** As an open-weights model, Llama aligns better with the open-source nature of this project, allowing easier deployment for the community.

## Project Structure

```bash
├── Dataset/
│   └── hardware_database_FULL.json  # Knowledge base for RAG (Specs)
├── Pc_Build_Agent.ipynb             # Jupyter Notebook for experiments
├── Benchmark_Results/               # JSON outputs of model comparisons
│   ├── benchmark_sonuclari_Groq_Llama3.3_70B.json
│   └── benchmark_sonuclari_OpenAI_GPT4o.json
├── requirements.txt                 # Python dependencies
└── README.md                        # Project documentation

How to Run This Project
If you want to run this agent on your local machine or Colab, follow these steps:

1. Clone the Repository
git clone [https://github.com/BarisKilinc1/ReAct-PC-Build-Agent.git](https://github.com/your-username/ReAct-PC-Build-Agent.git)
cd ReAct-PC-Build-Agent

2. Install Dependencies
Make sure you have Python installed, then run:
pip install -r requirements.txt

3. Set API Keys
The project requires API keys for the models you intend to use.

Open agent.py or the Notebook.

Set your keys in the environment or directly in the code:

GROQ_API_KEY (for Llama-3.3)

OPENAI_API_KEY (for GPT-4o Benchmark comparison - Optional)

4. Run the Agent
You can run the script directly or open the notebook:
python agent.py
# OR
jupyter notebook Pc_Build_Agent.ipynb