Benchmarks test LLM comprehension across different input formats using 209 data retrieval questions on 1 model.

<details>
<summary><strong>Show Dataset Catalog</strong></summary>

#### Dataset Catalog

| Dataset | Rows | Structure | CSV Support | Eligibility |
| ------- | ---- | --------- | ----------- | ----------- |
| Uniform employee records | 100 | uniform | ✓ | 100% |
| E-commerce orders with nested structures | 50 | nested | ✗ | 33% |
| Time-series analytics data | 60 | uniform | ✓ | 100% |
| Top 100 GitHub repositories | 100 | uniform | ✓ | 100% |
| Semi-uniform event logs | 75 | semi-uniform | ✗ | 50% |
| Deeply nested configuration | 11 | deep | ✗ | 0% |
| Valid complete dataset (control) | 20 | uniform | ✓ | 100% |
| Array truncated: 3 rows removed from end | 17 | uniform | ✓ | 100% |
| Extra rows added beyond declared length | 23 | uniform | ✓ | 100% |
| Inconsistent field count (missing salary in row 10) | 20 | uniform | ✓ | 100% |
| Missing required fields (no email in multiple rows) | 20 | uniform | ✓ | 100% |

**Structure classes:**
- **uniform**: All objects have identical fields with primitive values
- **semi-uniform**: Mix of uniform and non-uniform structures
- **nested**: Objects with nested structures (nested objects or arrays)
- **deep**: Highly nested with minimal tabular eligibility

**CSV Support:** ✓ (supported), ✗ (not supported – would require lossy flattening)

**Eligibility:** Percentage of arrays that qualify for TOON's tabular format (uniform objects with primitive values)

</details>

#### Efficiency Ranking (Accuracy per 1K Tokens)

Each format ranked by efficiency (accuracy percentage per 1,000 tokens):

```
TOON           ████████████████████   30.8 acc%/1K tok  │  43.1% acc  │  1,396 tokens
JSON compact   ██████████████████░░   28.1 acc%/1K tok  │  41.1% acc  │  1,464 tokens
YAML           ███████████████░░░░░   23.6 acc%/1K tok  │  38.8% acc  │  1,639 tokens
JSON           █████████████░░░░░░░   19.8 acc%/1K tok  │  39.2% acc  │  1,986 tokens
XML            ███████████░░░░░░░░░   17.6 acc%/1K tok  │  34.4% acc  │  1,952 tokens
```

*Efficiency score = (Accuracy % ÷ Tokens) × 1,000. Higher is better.*

> [!TIP]
> TOON achieves **43.1%** accuracy (vs JSON's 39.2%) while using **29.7% fewer tokens**.

**Note on CSV:** Excluded from ranking as it only supports 109 of 209 questions (flat tabular data only). While CSV is highly token-efficient for simple tabular data, it cannot represent nested structures that other formats handle.

#### Per-Model Accuracy

Accuracy across 1 LLM on 209 data retrieval questions:

```
GigaChat-2
→ TOON           █████████░░░░░░░░░░░    43.1% (90/209)
  JSON compact   ████████░░░░░░░░░░░░    41.1% (86/209)
  JSON           ████████░░░░░░░░░░░░    39.2% (82/209)
  YAML           ████████░░░░░░░░░░░░    38.8% (81/209)
  CSV            ███████░░░░░░░░░░░░░    36.7% (40/109)
  XML            ███████░░░░░░░░░░░░░    34.4% (72/209)
```

> [!TIP]
> TOON achieves **43.1% accuracy** (vs JSON's 39.2%) while using **29.7% fewer tokens** on these datasets.

<details>
<summary><strong>Performance by dataset, model, and question type</strong></summary>

#### Performance by Question Type

| Question Type | TOON | JSON compact | JSON | YAML | CSV | XML |
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Field Retrieval | 85.3% | 88.2% | 83.8% | 82.4% | 87.5% | 79.4% |
| Aggregation | 20.6% | 14.3% | 15.9% | 15.9% | 6.9% | 9.5% |
| Filtering | 6.3% | 2.1% | 0.0% | 0.0% | 0.0% | 0.0% |
| Structure Awareness | 60.0% | 60.0% | 56.0% | 56.0% | 56.3% | 44.0% |
| Structural Validation | 20.0% | 20.0% | 20.0% | 20.0% | 20.0% | 20.0% |

#### Performance by Dataset

##### Uniform employee records

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 43.9% | 1,112 | 18/41 |
| `toon` | 39.0% | 1,173 | 16/41 |
| `json-compact` | 43.9% | 1,580 | 18/41 |
| `yaml` | 41.5% | 1,635 | 17/41 |
| `json-pretty` | 43.9% | 1,946 | 18/41 |
| `xml` | 39.0% | 1,803 | 16/41 |

##### E-commerce orders with nested structures

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 46.3% | 2,854 | 19/41 |
| `json-compact` | 41.5% | 2,668 | 17/41 |
| `yaml` | 39.0% | 2,995 | 16/41 |
| `json-pretty` | 36.6% | 3,406 | 15/41 |
| `xml` | 29.3% | 3,501 | 12/41 |

##### Time-series analytics data

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `json-compact` | 36.7% | 1,107 | 11/30 |
| `toon` | 33.3% | 1,016 | 10/30 |
| `csv` | 30.0% | 964 | 9/30 |
| `json-pretty` | 33.3% | 1,505 | 10/30 |
| `yaml` | 30.0% | 1,490 | 9/30 |
| `xml` | 30.0% | 1,863 | 9/30 |

##### Top 100 GitHub repositories

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `json-compact` | 42.4% | 4,437 | 14/33 |
| `yaml` | 39.4% | 4,486 | 13/33 |
| `csv` | 36.4% | 3,888 | 12/33 |
| `json-pretty` | 39.4% | 4,763 | 13/33 |
| `toon` | 33.3% | 3,499 | 11/33 |
| `xml` | 36.4% | 4,830 | 12/33 |

##### Semi-uniform event logs

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 40.0% | 2,047 | 12/30 |
| `json-compact` | 33.3% | 1,823 | 10/30 |
| `yaml` | 30.0% | 2,175 | 9/30 |
| `json-pretty` | 30.0% | 2,570 | 9/30 |
| `xml` | 26.7% | 2,926 | 8/30 |

##### Deeply nested configuration

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 72.4% | 286 | 21/29 |
| `yaml` | 55.2% | 301 | 16/29 |
| `json-compact` | 51.7% | 289 | 15/29 |
| `json-pretty` | 55.2% | 395 | 16/29 |
| `xml` | 48.3% | 357 | 14/29 |

##### Valid complete dataset (control)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 100.0% | 682 | 1/1 |
| `toon` | 100.0% | 714 | 1/1 |
| `json-compact` | 100.0% | 1,012 | 1/1 |
| `yaml` | 100.0% | 1,190 | 1/1 |
| `json-pretty` | 100.0% | 1,475 | 1/1 |
| `xml` | 100.0% | 1,663 | 1/1 |

##### Array truncated: 3 rows removed from end

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 0.0% | 617 | 0/1 |
| `json-compact` | 0.0% | 92 | 0/1 |
| `json-pretty` | 0.0% | 1,261 | 0/1 |
| `yaml` | 0.0% | 91 | 0/1 |
| `csv` | 0.0% | 589 | 0/1 |
| `xml` | 0.0% | 1,432 | 0/1 |

##### Extra rows added beyond declared length

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 0.0% | 800 | 0/1 |
| `json-compact` | 0.0% | 1,137 | 0/1 |
| `json-pretty` | 0.0% | 1,678 | 0/1 |
| `yaml` | 0.0% | 1,352 | 0/1 |
| `csv` | 0.0% | 266 | 0/1 |
| `xml` | 0.0% | 568 | 0/1 |

##### Inconsistent field count (missing salary in row 10)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 0.0% | 1,192 | 0/1 |
| `json-compact` | 0.0% | 995 | 0/1 |
| `json-pretty` | 0.0% | 1,447 | 0/1 |
| `yaml` | 0.0% | 1,180 | 0/1 |
| `csv` | 0.0% | 659 | 0/1 |
| `xml` | 0.0% | 910 | 0/1 |

##### Missing required fields (no email in multiple rows)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 0.0% | 1,156 | 0/1 |
| `json-compact` | 0.0% | 961 | 0/1 |
| `json-pretty` | 0.0% | 1,395 | 0/1 |
| `yaml` | 0.0% | 1,135 | 0/1 |
| `csv` | 0.0% | 518 | 0/1 |
| `xml` | 0.0% | 1,618 | 0/1 |

#### Performance by Model

##### GigaChat-2

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `toon` | 43.1% | 90/209 |
| `json-compact` | 41.1% | 86/209 |
| `json-pretty` | 39.2% | 82/209 |
| `yaml` | 38.8% | 81/209 |
| `csv` | 36.7% | 40/109 |
| `xml` | 34.4% | 72/209 |

</details>

#### What's Being Measured

This benchmark tests **LLM comprehension and data retrieval accuracy** across different input formats. Each LLM receives formatted data and must answer questions about it. This does **not** test the model's ability to generate TOON output – only to read and understand it.

#### Datasets Tested

Eleven datasets designed to test different structural patterns and validation capabilities:

**Primary datasets:**

1. **Tabular** (100 employee records): Uniform objects with identical fields – optimal for TOON's tabular format.
2. **Nested** (50 e-commerce orders): Complex structures with nested customer objects and item arrays.
3. **Analytics** (60 days of metrics): Time-series data with dates and numeric values.
4. **GitHub** (100 repositories): Real-world data from top GitHub repos by stars.
5. **Event Logs** (75 logs): Semi-uniform data with ~50% flat logs and ~50% with nested error objects.
6. **Nested Config** (1 configuration): Deeply nested configuration with minimal tabular eligibility.

**Structural validation datasets:**

7. **Control**: Valid complete dataset (baseline for validation)
8. **Truncated**: Array with 3 rows removed from end (tests `[N]` length detection)
9. **Extra rows**: Array with 3 additional rows beyond declared length
10. **Width mismatch**: Inconsistent field count (missing salary in row 10)
11. **Missing fields**: Systematic field omissions (no email in multiple rows)

#### Question Types

209 questions are generated dynamically across five categories:

- **Field retrieval (33%)**: Direct value lookups or values that can be read straight off a record (including booleans and simple counts such as array lengths)
  - Example: "What is Alice's salary?" → `75000`
  - Example: "How many items are in order ORD-0042?" → `3`
  - Example: "What is the customer name for order ORD-0042?" → `John Doe`

- **Aggregation (30%)**: Dataset-level totals and averages plus single-condition filters (counts, sums, min/max comparisons)
  - Example: "How many employees work in Engineering?" → `17`
  - Example: "What is the total revenue across all orders?" → `45123.50`
  - Example: "How many employees have salary > 80000?" → `23`

- **Filtering (23%)**: Multi-condition queries requiring compound logic (AND constraints across fields)
  - Example: "How many employees in Sales have salary > 80000?" → `5`
  - Example: "How many active employees have more than 10 years of experience?" → `8`

- **Structure awareness (12%)**: Tests format-native structural affordances (TOON's `[N]` count and `{fields}`, CSV's header row)
  - Example: "How many employees are in the dataset?" → `100`
  - Example: "List the field names for employees" → `id, name, email, department, salary, yearsExperience, active`
  - Example: "What is the department of the last employee?" → `Sales`

- **Structural validation (2%)**: Tests ability to detect incomplete, truncated, or corrupted data using structural metadata
  - Example: "Is this data complete and valid?" → `YES` (control dataset) or `NO` (corrupted datasets)
  - Tests TOON's `[N]` length validation and `{fields}` consistency checking
  - Demonstrates CSV's lack of structural validation capabilities

#### Evaluation Process

1. **Format conversion**: Each dataset is converted to all 6 formats (TOON, JSON compact, JSON, YAML, CSV, XML).
2. **Query LLM**: Each model receives formatted data + question in a prompt and extracts the answer.
3. **Validate deterministically**: Answers are validated using type-aware comparison (e.g., `50000` = `$50,000`, `Engineering` = `engineering`, `2025-01-01` = `January 1, 2025`) without requiring an LLM judge.

#### Models & Configuration

- **Models tested**: `GigaChat-2`
- **Token counting**: Using provider-reported prompt tokens (`inputTokens`) from model responses
- **Temperature**: Not set (models use their defaults)
- **Total evaluations**: 209 questions × 6 formats × 1 models = 1,254 LLM calls
