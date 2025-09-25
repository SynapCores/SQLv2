# **Contributing to SQLv2**

Thank you for your interest in helping shape **SQLv2**, the open standard for **AI-native databases**.
This repository serves as the **official home of the SQLv2 specification**, where the community can propose new features, suggest improvements, and clarify details of the language.

SQLv2 unifies **traditional SQL, machine learning, vector search, generative AI, and multimedia support** into a single query language designed for the AI era.

We welcome contributions from:

* Database engineers
* Machine learning practitioners
* AI researchers
* Open-source developers
* Companies implementing SQLv2 in production

---

## **How to Participate**

There are four main ways you can contribute:

| Contribution Type           | Description                                                            | Where to Submit                                     |
| --------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------- |
| **Clarification Request**   | Ask questions or request clarification on ambiguous parts of the spec. | [GitHub Issues](../../issues)                       |
| **New Feature Proposal**    | Suggest new SQLv2 functions, data types, or extensions.                | [GitHub Issues](../../issues) → PR to `/proposals/` |
| **Implementation Feedback** | Share lessons learned from using SQLv2 in production or prototypes.    | [GitHub Issues](../../issues)                       |
| **Errata / Corrections**    | Fix typos, incorrect syntax, or small editorial updates to the spec.   | Pull Request directly to `/SQLv2Specs.md`           |

---

## **Getting Started**

### 1. Read the Core Specification

Start by reading the full SQLv2 spec in [SQLv2Specs.md](SQLv2Specs.md).
This will give you a solid understanding of:

* AI/ML function definitions
* Vector search syntax and operators
* Multimedia support
* AutoML and generative AI features
* Conformance levels (Core, Enhanced, Full)

---

### 2. Search Existing Issues

Before creating a new issue, **search the issue tracker** to see if someone has already:

* Asked the same clarification question.
* Proposed a similar feature.
* Reported the same feedback.

This helps reduce duplicates and keeps discussions organized.

---

### 3. Decide on the Type of Contribution

Each contribution should align with **one of the four main categories**:

1. Clarification
2. Proposal
3. Feedback
4. Errata

Use the appropriate **GitHub label** when opening an issue or PR.

---

## **Proposing a New Feature**

If you have an idea for a new SQLv2 feature, follow this process:

### **Step 1: Open a GitHub Issue**

* Label the issue as `proposal`.
* Provide a **summary of the feature**, its motivation, and potential use cases.
* Example:

  > *"I propose adding a `CLUSTER_EMBEDDINGS()` function to perform unsupervised clustering of vector data directly inside SQLv2."*

### **Step 2: Draft a Proposal Document**

Once there is agreement on the high-level idea:

* Create a new Markdown file under `/proposals/`.
* Follow the required template: `/proposals/TEMPLATE.md`.

**Proposal filename format:**

```
/proposals/0001-short-title.md
```

**Example:**

```
/proposals/0005-cluster-embeddings.md
```

---

### **Proposal Template**

Here’s what every proposal document must include:

````markdown
# Proposal: CLUSTER_EMBEDDINGS()

## Summary
Introduce a new SQLv2 function `CLUSTER_EMBEDDINGS()` for unsupervised clustering of vector data.

## Motivation
Explain why this feature is needed, what problem it solves, and how it fits SQLv2's mission.

## Proposed Syntax
```sql
SELECT CLUSTER_EMBEDDINGS(embedding_column, k=5)
FROM embeddings;
````

## Examples

Provide at least one end-to-end example query using the new feature.

## Backward Compatibility

Note any changes required to existing SQLv2 syntax or behavior.

## Alternatives Considered

List other approaches you considered and why they were rejected.

## Open Questions

Document unresolved questions for community discussion.

````

---

### **Step 3: Submit a Pull Request**
- Submit a PR adding the new file to `/proposals/`.
- Reference the original issue in the PR description.
- Include reviewers or stakeholders who should weigh in.

---

### **Step 4: Community Discussion**
- The proposal will be reviewed by the community and SQLv2 maintainers.
- Discussion happens in the PR comments.
- Proposals may go through multiple revisions before acceptance.

---

### **Step 5: Acceptance and Merge**
- Once approved, the proposal is merged into `/proposals/`.
- The spec maintainers decide when to integrate it into the core SQLv2 spec.

---

## **Labels and Workflow**

| Label | Purpose |
|-------|----------|
| `clarification` | Questions or requests for clarification about the spec. |
| `proposal` | New feature suggestions or extensions to SQLv2. |
| `implementation-feedback` | Insights from real-world implementations. |
| `errata` | Fixes for typos, syntax errors, or small corrections. |
| `discussion` | Open-ended conversation, brainstorming, or research topics. |

---

## **Style Guidelines**

To ensure consistency, follow these conventions:

1. **SQL Syntax Examples**
   - Use uppercase for SQL keywords:
     ```sql
     SELECT * FROM users WHERE age > 30;
     ```
   - Use lowercase for function parameters and table names.

2. **Markdown Structure**
   - Use `#` for top-level headings.
   - Use code blocks for SQL examples.
   - Keep line lengths under 100 characters for readability.

3. **Terminology**
   - Always refer to the standard as **SQLv2**, not "SQL V2" or "SQL2".
   - Use `[SQLv2 Extension]` annotations to mark non-standard features.

---

## **Governance Process**

The SQLv2 project uses an **open, transparent governance model**:
1. **Luis B. Mata** (creator of SQLv2) and the **SynapCores team** are the initial maintainers.
2. Decisions are made based on:
   - Technical merit
   - Community consensus
   - Alignment with SQLv2's mission
3. Quarterly roadmap reviews will be posted in `/proposals/roadmap.md`.

> **Goal:** SQLv2 will grow into a **vendor-neutral, community-driven standard**, much like Kubernetes or OpenAPI.

---

## **Code of Conduct**

By participating in this project, you agree to:
- Treat others with respect and professionalism.
- Keep discussions focused on technical merit.
- Avoid personal attacks, harassment, or discriminatory behavior.

Violations may result in removal from the project.

---

## **License**

The SQLv2 specification and all proposals are released under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/).

> This means you are free to copy, modify, and distribute the specification, provided attribution is given to the original author(s).

The **SynapCores database implementation** is proprietary and **not part of this repository**.

---

## **Helpful Links**

- 🌐 [SQLv2 Website](https://synapcores.com/sqlv2)  
- 📖 [Full Specification](SQLv2Specs.md)  
- 📝 [Issue Tracker](../../issues)  
- 🧪 [SynapCores Beta Signup](https://synapcores.com/early-access-beta)

---

## **Summary**
By contributing to SQLv2, you are helping to define the **next generation of data infrastructure** — one where AI, machine learning, and structured data converge in a single, unified language.

> **Join the discussion.**  
> Help build the standard that will power the future of AI-native applications.
````
