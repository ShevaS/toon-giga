Benchmarks test LLM comprehension across different input formats using 209 data retrieval questions on 5 models.

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
TOON           ████████████████████   24.9 acc%/1K tok  │  69.8% acc  │  2,803 tokens
JSON compact   █████████████████░░░   21.7 acc%/1K tok  │  67.2% acc  │  3,095 tokens
YAML           ███████████████░░░░░   18.4 acc%/1K tok  │  67.4% acc  │  3,667 tokens
JSON           ████████████░░░░░░░░   14.8 acc%/1K tok  │  67.8% acc  │  4,579 tokens
XML            ██████████░░░░░░░░░░   12.6 acc%/1K tok  │  64.6% acc  │  5,131 tokens
```

*Efficiency score = (Accuracy % ÷ Tokens) × 1,000. Higher is better.*

> [!TIP]
> TOON achieves **69.8%** accuracy (vs JSON's 67.8%) while using **38.8% fewer tokens**.

**Note on CSV:** Excluded from ranking as it only supports 109 of 209 questions (flat tabular data only). While CSV is highly token-efficient for simple tabular data, it cannot represent nested structures that other formats handle.

#### Per-Model Accuracy

Accuracy across 5 LLMs on 209 data retrieval questions:

```
claude-haiku-4-5-20251001
→ TOON           ████████████░░░░░░░░    59.8% (125/209)
  JSON           ███████████░░░░░░░░░    57.4% (120/209)
  YAML           ███████████░░░░░░░░░    56.0% (117/209)
  XML            ███████████░░░░░░░░░    55.5% (116/209)
  JSON compact   ███████████░░░░░░░░░    55.0% (115/209)
  CSV            ██████████░░░░░░░░░░    50.5% (55/109)

gemini-3-flash-preview
  XML            ████████████████████    98.1% (205/209)
  JSON           ███████████████████░    97.1% (203/209)
  YAML           ███████████████████░    97.1% (203/209)
→ TOON           ███████████████████░    96.7% (202/209)
  JSON compact   ███████████████████░    96.7% (202/209)
  CSV            ███████████████████░    96.3% (105/109)

gpt-5-nano
→ TOON           ██████████████████░░    90.9% (190/209)
  JSON compact   ██████████████████░░    90.9% (190/209)
  JSON           ██████████████████░░    89.0% (186/209)
  CSV            ██████████████████░░    89.0% (97/109)
  YAML           █████████████████░░░    87.1% (182/209)
  XML            ████████████████░░░░    80.9% (169/209)

grok-4-1-fast-non-reasoning
→ TOON           ████████████░░░░░░░░    58.4% (122/209)
  YAML           ████████████░░░░░░░░    57.9% (121/209)
  JSON           ███████████░░░░░░░░░    56.5% (118/209)
  XML            ███████████░░░░░░░░░    54.1% (113/209)
  JSON compact   ██████████░░░░░░░░░░    52.2% (109/209)
  CSV            ██████████░░░░░░░░░░    51.4% (56/109)

GigaChat-2
→ TOON           █████████░░░░░░░░░░░    43.1% (90/209)
  JSON compact   ████████░░░░░░░░░░░░    41.1% (86/209)
  JSON           ████████░░░░░░░░░░░░    39.2% (82/209)
  YAML           ████████░░░░░░░░░░░░    38.8% (81/209)
  CSV            ███████░░░░░░░░░░░░░    36.7% (40/109)
  XML            ███████░░░░░░░░░░░░░    34.4% (72/209)
```

> [!TIP]
> TOON achieves **69.8% accuracy** (vs JSON's 67.8%) while using **38.8% fewer tokens** on these datasets.

<details>
<summary><strong>Performance by dataset, model, and question type</strong></summary>

#### Performance by Question Type

| Question Type | TOON | JSON | YAML | JSON compact | CSV | XML |
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Field Retrieval | 96.8% | 96.2% | 95.3% | 96.5% | 97.5% | 95.0% |
| Aggregation | 53.7% | 52.7% | 51.1% | 49.5% | 42.1% | 45.4% |
| Filtering | 46.7% | 42.5% | 45.0% | 44.6% | 40.7% | 41.3% |
| Structure Awareness | 83.2% | 80.8% | 78.4% | 79.2% | 80.0% | 73.6% |
| Structural Validation | 60.0% | 52.0% | 52.0% | 48.0% | 68.0% | 72.0% |

#### Performance by Dataset

##### Uniform employee records

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 67.3% | 2,465 | 138/205 |
| `toon` | 66.3% | 2,591 | 136/205 |
| `json-compact` | 67.8% | 3,865 | 139/205 |
| `yaml` | 67.3% | 4,727 | 138/205 |
| `json-pretty` | 67.8% | 6,230 | 139/205 |
| `xml` | 67.3% | 7,051 | 138/205 |

##### E-commerce orders with nested structures

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 75.1% | 7,116 | 154/205 |
| `json-compact` | 71.2% | 6,757 | 146/205 |
| `yaml` | 71.7% | 8,093 | 147/205 |
| `json-pretty` | 70.7% | 10,667 | 145/205 |
| `xml` | 67.8% | 11,833 | 139/205 |

##### Time-series analytics data

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 69.3% | 1,686 | 104/150 |
| `csv` | 66.0% | 1,608 | 99/150 |
| `json-compact` | 66.7% | 2,331 | 100/150 |
| `yaml` | 66.7% | 2,959 | 100/150 |
| `json-pretty` | 66.7% | 3,630 | 100/150 |
| `xml` | 64.0% | 4,241 | 96/150 |

##### Top 100 GitHub repositories

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 60.0% | 8,530 | 99/165 |
| `toon` | 60.0% | 8,620 | 99/165 |
| `json-compact` | 56.4% | 11,061 | 93/165 |
| `yaml` | 60.0% | 12,542 | 99/165 |
| `json-pretty` | 58.8% | 14,569 | 97/165 |
| `xml` | 52.1% | 16,210 | 86/165 |

##### Semi-uniform event logs

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `json-compact` | 61.3% | 4,571 | 92/150 |
| `toon` | 60.0% | 5,459 | 90/150 |
| `json-pretty` | 61.3% | 6,581 | 92/150 |
| `yaml` | 55.3% | 5,471 | 83/150 |
| `xml` | 52.0% | 7,382 | 78/150 |

##### Deeply nested configuration

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 90.3% | 752 | 131/145 |
| `json-compact` | 82.8% | 651 | 120/145 |
| `yaml` | 85.5% | 764 | 124/145 |
| `json-pretty` | 84.8% | 1,023 | 123/145 |
| `xml` | 82.8% | 1,073 | 120/145 |

##### Valid complete dataset (control)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `toon` | 100.0% | 735 | 5/5 |
| `json-compact` | 100.0% | 1,005 | 5/5 |
| `yaml` | 100.0% | 1,204 | 5/5 |
| `json-pretty` | 100.0% | 1,548 | 5/5 |
| `xml` | 40.0% | 1,761 | 2/5 |
| `csv` | 20.0% | 687 | 1/5 |

##### Array truncated: 3 rows removed from end

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 80.0% | 606 | 4/5 |
| `xml` | 80.0% | 1,849 | 4/5 |
| `toon` | 0.0% | 651 | 0/5 |
| `json-pretty` | 0.0% | 1,338 | 0/5 |
| `yaml` | 0.0% | 858 | 0/5 |
| `json-compact` | 0.0% | 719 | 0/5 |

##### Extra rows added beyond declared length

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 80.0% | 667 | 4/5 |
| `toon` | 60.0% | 818 | 3/5 |
| `xml` | 80.0% | 1,739 | 4/5 |
| `json-compact` | 60.0% | 1,132 | 3/5 |
| `yaml` | 60.0% | 1,364 | 3/5 |
| `json-pretty` | 40.0% | 1,758 | 2/5 |

##### Inconsistent field count (missing salary in row 10)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 80.0% | 679 | 4/5 |
| `json-compact` | 80.0% | 997 | 4/5 |
| `yaml` | 80.0% | 1,196 | 4/5 |
| `toon` | 80.0% | 1,220 | 4/5 |
| `json-pretty` | 80.0% | 1,535 | 4/5 |
| `xml` | 80.0% | 1,602 | 4/5 |

##### Missing required fields (no email in multiple rows)

| Format | Accuracy | Tokens | Correct/Total |
| ------ | -------- | ------ | ------------- |
| `csv` | 80.0% | 509 | 4/5 |
| `xml` | 80.0% | 1,702 | 4/5 |
| `toon` | 60.0% | 1,181 | 3/5 |
| `json-pretty` | 40.0% | 1,486 | 2/5 |
| `yaml` | 20.0% | 1,155 | 1/5 |
| `json-compact` | 0.0% | 960 | 0/5 |

#### Performance by Model

##### claude-haiku-4-5-20251001

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `toon` | 59.8% | 125/209 |
| `json-pretty` | 57.4% | 120/209 |
| `yaml` | 56.0% | 117/209 |
| `xml` | 55.5% | 116/209 |
| `json-compact` | 55.0% | 115/209 |
| `csv` | 50.5% | 55/109 |

##### gemini-3-flash-preview

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `xml` | 98.1% | 205/209 |
| `json-pretty` | 97.1% | 203/209 |
| `yaml` | 97.1% | 203/209 |
| `toon` | 96.7% | 202/209 |
| `json-compact` | 96.7% | 202/209 |
| `csv` | 96.3% | 105/109 |

##### gpt-5-nano

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `toon` | 90.9% | 190/209 |
| `json-compact` | 90.9% | 190/209 |
| `json-pretty` | 89.0% | 186/209 |
| `csv` | 89.0% | 97/109 |
| `yaml` | 87.1% | 182/209 |
| `xml` | 80.9% | 169/209 |

##### grok-4-1-fast-non-reasoning

| Format | Accuracy | Correct/Total |
| ------ | -------- | ------------- |
| `toon` | 58.4% | 122/209 |
| `yaml` | 57.9% | 121/209 |
| `json-pretty` | 56.5% | 118/209 |
| `xml` | 54.1% | 113/209 |
| `json-compact` | 52.2% | 109/209 |
| `csv` | 51.4% | 56/109 |

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

1. **Format conversion**: Each dataset is converted to all 6 formats (TOON, JSON, YAML, JSON compact, CSV, XML).
2. **Query LLM**: Each model receives formatted data + question in a prompt and extracts the answer.
3. **Validate deterministically**: Answers are validated using type-aware comparison (e.g., `50000` = `$50,000`, `Engineering` = `engineering`, `2025-01-01` = `January 1, 2025`) without requiring an LLM judge.

#### Models & Configuration

- **Models tested**: `claude-haiku-4-5-20251001`, `gemini-3-flash-preview`, `gpt-5-nano`, `grok-4-1-fast-non-reasoning`, `GigaChat-2`
- **Token counting**: Using provider-reported prompt tokens (`inputTokens`) from model responses
- **Temperature**: Not set (models use their defaults)
- **Total evaluations**: 209 questions × 6 formats × 5 models = 6,270 LLM calls
