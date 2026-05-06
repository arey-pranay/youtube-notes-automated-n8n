# Building a Personal Wiki with LLMs

## TL;DR
A personal wiki can be built using LLMs by creating a structured knowledge base from raw documents. This approach involves an AI agent that reads, processes, and links information, allowing for efficient retrieval and synthesis of knowledge over time. The system typically consists of three layers: raw sources, the wiki itself (as markdown files), and a schema that guides the AI's operation.

## Key Takeaways
- The standard Retrieval Augmented Generation (RAG) approach for LLMs involves uploading documents, asking questions, and having the AI search and generate answers, but it lacks memory and compounding knowledge.
- Andrej Karpathy's LLM Wiki approach addresses this by having the AI build a structured, interlinked knowledge base from raw documents.
- This wiki is maintained by the AI, which reads sources, extracts key ideas, updates existing pages, creates new concept pages, links related ideas, and flags contradictions.
- The system has three layers: Raw Sources (immutable, read-only documents), The Wiki (AI-maintained markdown files), and The Schema (rules document guiding AI operation).
- Tools like Obsidian are useful for managing the wiki due to their graph view and markdown capabilities, and an AI coding agent is necessary for processing and writing files.

## Timestamped Sections
| Timestamp | Topic | What You Need to Know |
|---|---|---|
| 00:00 | Introduction to the Problem | Standard LLM use with documents lacks memory and knowledge compounding; each question starts from scratch. |
| 00:28 | Andrej Karpathy's LLM Wiki Idea | A pattern for building personal knowledge bases using LLMs, where the AI reads documents and builds a structured, interlinked wiki of markdown files. |
| 01:52 | The LLM Wiki Approach | The AI reads documents once, builds a structured, interlinked knowledge base of markdown files, and maintains it. |
| 02:07 | When You Add a New Source | The AI reads, extracts key ideas, updates existing pages, creates new concept pages, links related ideas, and flags contradictions. |
| 02:27 | Knowledge That Compounds | The wiki grows richer with each source, with cross-references, flagged contradictions, and synthesized information already built. |
| 02:41 | Karpathy's Analogy | Obsidian is the IDE, the LLM is the programmer, and the wiki is the codebase. |
| 02:58 | Three Simple Layers | 1. Raw Sources (original documents), 2. The Wiki (AI-created markdown pages), 3. The Schema (rules document for AI operation). |
| 03:01 | Layer 1: Raw Sources | Curated collection of source documents (PDFs, articles, etc.) that the AI reads but never modifies. This is the source of truth. |
| 03:16 | Layer 2: The Wiki | A folder of markdown files created and maintained by the AI, all interlinked and organized. Includes index, concept, and entity pages. |
| 03:32 | Layer 3: The Schema | A rules document (e.g., `CLAUDE.md`) that tells the AI how to structure, ingest, and maintain the wiki, including purpose, workflow rules, formatting standards, and question-answering behavior. |
| 03:53 | What You Need | Obsidian (free markdown editor with graph view), an AI Coding Agent (like Claude Code, Cursor) that can read/write files, and optionally the Obsidian Web Clipper. |
| 04:38 | Setting Up Obsidian | Create a new vault (folder) for your wiki. |
| 05:03 | Folder Structure | Create three folders: `raw` (for source documents), `wiki` (for AI-generated markdown pages), and `templates` (optional, for custom page formats). |
| 05:50 | The Schema File | Create a `CLAUDE.md` file in the root of your vault to define the AI's behavior and rules. |
| 06:15 | Populating the Wiki | Drag and drop source documents into the `raw` folder. |
| 08:01 | Using the Obsidian Web Clipper | Save web articles directly into your Obsidian vault as markdown files. |
| 09:19 | Ingesting a New Source | Use the AI agent (e.g., Claude Code) to ingest the new source by typing a command like "I just added a new source to the raw folder. Please read it and update the wiki." |
| 10:14 | Reviewing the Wiki Output | The AI will list the pages it created/updated and provide a summary of its actions. |
| 11:57 | Linting Your Wiki | Periodically audit the wiki for health issues like contradictions, stale claims, orphan pages, or missing concept pages. |
| 12:23 | Example Query | Ask the AI a question, e.g., "What neighborhood should I stay in if I want to be close to the best food and still near the major temples?" |
| 12:34 | AI's Response and Summary | The AI provides an answer based on the wiki, citing sources, and offers a summary of the wiki's health. |
| 13:00 | Use Cases | Student/Researcher (building knowledge from papers), Teacher (organizing curriculum), Business/Team (managing project docs), Curious Reader (tracking learning). |
| 13:41 | Honest Limitations | Best at personal scale (up to ~100 sources), requires curation of raw data, needs a coding agent, and AI can make mistakes. |

## Core Concepts Explained

### Retrieval Augmented Generation (RAG)
RAG is a technique used with Large Language Models (LLMs) to improve the accuracy and relevance of their responses by grounding them in external data. The process typically involves:
1.  **Retrieval:** When a user asks a question, the system searches a knowledge base (often a vector database containing embeddings of documents) for relevant information chunks.
2.  **Augmentation:** The retrieved information is combined with the original user query to form a more comprehensive prompt.
3.  **Generation:** The LLM uses this augmented prompt to generate a more informed and contextually relevant answer.
While effective for answering specific questions based on provided documents, standard RAG lacks a mechanism for building a persistent, interconnected knowledge base that grows and improves over time.

### LLM Wiki (Andrej Karpathy's Approach)
This approach transforms the way LLMs interact with personal knowledge bases. Instead of a stateless RAG system that processes documents for each query, the LLM Wiki aims to build a persistent, interconnected knowledge graph. Key aspects include:
*   **AI-driven Knowledge Curation:** The AI agent actively reads and processes source documents, creating structured markdown files that form a wiki.
*   **Interlinking and Synthesis:** The AI automatically creates links between related concepts and pages, synthesizing information from various sources.
*   **Memory and Compounding Knowledge:** Unlike standard RAG, the wiki retains information, allowing knowledge to build and compound over time, leading to richer and more nuanced answers to subsequent queries.
*   **Self-Improvement:** The system can identify and flag issues like contradictions or outdated information, allowing for continuous improvement.
*   **Schema-driven Operation:** A schema document guides the AI's behavior, defining how it should ingest, structure, and maintain the wiki.

### Obsidian
Obsidian is a free markdown editor and knowledge management application that functions as a "second brain." It excels at creating and linking notes, visualizing connections between them through a graph view, and organizing information in a flexible, user-controlled way. Its capabilities make it an ideal tool for managing the markdown files generated by an LLM Wiki.

### AI Coding Agent (e.g., Claude Code)
An AI coding agent is an LLM specifically designed to understand and execute code, interact with files, and perform complex tasks. For the LLM Wiki, such an agent is crucial for:
*   **Reading and Processing Sources:** Ingesting various document formats (PDFs, text files, web pages) from the `raw` folder.
*   **Writing and Maintaining Wiki Pages:** Creating new markdown files, updating existing ones, and establishing links between them based on the schema.
*   **Executing the Schema:** Following the rules defined in the schema document to manage the wiki's structure and content.
*   **Linting:** Auditing the wiki for consistency, identifying potential issues like contradictions or orphan pages.

## Interview Perspective
### Why This Matters
This approach fundamentally changes how individuals can leverage LLMs for personal knowledge management, moving beyond simple Q&A to building a dynamic, evolving knowledge base. It addresses the limitations of stateless LLM interactions by creating a system where knowledge compounds over time. This is highly relevant for roles requiring deep research, continuous learning, and efficient information synthesis.

### Concepts Likely to Be Asked
- **LLM Wiki vs. RAG:** How does Karpathy's wiki approach differ from standard RAG, and what are the benefits of the wiki model (compounding knowledge, AI-driven maintenance)?
- **The Three Layers:** Explain the purpose and function of Raw Sources, The Wiki, and The Schema.
- **Role of Obsidian:** Why is Obsidian a suitable tool for this, and what features are particularly important (graph view, markdown)?
- **AI Agent's Role:** What specific tasks does the AI agent perform in this workflow (ingestion, linking, linting)?
- **Limitations:** What are the key limitations of this approach (scale, data quality, AI errors)?

### At a Glance Checkpoints
- [ ] Can you explain the difference between RAG and the LLM Wiki approach?
- [ ] Can you list the three layers of the LLM Wiki and their functions?
- [ ] Can you describe the role of the `CLAUDE.md` schema file?
- [ ] Can you give an example of how an AI agent might "lint" a wiki?

## Quick Reference
- **LLM Wiki Layers:**
    1.  **Raw Sources:** Immutable, read-only original documents.
    2.  **The Wiki:** AI-maintained markdown files, interlinked and organized.
    3.  **The Schema:** Rules document (`CLAUDE.md`) guiding AI operations.
- **Key AI Tasks:** Read sources, extract ideas, create/update pages, link concepts, flag contradictions.
- **Linting Checks:** Format compliance, broken links, orphan pages, missing concept pages, stale claims.
- **Tools:** Obsidian (for management), AI Coding Agent (for processing).

**Metadata**
**Category:** General AI / Knowledge Management
**Tags:** `LLM`, `AI`, `knowledge management`, `wiki`, `Andrej Karpathy`, `Obsidian`, `RAG`, `Claude Code`
**Interview Relevance:** Must Know (for understanding advanced LLM applications)
**Difficulty:** Intermediate
**Est. Read Time:** 5 min

---

**Source:** https://www.youtube.com/watch?v=iXd0t60YmMw  
**Saved:** 2026-05-06T16:12:43.334Z
**AI Source:** gemini
