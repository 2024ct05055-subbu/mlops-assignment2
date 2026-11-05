# LLMops Educational Assistant: Prompt Engineering & Metric Evaluation

This repository evaluates LLM prompt optimization, cost structures, and tracking using MLflow. It benchmarks three iterations of prompts designed for an automated educational student dashboard system.

---

## Table of Contents
1. [Project Setup](#project-setup)
2. [Prompt Variations](#prompt-variations)
3. [Evaluation Metrics & Results](#evaluation-metrics--results)
4. [Token and Cost Projections](#token-and-cost-projections)
5. [Production Promotion Justification](#production-promotion-justification)
6. [Requirements](#requirements)

---

## Project Setup

1. **Prerequisites & Installation**:
   Install the required libraries listed in `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```

2. **API Secret Configuration**:
   Configure your API key as a Colab secret under the name `OPENAI_API_KEY`.

3. **Run Evaluations**:
   Execute the notebook evaluation cell (`6d5f2669`) to execute runs, record structured text configurations, compute latencies, and track all artifacts directly into MLflow.

---

## Prompt Variations

* **`Prompt_v1_Basic`**: Quick, direct instructions. Useful for basic queries but output has no standard formatting structure.
* **`Prompt_v2_Structured`**: Designed as an academic assistant using simplified vocabulary suitable for undergraduate students.
* **`Prompt_v3_JSON_Output`**: Constrains the model output strictly to a predefined structural JSON schema containing an academic answer, confidence level, and key points.

---

## Evaluation Metrics & Results

Based on baseline testing, here is the aggregate comparative summary recorded inside `prompt_evaluation_results.csv`:

| Prompt Version | Avg Latency | Avg Input Tokens | Avg Output Tokens | Avg Cost (USD) | Valid JSON Rate | Recommended? |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Prompt_v1_Basic** | 0.10s | 17.0 | 134.0 | $0.0000415 | N/A | No |
| **Prompt_v2_Structured** | 0.10s | 47.0 | 222.0 | $0.0000701 | N/A | No |
| **Prompt_v3_JSON_Output** | 0.10s | 87.0 | 119.0 | $0.0000422 | 100.0% | **Yes (Best choice for automated pipelines)** |

---

## Token and Cost Projections
For a regular monthly operational workload of **10,000 requests** under `gemini-2.5-flash-lite` pricing standards, we observe the following costs:
* **Prompt_v1_Basic**: $0.4148 (~₹35.88)
* **Prompt_v2_Structured**: $0.7012 (~₹60.66)
* **Prompt_v3_JSON_Output**: $0.4222 (~₹36.52)

### Optimization Tips:
1. **Caching**: Utilize context-aware system prompting parameters to reduce input pricing footprints.
2. **Minified Schemas**: Shorten descriptions within prompt templates or transition to programmatic Pydantic models.

---

## Production Promotion Justification

**`Prompt_v3_JSON_Output`** is flagged with the `production` tag inside MLflow due to:
* **Reliable Integration**: Valid 100% JSON parsing allows seamless integration with backend APIs.
* **High Efficiency**: Limits output verbosity to only 119 tokens on average (compared to 222 in prompt 2).
* **Substantial Value**: Delivers the safety benefits of high-level structure at practically equivalent operational costs to basic, unstructured prompts.
