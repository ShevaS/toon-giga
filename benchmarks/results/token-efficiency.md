#### Mixed-Structure Track

Datasets with nested or semi-uniform structures. CSV excluded as it cannot properly represent these structures.

```
🛒 E-commerce orders with nested structures  ┊  Tabular: 33%
   │
   TOON                █████████████░░░░░░░     7,116 tokens
   ├─ vs JSON          (−33.3%)                10,667 tokens
   ├─ vs JSON compact  (+5.3%)                  6,757 tokens
   ├─ vs YAML          (−12.1%)                 8,093 tokens
   └─ vs XML           (−39.9%)                11,833 tokens

🧾 Semi-uniform event logs  ┊  Tabular: 50%
   │
   TOON                █████████████████░░░     5,459 tokens
   ├─ vs JSON          (−17.0%)                 6,581 tokens
   ├─ vs JSON compact  (+19.4%)                 4,571 tokens
   ├─ vs YAML          (−0.2%)                  5,471 tokens
   └─ vs XML           (−26.0%)                 7,382 tokens

🧩 Deeply nested configuration  ┊  Tabular: 0%
   │
   TOON                ███████████████░░░░░       752 tokens
   ├─ vs JSON          (−26.5%)                 1,023 tokens
   ├─ vs JSON compact  (+15.5%)                   651 tokens
   ├─ vs YAML          (−1.6%)                    764 tokens
   └─ vs XML           (−29.9%)                 1,073 tokens

──────────────────────────────────── Total ────────────────────────────────────
   TOON                ███████████████░░░░░    13,327 tokens
   ├─ vs JSON          (−27.1%)                18,271 tokens
   ├─ vs JSON compact  (+11.3%)                11,979 tokens
   ├─ vs YAML          (−7.0%)                 14,328 tokens
   └─ vs XML           (−34.3%)                20,288 tokens
```

#### Flat-Only Track

Datasets with flat tabular structures where CSV is applicable.

```
👥 Uniform employee records  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░     2,465 tokens
   TOON                ████████████████████     2,591 tokens   (+5.1% vs CSV)
   ├─ vs JSON          (−58.4%)                 6,230 tokens
   ├─ vs JSON compact  (−33.0%)                 3,865 tokens
   ├─ vs YAML          (−45.2%)                 4,727 tokens
   └─ vs XML           (−63.3%)                 7,051 tokens

📈 Time-series analytics data  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░     1,608 tokens
   TOON                ████████████████████     1,686 tokens   (+4.9% vs CSV)
   ├─ vs JSON          (−53.6%)                 3,630 tokens
   ├─ vs JSON compact  (−27.7%)                 2,331 tokens
   ├─ vs YAML          (−43.0%)                 2,959 tokens
   └─ vs XML           (−60.2%)                 4,241 tokens

⭐ Top 100 GitHub repositories  ┊  Tabular: 100%
   │
   CSV                 ████████████████████     8,530 tokens
   TOON                ████████████████████     8,620 tokens   (+1.1% vs CSV)
   ├─ vs JSON          (−40.8%)                14,569 tokens
   ├─ vs JSON compact  (−22.1%)                11,061 tokens
   ├─ vs YAML          (−31.3%)                12,542 tokens
   └─ vs XML           (−46.8%)                16,210 tokens

──────────────────────────────────── Total ────────────────────────────────────
   CSV                 ████████████████████    12,603 tokens
   TOON                ████████████████████    12,897 tokens   (+2.3% vs CSV)
   ├─ vs JSON          (−47.2%)                24,429 tokens
   ├─ vs JSON compact  (−25.3%)                17,257 tokens
   ├─ vs YAML          (−36.2%)                20,228 tokens
   └─ vs XML           (−53.1%)                27,502 tokens
```

<details>
<summary><strong>Show detailed examples</strong></summary>

#### 📈 Time-series analytics data

**Savings:** 1,944 tokens (53.6% reduction vs JSON)

**JSON** (3,630 tokens):

```json
{
  "metrics": [
    {
      "date": "2025-01-01",
      "views": 6138,
      "clicks": 174,
      "conversions": 12,
      "revenue": 2712.49,
      "bounceRate": 0.35
    },
    {
      "date": "2025-01-02",
      "views": 4616,
      "clicks": 274,
      "conversions": 34,
      "revenue": 9156.29,
      "bounceRate": 0.56
    },
    {
      "date": "2025-01-03",
      "views": 4460,
      "clicks": 143,
      "conversions": 8,
      "revenue": 1317.98,
      "bounceRate": 0.59
    },
    {
      "date": "2025-01-04",
      "views": 4740,
      "clicks": 125,
      "conversions": 13,
      "revenue": 2934.77,
      "bounceRate": 0.37
    },
    {
      "date": "2025-01-05",
      "views": 6428,
      "clicks": 369,
      "conversions": 19,
      "revenue": 1317.24,
      "bounceRate": 0.3
    }
  ]
}
```

**TOON** (1,686 tokens):

```
metrics[5]{date,views,clicks,conversions,revenue,bounceRate}:
  2025-01-01,6138,174,12,2712.49,0.35
  2025-01-02,4616,274,34,9156.29,0.56
  2025-01-03,4460,143,8,1317.98,0.59
  2025-01-04,4740,125,13,2934.77,0.37
  2025-01-05,6428,369,19,1317.24,0.3
```

---

#### ⭐ Top 100 GitHub repositories

**Savings:** 5,949 tokens (40.8% reduction vs JSON)

**JSON** (14,569 tokens):

```json
{
  "repositories": [
    {
      "id": 28457823,
      "name": "freeCodeCamp",
      "repo": "freeCodeCamp/freeCodeCamp",
      "description": "freeCodeCamp.org's open-source codebase and curriculum. Learn math, programming,…",
      "createdAt": "2014-12-24T17:49:19Z",
      "updatedAt": "2025-10-28T11:58:08Z",
      "pushedAt": "2025-10-28T10:17:16Z",
      "stars": 430886,
      "watchers": 8583,
      "forks": 42146,
      "defaultBranch": "main"
    },
    {
      "id": 132750724,
      "name": "build-your-own-x",
      "repo": "codecrafters-io/build-your-own-x",
      "description": "Master programming by recreating your favorite technologies from scratch.",
      "createdAt": "2018-05-09T12:03:18Z",
      "updatedAt": "2025-10-28T12:37:11Z",
      "pushedAt": "2025-10-10T18:45:01Z",
      "stars": 430877,
      "watchers": 6332,
      "forks": 40453,
      "defaultBranch": "master"
    },
    {
      "id": 21737465,
      "name": "awesome",
      "repo": "sindresorhus/awesome",
      "description": "😎 Awesome lists about all kinds of interesting topics",
      "createdAt": "2014-07-11T13:42:37Z",
      "updatedAt": "2025-10-28T12:40:21Z",
      "pushedAt": "2025-10-27T17:57:31Z",
      "stars": 410052,
      "watchers": 8017,
      "forks": 32029,
      "defaultBranch": "main"
    }
  ]
}
```

**TOON** (8,620 tokens):

```
repositories[3]{id,name,repo,description,createdAt,updatedAt,pushedAt,stars,watchers,forks,defaultBranch}:
  28457823,freeCodeCamp,freeCodeCamp/freeCodeCamp,"freeCodeCamp.org's open-source codebase and curriculum. Learn math, programming,…","2014-12-24T17:49:19Z","2025-10-28T11:58:08Z","2025-10-28T10:17:16Z",430886,8583,42146,main
  132750724,build-your-own-x,codecrafters-io/build-your-own-x,Master programming by recreating your favorite technologies from scratch.,"2018-05-09T12:03:18Z","2025-10-28T12:37:11Z","2025-10-10T18:45:01Z",430877,6332,40453,master
  21737465,awesome,sindresorhus/awesome,😎 Awesome lists about all kinds of interesting topics,"2014-07-11T13:42:37Z","2025-10-28T12:40:21Z","2025-10-27T17:57:31Z",410052,8017,32029,main
```

</details>
