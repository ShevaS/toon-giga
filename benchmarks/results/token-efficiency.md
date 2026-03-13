#### Mixed-Structure Track

Datasets with nested or semi-uniform structures. CSV excluded as it cannot properly represent these structures.

```
🛒 E-commerce orders with nested structures  ┊  Tabular: 33%
   │
   TOON                █████████████░░░░░░░     8,181 tokens
   ├─ vs JSON          (−34.5%)                12,483 tokens
   ├─ vs JSON compact  (+5.2%)                  7,780 tokens
   ├─ vs YAML          (−12.7%)                 9,368 tokens
   └─ vs XML           (−41.2%)                13,916 tokens

🧾 Semi-uniform event logs  ┊  Tabular: 50%
   │
   TOON                █████████████████░░░     6,312 tokens
   ├─ vs JSON          (−16.8%)                 7,584 tokens
   ├─ vs JSON compact  (+20.0%)                 5,259 tokens
   ├─ vs YAML          (+0.3%)                  6,295 tokens
   └─ vs XML           (−25.7%)                 8,496 tokens

🧩 Deeply nested configuration  ┊  Tabular: 0%
   │
   TOON                ███████████████░░░░░       868 tokens
   ├─ vs JSON          (−26.4%)                 1,180 tokens
   ├─ vs JSON compact  (+17.0%)                   742 tokens
   ├─ vs YAML          (−1.4%)                    880 tokens
   └─ vs XML           (−30.7%)                 1,252 tokens

──────────────────────────────────── Total ────────────────────────────────────
   TOON                ██████████████░░░░░░    15,361 tokens
   ├─ vs JSON          (−27.7%)                21,247 tokens
   ├─ vs JSON compact  (+11.5%)                13,781 tokens
   ├─ vs YAML          (−7.1%)                 16,543 tokens
   └─ vs XML           (−35.1%)                23,664 tokens
```

#### Flat-Only Track

Datasets with flat tabular structures where CSV is applicable.

```
👥 Uniform employee records  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░     2,804 tokens
   TOON                ████████████████████     2,945 tokens   (+5.0% vs CSV)
   ├─ vs JSON          (−59.7%)                 7,301 tokens
   ├─ vs JSON compact  (−33.6%)                 4,436 tokens
   ├─ vs YAML          (−46.5%)                 5,500 tokens
   └─ vs XML           (−64.8%)                 8,363 tokens

📈 Time-series analytics data  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░     1,769 tokens
   TOON                ████████████████████     1,854 tokens   (+4.8% vs CSV)
   ├─ vs JSON          (−55.4%)                 4,161 tokens
   ├─ vs JSON compact  (−29.7%)                 2,637 tokens
   ├─ vs YAML          (−44.3%)                 3,327 tokens
   └─ vs XML           (−61.7%)                 4,836 tokens

⭐ Top 100 GitHub repositories  ┊  Tabular: 100%
   │
   CSV                 ████████████████████     9,691 tokens
   TOON                ████████████████████     9,900 tokens   (+2.2% vs CSV)
   ├─ vs JSON          (−41.8%)                17,021 tokens
   ├─ vs JSON compact  (−22.2%)                12,717 tokens
   ├─ vs YAML          (−32.0%)                14,556 tokens
   └─ vs XML           (−48.0%)                19,055 tokens

──────────────────────────────────── Total ────────────────────────────────────
   CSV                 ███████████████████░    14,264 tokens
   TOON                ████████████████████    14,699 tokens   (+3.0% vs CSV)
   ├─ vs JSON          (−48.4%)                28,483 tokens
   ├─ vs JSON compact  (−25.7%)                19,790 tokens
   ├─ vs YAML          (−37.1%)                23,383 tokens
   └─ vs XML           (−54.4%)                32,254 tokens
```

<details>
<summary><strong>Show detailed examples</strong></summary>

#### 📈 Time-series analytics data

**Savings:** 2,307 tokens (55.4% reduction vs JSON)

**JSON** (4,161 tokens):

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

**TOON** (1,854 tokens):

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

**Savings:** 7,121 tokens (41.8% reduction vs JSON)

**JSON** (17,021 tokens):

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

**TOON** (9,900 tokens):

```
repositories[3]{id,name,repo,description,createdAt,updatedAt,pushedAt,stars,watchers,forks,defaultBranch}:
  28457823,freeCodeCamp,freeCodeCamp/freeCodeCamp,"freeCodeCamp.org's open-source codebase and curriculum. Learn math, programming,…","2014-12-24T17:49:19Z","2025-10-28T11:58:08Z","2025-10-28T10:17:16Z",430886,8583,42146,main
  132750724,build-your-own-x,codecrafters-io/build-your-own-x,Master programming by recreating your favorite technologies from scratch.,"2018-05-09T12:03:18Z","2025-10-28T12:37:11Z","2025-10-10T18:45:01Z",430877,6332,40453,master
  21737465,awesome,sindresorhus/awesome,😎 Awesome lists about all kinds of interesting topics,"2014-07-11T13:42:37Z","2025-10-28T12:40:21Z","2025-10-27T17:57:31Z",410052,8017,32029,main
```

</details>
