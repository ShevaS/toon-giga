Benchmarks test LLM comprehension across different input formats using 2 data retrieval questions on 1 model.

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
TOON           ████████████████████   38.4 acc%/1K tok  │  100.0% acc  │  2,605 tokens
JSON compact   ███████████░░░░░░░░░   20.9 acc%/1K tok  │  100.0% acc  │  4,789 tokens
YAML           █████████░░░░░░░░░░░   17.5 acc%/1K tok  │  100.0% acc  │  5,727 tokens
JSON           ███████░░░░░░░░░░░░░   14.1 acc%/1K tok  │  100.0% acc  │  7,096 tokens
XML            ██████░░░░░░░░░░░░░░   12.3 acc%/1K tok  │  100.0% acc  │  8,101 tokens
```

*Efficiency score = (Accuracy % ÷ Tokens) × 1,000. Higher is better.*

> [!TIP]
> TOON achieves **100.0%** accuracy (vs JSON's 100.0%) while using **63.3% fewer tokens**.

**Note on CSV:** Excluded from ranking as it only supports 2 of 2 questions (flat tabular data only). While CSV is highly token-efficient for simple tabular data, it cannot represent nested structures that other formats handle.

#### Per-Model Accuracy

Accuracy across 1 LLM on 2 data retrieval questions:

```
GigaChat-2
  JSON           ████████████████████   100.0% (2/2)
  JSON compact   ████████████████████   100.0% (2/2)
→ TOON           ████████████████████   100.0% (2/2)
  CSV            ████████████████████   100.0% (2/2)
  XML            ████████████████████   100.0% (2/2)
  YAML           ████████████████████   100.0% (2/2)
```

> [!TIP]
> TOON achieves **100.0% accuracy** (vs JSON's 100.0%) while using **63.3% fewer tokens** on these datasets.

<details>
<summary><strong>Performance by dataset, model, and question type</strong></summary>

#### Performance by Question Type

| Question Type | JSON | JSON compact | TOON | CSV | XML | YAML |
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Field Retrieval | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% | 100.0% |

#### Performance by Dataset

##### Uniform employee records

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 100.0% | 2,605 | 2/2 |
| `csv` | 100.0% | 3,084 | 2/2 |
| `json-compact` | 100.0% | 4,789 | 2/2 |
| `yaml` | 100.0% | 5,727 | 2/2 |
| `json-pretty` | 100.0% | 7,096 | 2/2 |
| `xml` | 100.0% | 8,101 | 2/2 |

#### Performance by Model

##### GigaChat-2

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `json-pretty` | 100.0% | 2/2 |
| `json-compact` | 100.0% | 2/2 |
| `toon` | 100.0% | 2/2 |
| `csv` | 100.0% | 2/2 |
| `xml` | 100.0% | 2/2 |
| `yaml` | 100.0% | 2/2 |

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

2 questions are generated dynamically across five categories:

- **Field retrieval (3400%)**: Direct value lookups or values that can be read straight off a record (including booleans and simple counts such as array lengths)
  - Example: "What is Alice's salary?" → `75000`
  - Example: "How many items are in order ORD-0042?" → `3`
  - Example: "What is the customer name for order ORD-0042?" → `John Doe`

- **Aggregation (3150%)**: Dataset-level totals and averages plus single-condition filters (counts, sums, min/max comparisons)
  - Example: "How many employees work in Engineering?" → `17`
  - Example: "What is the total revenue across all orders?" → `45123.50`
  - Example: "How many employees have salary > 80000?" → `23`

- **Filtering (2400%)**: Multi-condition queries requiring compound logic (AND constraints across fields)
  - Example: "How many employees in Sales have salary > 80000?" → `5`
  - Example: "How many active employees have more than 10 years of experience?" → `8`

- **Structure awareness (1250%)**: Tests format-native structural affordances (TOON's `[N]` count and `{fields}`, CSV's header row)
  - Example: "How many employees are in the dataset?" → `100`
  - Example: "List the field names for employees" → `id, name, email, department, salary, yearsExperience, active`
  - Example: "What is the department of the last employee?" → `Sales`

- **Structural validation (250%)**: Tests ability to detect incomplete, truncated, or corrupted data using structural metadata
  - Example: "Is this data complete and valid?" → `YES` (control dataset) or `NO` (corrupted datasets)
  - Tests TOON's `[N]` length validation and `{fields}` consistency checking
  - Demonstrates CSV's lack of structural validation capabilities

#### Evaluation Process

1. **Format conversion**: Each dataset is converted to all 6 formats (JSON, JSON compact, TOON, CSV, XML, YAML).
2. **Query LLM**: Each model receives formatted data + question in a prompt and extracts the answer.
3. **Validate deterministically**: Answers are validated using type-aware comparison (e.g., `50000` = `$50,000`, `Engineering` = `engineering`, `2025-01-01` = `January 1, 2025`) without requiring an LLM judge.

#### Models & Configuration

- **Models tested**: `GigaChat-2`
- **Token counting**: Using provider-reported prompt tokens (`inputTokens`) from model responses
- **Temperature**: Not set (models use their defaults)
- **Total evaluations**: 2 questions × 6 formats × 1 models = 12 LLM calls
