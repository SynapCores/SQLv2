# **SQLv2 – The Open Standard for AI-Native Databases**

> **SQLv2 is a next-generation standard** that unifies **traditional SQL, machine learning, vector search, generative AI, and multimedia support** into a single, cohesive query language.
>
> Built for the AI era, SQLv2 eliminates the complexity of stitching together multiple systems — relational databases, vector databases, ETL pipelines, and external ML services — by bringing everything natively inside SQL.

---

## **Why SQLv2?**

Modern AI applications require developers to maintain **disconnected data stacks**:

* A relational database for structured data
* A separate vector database for embeddings
* External machine learning APIs
* ETL pipelines to move data between systems
* Ah! And multiple GenAI endpoints

This leads to:

* **Data silos** and inconsistent state
* **High infrastructure costs**
* **Latency and performance bottlenecks**
* **Slower development cycles**

SQLv2 solves these problems by introducing **AI-native primitives directly into the SQL language**.

---

## **Core Innovations**

SQLv2 builds on ANSI SQL while adding new constructs designed for modern AI workloads:

| Category                         | SQLv2 Features                                                                                           |
| -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **AI/ML Functions**              | `PREDICT()`, `CLASSIFY()`, `GENERATE()`, `SENTIMENT()`                                                   |
| **Vector Search**                | Native vector type (`VECTOR(n)`), similarity operators `<=>` and `<->`, functions like `VECTOR_SEARCH()` |
| **Generative AI**                | `GENERATE()` for text synthesis, summarization, and content generation directly in SQL                   |
| **Multimedia Support**           | First-class data types: `IMAGE`, `VIDEO`, `AUDIO`, `PDF`                                                 |
| **AutoML**                       | `CREATE EXPERIMENT`, `DEPLOY MODEL`, `PREDICT ... USING ...`                                             |
| **Zero-Copy & GPU Acceleration** | Built-in performance for ML and vector operations                                                        |

---

## **Example Queries**

### 1. Run Machine Learning Inference

```sql
SELECT user_id, 
       PREDICT(purchase_likelihood)
FROM users;
```

---

### 2. Generative AI Inside SQL

```sql
SELECT product_id,
       GENERATE('Write a 2-sentence description for ' || product_name)
FROM products;
```

---

### 3. Vector Similarity Search

```sql
SELECT doc_id, content
FROM documents
ORDER BY embedding <=> EMBED('healthy recipes')
LIMIT 5;
```

---

### 4. Multimedia + AI in a Single Query

```sql
SELECT video_id,
       TRANSCRIBE(video_data) AS transcript,
       SUMMARIZE(TRANSCRIBE(video_data), 100) AS summary
FROM videos
WHERE JSON_EXTRACT(DIMENSIONS(video_data), '$.width') >= 1920;
```

---

## **Goals of This Repository**

This repository is the **official home of the SQLv2 specification**.
It serves as a **living document and collaboration hub** for the SQLv2 community.

* 📄 **SQLv2 Specification** – The full technical definition of the language.
* 💬 **Community Proposals** – Suggest new features or changes to the standard.
* 🗂 **Reference Examples** – Example SQLv2 queries for developers and implementers.
* 📈 **Version History** – Transparent changelog for all revisions of the spec.

---

## **Repository Structure**

```
sqlv2/
├── README.md          # Introduction and overview (this file)
├── SQLv2Specs.md      # Full technical specification
├── proposals/         # Community-driven feature proposals
│   └── TEMPLATE.md    # Template for new proposals
├── examples/          # Example SQLv2 queries
│   ├── ai_queries.sql
│   ├── vector_search.sql
│   └── multimedia.sql
├── CONTRIBUTING.md    # Guidelines for proposing changes
└── CHANGELOG.md       # Version history and spec updates
```

---

## **How to Contribute**

We welcome contributions from database engineers, ML practitioners, and anyone interested in shaping the future of AI-native data systems.

There are three main ways to participate:

| Contribution Type           | Description                                                  | Where                                         |
| --------------------------- | ------------------------------------------------------------ | --------------------------------------------- |
| **Clarification Request**   | Ask questions about parts of the spec that need more detail. | GitHub Issues                                 |
| **New Feature Proposal**    | Suggest new functions, data types, or language extensions.   | GitHub Issues → Pull Request to `/proposals/` |
| **Implementation Feedback** | Share insights from real-world usage of SQLv2.               | GitHub Issues                                 |

See our [CONTRIBUTING.md](CONTRIBUTING.md) for step-by-step instructions.

---

## **Versioning**

* SQLv2 follows a **semantic versioning** approach:

  * **v2.0.0** – Initial stable release
  * **v2.1.0** – New features added
  * **v2.2.0** – Improvements and clarifications
* All changes are documented in [CHANGELOG.md](CHANGELOG.md).

---

## **Governance Model**

* SQLv2 was initially developed by **Luis B. Mata** and the **SynapCores team**.
* SynapCores is the **first implementation**, but SQLv2 is intended to be **open and vendor-neutral**.
* Decisions about the spec are made openly, with feedback from the community via:

  * GitHub Issues
  * Pull Requests
  * Quarterly roadmap reviews

---

## **Roadmap**

The following milestones are planned for SQLv2 evolution:

| Milestone                           | Status           |
| ----------------------------------- | ---------------- |
| Core spec publication               | ✅ Completed      |
| Public GitHub repo launch           | ✅ Completed      |
| Beta implementation via SynapCores  | 🚧 In progress   |
| RFC submission to IETF              | Planned          |
| Multimedia deep learning extensions | Planned          |
| ISO SQL committee engagement        | Future milestone |

---

## **License**

The SQLv2 specification is **free to use and implement** under the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/).

> You are free to copy, modify, and distribute the specification, provided attribution is given to the original author(s).

The **SynapCores implementation** of SQLv2 is proprietary and separate from this specification.

---

## **Links**

* 🌐 [Official Website](https://synapcores.com/sqlv2)
* 📖 [Full Specification](SQLv2Specs.md)
* 📝 [Contributing Guide](CONTRIBUTING.md)
* 🧪 [Beta Signup](https://synapcores.com/early-access-beta)

---

## **Acknowledgments**

SQLv2 was created by **Luis B. Mata** with the support of the SynapCores engineering team and early design partners.
Special thanks to the developer community for shaping the future of this open standard.

---

## **Next Steps**

* Clone this repository and read the [SQLv2Specs.md](SQLv2Specs.md) file.
* Try the example queries in `/examples/`.
* Submit proposals for new features under `/proposals/`.
* Sign up for the [SynapCores beta](https://synapcores.com/early-access-beta) to experience the first implementation.

---

## **Summary**

SQLv2 is more than a database extension — it’s the **unified query language for the AI era**.
By bringing structured data, AI, and multimedia together, SQLv2 aims to do for **AI-powered applications** what SQL did for relational data in the 1970s.

> **Join us in shaping the future of data.**
> Start here: [github.com/synapcores/sqlv2](https://github.com/synapcores/sqlv2)

