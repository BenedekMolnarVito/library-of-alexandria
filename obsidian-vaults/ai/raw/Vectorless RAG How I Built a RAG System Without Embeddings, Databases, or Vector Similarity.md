---
title: "Vectorless RAG: How I Built a RAG System Without Embeddings, Databases, or Vector Similarity"
source: "https://pub.towardsai.net/vectorless-rag-how-i-built-a-rag-system-without-embeddings-databases-or-vector-similarity-efccf21e42ff"
author:
  - "[[Alpha Iterations]]"
published: 2026-04-04
created: 2026-04-18
description: "Vectorless RAG - End to End Agentic AI Project (Code Included). A journey from “vector similarity ≠ relevance” to building a reasoning-based RAG system that actually understands documents"
tags:
  - "clippings"
---
## [Towards AI](https://pub.towardsai.net/?source=post_page---publication_nav-98111c9905da-efccf21e42ff---------------------------------------)

[![Towards AI](https://miro.medium.com/v2/resize:fill:48:48/1*JyIThO-cLjlChQLb6kSlVQ.png)](https://pub.towardsai.net/?source=post_page---post_publication_sidebar-98111c9905da-efccf21e42ff---------------------------------------)

We build Enterprise AI. We teach what we learn. Join 100K+ AI practitioners on Towards AI Academy. Free: 6-day Agentic AI Engineering Email Guide: [https://email-course.towardsai.net/](https://email-course.towardsai.net/)

## A journey from “vector similarity ≠ relevance” to building a reasoning-based RAG system that actually understands documents (Code Included)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*tleohhao1xjgtdHa)

Photo by Becca Tapert on Unsplash

Non-members [read here for free.](https://pub.towardsai.net/vectorless-rag-how-i-built-a-rag-system-without-embeddings-databases-or-vector-similarity-efccf21e42ff?sk=d94c796b7e5e875b3b50ac559a91ad3a)

## Introduction

Retrieval-Augmented Generation (RAG) has become a foundational pattern for building AI systems that can answer questions over private data. Traditionally, RAG relies on **vector embeddings** to retrieve relevant chunks of text, which are then passed to a language model for generation.

However, as systems scale and use cases become more complex, a new paradigm is emerging: **Vectorless RAG**, also known as **reasoning-based retrieval**.

Instead of relying on embeddings and similarity search, vectorless RAG **navigates information like a human would** — following structure, reasoning step-by-step, and dynamically deciding where to look next.

This article explores:

- What vectorless RAG is
- How it compares to traditional RAG
- Its advantages and trade-offs
- When you should (and shouldn’t) use it

## Traditional RAG: The Baseline

Traditional RAG works in three main steps:

1. **Chunking**: Break documents into small pieces
2. **Embedding**: Convert each chunk into a vector
3. **Retrieval**: Use similarity search (e.g., cosine similarity) to find relevant chunks

Then:

- Top-k chunks are sent to an LLM
- The LLM generates an answer

**Example Flow:**

```c
Query → Embedding → Vector DB → Top-k Chunks → LLM → Answer
```

There have been variations of RAG systems like ReRanking, Agentic RAG, Hybrid RAG etc.

Traditional RAG itself has not remained static. Over time, several variations have emerged to address its limitations — particularly around retrieval quality, reasoning depth, and context relevance.

**1\. Re-ranking RAG** improves retrieval precision by introducing a second stage that reorders initially retrieved documents using LLM. Instead of trusting raw similarity scores, the system asks: *“Which of these results are actually most relevant to the query?”*

**2\. Hybrid RAG** combines multiple retrieval strategies — typically dense vector search with keyword-based methods like BM25. This helps overcome a key weakness of embeddings: they can miss exact matches (e.g., IDs, names, or rare terms), while keyword search alone lacks semantic understanding.

**3\. Agentic RAG** introduces iterative reasoning into the pipeline. Instead of retrieving once, the system can:

- Break down a query into sub-questions
- Perform multiple retrieval steps
- Decide dynamically what information to fetch next.

This begins to blur the line between retrieval and reasoning, making the system more flexible but also more complex.

## Limitations of Traditional RAG (A More Nuanced View)

Traditional RAG is highly effective for many use cases, especially when retrieving semantically similar content at scale. However, its limitations are often misunderstood. Rather than being fundamentally broken, most issues arise from **how retrieval is performed and what it optimizes for**.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*5mcV83IfseP80IRHaobLUw.png)

Traditional RAG (Image by Author )

### 1\. Shallow Retrieval (Core Limitation)

The most fundamental limitation of traditional RAG is that retrieval is based on **semantic similarity**, not **task relevance or reasoning**.

Vector search answers the question:

> *“What text looks similar to the query?”*

But many real-world queries require:

- causal understanding
- multi-step reasoning
- synthesizing information across sections

As a result, the system may retrieve text that is *topically related* but not *actually useful* for answering the question.

This is an inherent limitation of embedding-based retrieval and cannot be fully solved by better chunking or indexing alone.

### 2\. Context Fragmentation (Mitigatable)

Documents are typically split into chunks before embedding. This can lead to situations where:

- Important context is split across multiple chunks
- Retrieved chunks lack sufficient surrounding information
- Relationships between sections are lost

However, this is largely an **engineering problem**, not a fundamental limitation. Techniques such as:

- overlapping chunks
- sliding windows
- re-ranking
- multi-hop retrieval

can significantly reduce fragmentation.

### 3\. Loss of Structure (Implementation-Dependent)

In naive implementations, documents are flattened into chunks, losing their original structure (chapters, sections, subsections).

However, modern RAG systems often preserve structure using:

- metadata (e.g., section titles, hierarchy)
- hierarchical chunking
- parent-child retrieval strategies

When implemented properly, traditional RAG can retain much of the document’s structure. Therefore, this is not an inherent limitation, but rather a consequence of simplistic pipelines.

### 4\. Preprocessing Overhead (Architectural Trade-off)

Traditional RAG requires:

- embedding generation
- vector database storage
- indexing and maintenance

While this introduces upfront cost and system complexity, it enables:

- fast retrieval
- low-latency queries
- scalable performance

This is best understood as a **trade-off in cost distribution**:

- higher upfront cost
- lower per-query cost

rather than a true limitation.

## Key Takeaway

Among all commonly cited issues, the only fundamental limitation is:

> *Traditional RAG retrieves based on similarity, not reasoning.*

Everything else — structure, fragmentation, and cost — can be addressed with better system design.

This distinction is important when comparing traditional RAG with newer approaches like vectorless (reasoning-based) retrieval, which aim to shift retrieval from a similarity problem to a decision-making process.

## Vectorless RAG: The Core Idea

If the main limitation of traditional RAG is that retrieval lacks reasoning, the natural question becomes:

> What if retrieval itself could reason?

To understand this, consider how a human analyst approaches a document.

They don’t scan thousands of chunks or rely on similarity. Instead, they:

- Look at the **table of contents**
- Understand the **structure of the document**
- Reason: *“If I need information about X, it’s likely in section Y”*
- Navigate directly to that section
- Read the **full context**
- Synthesize an answer

This process is **structured, intentional, and iterative**. Retrieval is not a one-shot operation — it’s guided by reasoning at every step.

Vectorless RAG is built on this exact idea.

Instead of retrieving based on similarity, it treats retrieval as a **decision-making process**. The system learns to:

- interpret document structure
- decide where to navigate next
- progressively refine its search
- and only retrieve content when it has enough context

In other words, it shifts retrieval from:

> “What looks similar?”

to:

> “Where should I go next?”

This is the fundamental shift that defines Vectorless RAG.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*31NKAOc-0bzhIaTXNXsRXw.png)

Vectorless RAG (Image by Author )

## How It Works in Practice

Vectorless RAG replaces similarity-based retrieval with a structured, reasoning-driven process. In practice, this involves two phases: a one-time document transformation, followed by a reasoning-based retrieval loop at query time.

### Step 1: Build a Document Tree (One-time Setup)

Before any queries are processed, the document is converted into a hierarchical structure.

Conceptually, this is similar to how a book is organized:

- title
- chapters
- sections
- subsections

Using a preprocessing step (e.g., PageIndex), the document is parsed into a tree where each node contains:

- a title
- a short summary
- page boundaries
- optionally, the full text

This produces a structure like:

```c
{
  "title": "Google Bigtable Paper",
  "node_id": "0001",
  "summary": "Introduction to Bigtable architecture",
  "nodes": [
    {
      "title": "Data Model",
      "node_id": "0002",
      "summary": "Rows, columns, timestamps",
      "nodes": [...]
    },
    {
      "title": "Architecture",
      "node_id": "0003",
      "summary": "Master, tablet servers, Chubby",
      "nodes": [...]
    }
  ]
}
```

This tree acts as a **compact, structured representation of the document**, enabling navigation without scanning the full text.

### Step 2: Reasoning Over Structure

At query time, the system does not immediately retrieve text. Instead, it first reasons over the document structure.

The process is:

1\. Provide the LLM with:

- the query
- the tree structure (titles + summaries only)

2\. Ask the model:

> “Which sections are most likely to contain the answer?”

3\. The model then selects relevant nodes based on:

- semantic understanding of the query
- high-level document structure
- relationships between sections

For example, for a question about *Chubby in Bigtable*, the model may select:

- “Architecture”
- “Consistency & Synchronization”

This step replaces vector similarity with **explicit decision-making**.

### Step 3: Retrieve Full Context

Once relevant sections are identified:

- The system retrieves the **full text** of those nodes
- Optionally includes child sections for completeness
- Combines them into a structured context

This ensures that retrieval operates at the **section level**, rather than arbitrary chunks.

### Step 4: Generate the Answer

Finally, the retrieved context is passed to the LLM to generate an answer.

The model is instructed to:

- use only the provided context
- synthesize information across sections
- optionally cite sources

This step is similar to traditional RAG — the key difference lies in how the context was selected.

## Comparison with Vector RAG (Practical View)

To illustrate the difference, consider the question:

> *“How does Bigtable handle consistency across replicas?”*

### Traditional RAG

- Retrieves chunks based on similarity to terms like “consistency”, “replication”
- May return partially relevant chunks
- Requires the model to filter noise during generation

### Vectorless RAG

- First identifies the *relevant section* (e.g., “Consistency & Synchronization”)
- Retrieves the full section
- Provides more coherent and focused context

## Where This Helps — and Where It Doesn’t

Vectorless RAG can be advantageous when:

- Documents have **clear structure**
- Questions require **navigating sections**
- Context is spread across related subsections

However, it is not universally better.

## Trade-offs

- **Higher latency**: multiple LLM calls per query
- **Higher per-query cost** compared to vector lookup
- **Dependent on structure quality**: weak or noisy structure reduces effectiveness
- **Less suitable for large, unstructured corpora**

## Cost and Performance Considerations

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*z7C-gHMpI70PU-uTCStsRg.png)

Comparison of Traditional RAG vs Vectorless RAG

## Key Takeaway

Vectorless RAG does not replace traditional RAG — it shifts the retrieval strategy.

- Traditional RAG: efficient, similarity-driven, scalable
- Vectorless RAG: structured, reasoning-driven, more selective

The choice between them depends on the problem:

- **Search at scale → Vector RAG**
- **Reasoning over structured documents → Vectorless RAG**

## Implementation

We’ll now build a basic vectorless RAG system, starting with document structuring and retrieval.  
Complete end to end code is found [here](https://github.com/alphaiterations/agentic-ai-usecases/tree/main/advanced/vectorless-rag):

We will use a research paper about [Bigtable published by Google](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf) as our input document.

## Setup:

1. Create and Activate Virtual Environment

For macOS/Linux:

```c
python3 -m venv .venv
source .venv/bin/activate
```

For Windows (Command Prompt):\*\*

```c
python -m venv .venv
.venv\Scripts\activate
```

2\. Install dependencies from `requirements.txt`

```c
# Core LLM and Agentic Framework
openai==2.30.0              # OpenAI API client
langgraph==1.1.4            # LangGraph for building state graphs and agents
pydantic==2.12.5            # Data validation
# PDF Processing
PyMuPDF==1.27.2.2           # PDF parsing/manipulation (fitz)
pymupdf4llm                  # Layout-aware PDF to markdown conversion
# Utilities
python-dotenv==1.2.2        # Environment variable management (.env files)
```

3\. Create `.env` file with your `OPENAI_API_KEY`

Let’s move ahead.

## Step 1: Tree Generation

The first step in a vectorless retrieval pipeline is to convert the document into a **structured, navigable representation**. Instead of treating the document as flat text, we build a **hierarchical tree** that captures its logical organization.

For this, we use `**pymupdf4llm**`, a lightweight library built on top of PyMuPDF. It provides layout-aware PDF parsing and can extract content as clean markdown while preserving headings and structure.

There are also ready-made solutions like [PageIndex](https://github.com/VectifyAI/PageIndex) that can generate structured document representations out of the box. However, in this implementation, we build our own tree to keep full control over parsing, hierarchy, and metadata.

### Core Idea

We construct a tree where:

- Each node represents a section (chapter, subsection, etc.)
- Nodes are derived from markdown headers (`#`, `##`, `###`, …)
- Parent-child relationships reflect document structure
- Each node is mapped to page ranges and content

### Parsing Strategy

The implementation follows three key steps:

1. **Extract structured markdown**  
	Using `pymupdf4llm.to_markdown()` to preserve layout and headings.
2. **Build hierarchy from headers**  
	Markdown headers are parsed into levels, and a stack-based approach is used to construct the tree.
3. **Align content with pages**  
	Page-level chunks are used to refine page boundaries and ensure each node maps accurately to the original document.

Additionally:

- Headings are classified (numbered, roman, unnumbered, etc.)
- Content is summarized at higher-level nodes
- Leaf nodes retain the most detailed content

The result is a **DocumentTree** — a structured representation of the PDF that can be traversed, queried, and reasoned over.

```c
"""
tree.py
-------
Parses a PDF into a hierarchical DocumentTree using PyMuPDF4LLM.

Uses layout-aware PDF parsing without vector embeddings.
Strategy:
1. Extract markdown with layout preservation using PyMuPDF4LLM
2. Parse markdown headers into tree hierarchy
3. Use page_chunks for accurate page boundary detection

Install: pip install PyMuPDF pymupdf4llm
"""

import os
import re
import json
import time
from typing import List, Dict, Optional
from dataclasses import dataclass, field
from pathlib import Path

import fitz  # PyMuPDF
import pymupdf4llm  # Primary parser

# ── Data models ───────────────────────────────────────────────────────────────

@dataclass
class TreeNode:
    """Hierarchical document node"""
    id: str
    title: str
    level: int  # 0=root, 1=chapter, 2=section, 3=subsection
    page_start: int
    page_end: int
    content: str
    children: List['TreeNode'] = field(default_factory=list)
    heading_type: Optional[str] = None  # "numbered", "unnumbered", "page"
    summary: str = ""
    
    def to_dict(self) -> Dict:
        return {
            "id": self.id,
            "title": self.title,
            "level": self.level,
            "pages": f"{self.page_start}-{self.page_end}",
            "type": self.heading_type,
            "children_count": len(self.children),
            "content_preview": self.content[:200] + "..." if len(self.content) > 200 else self.content
        }

@dataclass
class DocumentTree:
    """Complete document tree with metadata"""
    document_name: str
    root: TreeNode
    total_pages: int
    source_path: str = ""
    
    def print_tree(self, node: Optional[TreeNode] = None, indent: int = 0):
        """Pretty print tree structure"""
        if node is None:
            node = self.root
            print(f"\n📄 {self.document_name} ({self.total_pages} pages)")
        
        prefix = "  " * indent
        icon = "📑" if node.level == 0 else "📖" if node.level == 1 else "📄" if node.level == 2 else "📝"
        print(f"{prefix}{icon} [{node.level}] {node.title} (p{node.page_start}-{node.page_end})")
        
        for child in node.children:
            self.print_tree(child, indent + 1)

class PyMuPDF4LLMTreeBuilder:
    """
    Build hierarchical document trees using PyMuPDF4LLM.
    10x faster than GPU-based methods, no model download required.
    """
    
    def __init__(self, max_content_length: int = 8000):
        self.max_content_length = max_content_length
        
        # Heading detection patterns
        self.patterns = {
            'numbered_section': re.compile(r'^(?:\d+\.)+\s+(.+)$'),  # 1. Introduction, 2.3.1 Methods
            'roman_section': re.compile(r'^(?:[IVX]+)\.?\s+(.+)$', re.IGNORECASE),  # I. Introduction, II.3
            'letter_section': re.compile(r'^([A-Z])\.\s+(.+)$'),  # A. Methods, B. Results
            'unnumbered_heading': re.compile(r'^([A-Z][a-zA-Z\s]{3,50})$'),  # Abstract, Conclusion
        }
    
    def parse_pdf(self, pdf_path: str) -> DocumentTree:
        """
        Parse PDF into hierarchical tree structure.
        
        Strategy:
        1. Extract markdown with layout preservation using PyMuPDF4LLM
        2. Parse markdown headers into tree hierarchy
        3. Use page_chunks for accurate page boundary detection
        """
        pdf_path = Path(pdf_path)
        print(f"🔍 Parsing {pdf_path.name} with PyMuPDF4LLM...")
        
        start_time = time.time()
        
        # Method 1: Get full markdown for structure
        full_md = pymupdf4llm.to_markdown(str(pdf_path))
        
        # Method 2: Get page chunks for accurate pagination
        page_chunks = pymupdf4llm.to_markdown(
            str(pdf_path),
            page_chunks=True,
            write_images=False,
            embed_images=False
        )
        
        # Build page index for content lookup
        page_contents = {i+1: chunk["text"] for i, chunk in enumerate(page_chunks)}
        total_pages = len(page_chunks)
        
        # Parse structure from markdown
        root = self._build_tree_from_markdown(full_md, page_contents, pdf_path.name)
        
        elapsed = time.time() - start_time
        print(f"✅ Parsed in {elapsed:.2f}s: {total_pages} pages, {self._count_nodes(root)} nodes")
        
        return DocumentTree(
            document_name=pdf_path.stem,
            root=root,
            total_pages=total_pages,
            source_path=str(pdf_path)
        )
    
    def _build_tree_from_markdown(
        self, 
        markdown: str, 
        page_contents: Dict[int, str],
        doc_name: str
    ) -> TreeNode:
        """
        Parse markdown headers into hierarchical tree.
        Handles both numbered and unnumbered headings.
        """
        lines = markdown.split('\n')
        
        # Create root node
        root = TreeNode(
            id="root",
            title=doc_name,
            level=0,
            page_start=1,
            page_end=max(page_contents.keys()) if page_contents else 1,
            content="",
            heading_type="root"
        )
        
        # Stack maintains current path: (level, node)
        stack = [(0, root)]
        current_content_lines = []
        current_start_page = 1
        
        def flush_content():
            """Attach accumulated content to current node"""
            if current_content_lines and stack:
                content = '\n'.join(current_content_lines).strip()
                if content:
                    stack[-1][1].content += "\n\n" + content
                    # Generate summary from first paragraph
                    if not stack[-1][1].summary:
                        first_para = content.replace('#', '').strip()[:300]
                        stack[-1][1].summary = first_para
            current_content_lines.clear()
        
        i = 0
        while i < len(lines):
            line = lines[i]
            stripped = line.strip()
            
            # Detect markdown headers
            if stripped.startswith('#'):
                flush_content()
                
                # Calculate level by counting # characters
                level = len(stripped.split()[0]) if stripped.split() else 0
                title = stripped.lstrip('#').strip()
                
                # Classify heading type
                heading_type = self._classify_heading(title)
                
                # Estimate page number based on content position
                # (We'll refine this using page_chunks later)
                page_num = self._estimate_page_number(i, len(lines), max(page_contents.keys()))
                
                # Create new node
                title_slug = '_'.join(re.findall(r'\w+', title))[:20]
                node_id = f"{title_slug}_{i}"
                new_node = TreeNode(
                    id=node_id,
                    title=title,
                    level=level,
                    page_start=page_num,
                    page_end=page_num,  # Will update later
                    content="",
                    heading_type=heading_type
                )
                
                # Attach to appropriate parent
                while stack and stack[-1][0] >= level:
                    closed_node = stack.pop()[1]
                    # Update parent's page_end
                    if stack:
                        stack[-1][1].page_end = max(stack[-1][1].page_end, closed_node.page_end)
                
                if stack:
                    parent = stack[-1][1]
                    parent.children.append(new_node)
                    parent.page_end = max(parent.page_end, page_num)
                
                stack.append((level, new_node))
                current_start_page = page_num
                
            else:
                current_content_lines.append(line)
            
            i += 1
        
        # Flush final content
        flush_content()
        
        # Refine page boundaries using page_chunks content matching
        self._refine_page_boundaries(root, page_contents)
        
        # Distribute content to leaf nodes
        self._distribute_content_to_leaves(root)
        
        return root
    
    def _classify_heading(self, title: str) -> str:
        """Classify heading as numbered, roman, letter, or unnumbered."""
        title = title.strip()
        
        if self.patterns['numbered_section'].match(title):
            return "numbered"
        elif self.patterns['roman_section'].match(title):
            return "roman"
        elif self.patterns['letter_section'].match(title):
            return "letter"
        elif self.patterns['unnumbered_heading'].match(title):
            return "unnumbered"
        else:
            return "unknown"
    
    def _estimate_page_number(self, line_idx: int, total_lines: int, total_pages: int) -> int:
        """Rough page estimation based on line position."""
        if total_pages == 0:
            return 1
        ratio = line_idx / total_lines if total_lines > 0 else 0
        return min(int(ratio * total_pages) + 1, total_pages)
    
    def _refine_page_boundaries(self, root: TreeNode, page_contents: Dict[int, str]):
        """
        Refine page boundaries by matching node content to page chunks.
        This corrects the rough estimates from markdown parsing.
        """
        def find_page_for_content(content: str, start_search: int = 1) -> int:
            """Find which page contains this content."""
            content_snippet = content[:100].strip()
            if not content_snippet:
                return start_search
            
            for page_num, page_text in page_contents.items():
                if page_num >= start_search and content_snippet in page_text:
                    return page_num
            return start_search
        
        def refine_node(node: TreeNode, parent_start: int = 1):
            # Update start page based on content match
            if node.content:
                matched_page = find_page_for_content(node.content, parent_start)
                node.page_start = matched_page
                node.page_end = matched_page
            
            # Process children
            prev_end = node.page_start
            for child in node.children:
                refine_node(child, prev_end)
                prev_end = max(prev_end, child.page_end)
            
            # Update node end to cover all children
            if node.children:
                node.page_end = max(c.page_end for c in node.children)
                node.page_start = min(c.page_start for c in node.children)
        
        refine_node(root)
    
    def _distribute_content_to_leaves(self, node: TreeNode):
        """
        Ensure content is stored at appropriate leaf nodes.
        If a node has children, its content becomes a summary.
        """
        if not node.children:
            return
        
        # Truncate content if node has children (it's a section header)
        if len(node.content) > 500:
            node.summary = node.content[:500] + "..."
            node.content = node.summary
        
        # Recurse
        for child in node.children:
            self._distribute_content_to_leaves(child)
    
    def _count_nodes(self, node: TreeNode) -> int:
        """Count total nodes in tree."""
        return 1 + sum(self._count_nodes(c) for c in node.children)

# Public API
def parse_pdf(pdf_path: str) -> DocumentTree:
    """Parse a PDF into a hierarchical document tree using PyMuPDF4LLM."""
    builder = PyMuPDF4LLMTreeBuilder()
    return builder.parse_pdf(pdf_path)
```

## Step 2: Retrieval (Tree Navigation)

Once we have a structured **DocumentTree**, the next step is retrieval. Instead of performing a one-shot lookup, we **navigate the tree step-by-step**, letting the model decide where to go next.

This is implemented as an **agentic traversal loop** using `langgraph`, where each step involves analyzing the current node and deciding whether to:

- **Retrieve content from the current node**, or
- **Descend into one of its children**

### Core Idea

Retrieval is treated as a **decision process over the tree**:

- Start at the root
- At each node, evaluate relevance to the query
- Either:  
	\- Stop and extract content, or  
	\- Move deeper into a more relevant subsection

This continues until a stopping condition is met (low confidence, max depth, or leaf node).

### Implementation Components

The retrieval pipeline is built as a graph with four main stages:

1. **Analyze (LLM-driven decision)**  
	The model is given:  
	\- Query  
	\- Current node (title, summary, content preview)  
	\- List of child nodes  
	It returns:  
	\- Confidence score  
	\- Whether to descend  
	\- Which child to explore next  
	\- Short reasoning
2. **Descend (tree traversal)**  
	Moves to the selected child node and repeats the process.
3. **Retrieve (content extraction)**  
	When traversal stops, the system extracts content from the current node, along with page metadata.
4. **Generate (final answer)**  
	The retrieved sections are passed to the model to generate a grounded answer with citations.

### Execution Flow

```c
Question
   ↓
[Step 1] Analyze Node      ← LLM evaluates relevance and decides next action
   ↓
[Step 2] Route Decision    ← Descend into children, retrieve content, or backtrack
   ↓
[Step 3] Retrieve Content  ← Extract full text from relevant nodes
   ↓
[Step 4] Generate Answer   ← LLM synthesizes final answer with sources
   ↓
Answer + Path + Confidence + Sources
```

Each step is logged, including:

- Traversal path
- Decisions made at each node
- Confidence scores
- Final sources used

This makes the retrieval process **fully transparent and debuggable**, unlike black-box retrieval systems.

### Key Characteristics

- Retrieval is **iterative, not one-shot**
- Decisions are **explicit and inspectable**
- Navigation is guided by **structure + reasoning**
- The system naturally focuses on **relevant subsections instead of broad chunks**

The full implementation below shows how this traversal is orchestrated using a stateful graph and controlled LLM calls.

```c
"""
retriever.py
------------
Agent-based retrieval that navigates a DocumentTree to answer a query,
with detailed logging of every LLM call and decision.
"""

import json
import re
import time
import logging
from typing import Annotated, Any, Dict, List, Optional, TypedDict
import operator

from langgraph.graph import StateGraph, END
from openai import OpenAI

from tree import TreeNode, DocumentTree

# ── Logger setup ──────────────────────────────────────────────────────────────
#
# Two handlers:
#   console  — INFO and above, human-readable with colour-coded prefixes
#   file     — DEBUG and above, full detail including raw prompts/responses
#
# Usage from outside:
#   import logging
#   logging.getLogger("retriever").setLevel(logging.DEBUG)  # show raw prompts too

logger = logging.getLogger("retriever")
logger.setLevel(logging.DEBUG)
logger.propagate = False   # don't bubble up to root logger

if not logger.handlers:
    # ── Console handler (INFO) ────────────────────────────────────────────
    _ch = logging.StreamHandler()
    _ch.setLevel(logging.INFO)
    _ch.setFormatter(logging.Formatter("%(message)s"))   # raw message only
    logger.addHandler(_ch)

    # ── File handler (DEBUG) ─────────────────────────────────────────────
    _fh = logging.FileHandler("retriever.log", mode="a", encoding="utf-8")
    _fh.setLevel(logging.DEBUG)
    _fh.setFormatter(logging.Formatter(
        "%(asctime)s  %(levelname)-7s  %(message)s",
        datefmt="%H:%M:%S",
    ))
    logger.addHandler(_fh)

# ── Visual helpers ────────────────────────────────────────────────────────────

_DIVIDER   = "─" * 65
_SEPARATOR = "═" * 65

def _box(title: str) -> str:
    return f"\n{_SEPARATOR}\n  {title}\n{_SEPARATOR}"

def _indent(text: str, n: int = 4) -> str:
    pad = " " * n
    return "\n".join(pad + line for line in str(text).splitlines())

# ── State ─────────────────────────────────────────────────────────────────────

class RetrievalState(TypedDict):
    query: str
    current_node: Optional[TreeNode]
    tree: TreeNode
    path_taken: Annotated[List[str], operator.add]
    retrieved_content: Annotated[List[str], operator.add]
    reasoning: str
    confidence: float
    should_descend: bool
    target_child_id: Optional[str]
    depth: int
    final_answer: Optional[str]
    call_log: Annotated[List[dict], operator.add]   # full log of every LLM call

# ── Core LLM caller with logging ──────────────────────────────────────────────

def _call_llm(
    client: OpenAI,
    model: str,
    prompt: str,
    call_type: str,          # "navigate" | "answer"
    call_number: int,
) -> tuple[str, float]:
    """
    Call the LLM and log everything:
      - call number and type
      - full prompt (DEBUG / file only)
      - raw response (DEBUG / file only)
      - latency
    Returns (response_text, elapsed_seconds).
    """
    logger.info(f"\n{_DIVIDER}")
    logger.info(f"  LLM Call #{call_number}  [{call_type.upper()}]")
    logger.info(_DIVIDER)

    # Full prompt goes to file (DEBUG) only — too verbose for console
    logger.debug(f"PROMPT:\n{_indent(prompt)}")

    t0 = time.perf_counter()
    response = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": prompt}],
        temperature=0.0,
    )
    elapsed = time.perf_counter() - t0
    raw = response.choices[0].message.content.strip()

    logger.debug(f"RAW RESPONSE:\n{_indent(raw)}")
    logger.info(f"  Model    : {model}")
    logger.info(f"  Latency  : {elapsed:.2f}s")
    logger.info(f"  Tokens   : {response.usage.prompt_tokens} in / "
                f"{response.usage.completion_tokens} out")

    return raw, elapsed

def _strip_fences(text: str) -> str:
    if "\`\`\`" in text:
        for part in text.split("\`\`\`"):
            part = part.strip().lstrip("json").strip()
            try:
                json.loads(part)
                return part
            except json.JSONDecodeError:
                continue
    return text

# ── Graph nodes ───────────────────────────────────────────────────────────────

def _make_analyze(client: OpenAI, model: str):
    def analyze_node(state: RetrievalState) -> dict:
        # Handle both TreeNode and DocumentTree objects
        if state["current_node"]:
            node: TreeNode = state["current_node"]
        else:
            # If tree is a DocumentTree, get its root; otherwise use it directly
            tree_obj = state["tree"]
            node = tree_obj.root if hasattr(tree_obj, "root") else tree_obj
        
        call_num = len(state["call_log"]) + 1
        depth = state["depth"]

        children_info = (
            [{"id": c.id, "title": c.title,
              "summary": getattr(c, "summary", "")[:150]}
             for c in node.children]
            if node.children else []
        )

        # ── Log: entering this node ───────────────────────────────────────
        logger.info(f"\n{'  ' * depth}┌─ Depth {depth} | Node: \"{node.title}\"")
        logger.info(f"{'  ' * depth}│  id={node.id}  pages={node.page_start}-{node.page_end}")
        logger.info(f"{'  ' * depth}│  children={[c.title for c in node.children] or 'none (leaf)'}")

        prompt = f"""You are navigating a research paper tree to answer a query.

Query: "{state['query']}"

Current node:
  id      : {node.id}
  title   : {node.title}
  summary : {getattr(node, 'summary', '')[:300]}
  pages   : {node.page_start}–{node.page_end}
  preview : {node.content[:500] if node.content else 'N/A'}

Children: {json.dumps(children_info, indent=2) if children_info else "None (leaf node)"}

Decide:
1. confidence      : 0–1, how likely does this node (or its children) contain the answer?
2. should_descend  : true only if a specific child is more relevant than this node's content
3. target_child_id : the id of the best child to visit (null if should_descend is false)
4. reasoning       : one sentence explaining your decision

Respond ONLY as valid JSON, no markdown fences:
{{
  "confidence": 0.85,
  "should_descend": true,
  "target_child_id": "1_Introduction_12",
  "reasoning": "The Introduction section directly addresses what Bigtable is."
}}"""

        raw, elapsed = _call_llm(client, model, prompt, "navigate", call_num)
        raw = _strip_fences(raw)

        try:
            decision = json.loads(raw)
        except json.JSONDecodeError:
            logger.warning(f"  [!] JSON parse failed — using fallback decision")
            decision = {
                "confidence": 0.5,
                "should_descend": bool(node.children),
                "target_child_id": node.children[0].id if node.children else None,
                "reasoning": "Fallback: could not parse LLM response",
            }

        conf      = float(decision.get("confidence", 0.5))
        descend   = bool(decision.get("should_descend", False))
        child_id  = decision.get("target_child_id")
        reasoning = decision.get("reasoning", "")

        # ── Log: decision ─────────────────────────────────────────────────
        arrow = "↓ descend" if (descend and node.children) else "→ retrieve"
        logger.info(f"{'  ' * depth}│")
        logger.info(f"{'  ' * depth}│  Decision   : {arrow}")
        logger.info(f"{'  ' * depth}│  Confidence : {conf:.0%}")
        if child_id and descend:
            logger.info(f"{'  ' * depth}│  Next node  : {child_id}")
        logger.info(f"{'  ' * depth}│  Reasoning  : {reasoning}")
        logger.info(f"{'  ' * depth}└─ ({elapsed:.2f}s)")

        entry = {
            "call_number":    call_num,
            "call_type":      "navigate",
            "node_id":        node.id,
            "node_title":     node.title,
            "depth":          depth,
            "confidence":     conf,
            "should_descend": descend,
            "target_child":   child_id,
            "reasoning":      reasoning,
            "latency_s":      round(elapsed, 3),
        }

        return {
            "path_taken":      [node.id],     # LangGraph appends automatically
            "current_node":    node,
            "confidence":      conf,
            "should_descend":  descend,
            "target_child_id": child_id,
            "reasoning":       reasoning,
            "depth":           depth + 1,
            "call_log":        [entry],        # LangGraph appends automatically
        }

    return analyze_node

def _make_descend():
    def descend(state: RetrievalState) -> dict:
        current: TreeNode = state["current_node"]
        target_id: Optional[str] = state.get("target_child_id")
        depth = state["depth"]

        target = next(
            (c for c in current.children if c.id == target_id),
            current.children[0],
        )

        logger.info(f"\n{'  ' * depth}➜  Descending into: \"{target.title}\"")

        return {"current_node": target}

    return descend

def _make_retrieve():
    def retrieve(state: RetrievalState) -> dict:
        node: TreeNode = state["current_node"]
        depth = state["depth"]

        logger.info(f"\n{'  ' * depth}✦  Retrieving content from: \"{node.title}\"")
        logger.info(f"{'  ' * depth}   Pages {node.page_start}–{node.page_end} | "
                    f"{len(node.content)} chars")

        chunk = (
            f"=== **{node.title}** "
            f"(Pages {node.page_start}-{node.page_end}) ===\n"
            f"{node.content}"
        )
        return {"retrieved_content": [chunk]}   # LangGraph appends automatically

    return retrieve

def _make_generate(client: OpenAI, model: str):
    def generate_answer(state: RetrievalState) -> dict:
        call_num  = len(state["call_log"]) + 1
        context   = "\n\n---\n\n".join(state["retrieved_content"])
        sources   = [s.splitlines()[0] for s in state["retrieved_content"]]

        logger.info(f"\n{_DIVIDER}")
        logger.info(f"  Generating answer from {len(state['retrieved_content'])} "
                    f"retrieved section(s):")
        for s in sources:
            logger.info(f"    • {s}")

        prompt = f"""You are an expert on distributed systems and database engineering.
Answer the question using ONLY the retrieved document sections below.
Cite the section title and page range for every claim you make.
If the context is insufficient, say so clearly — do not guess.

Question: {state['query']}

Retrieved sections:
{context}

Answer:"""

        raw, elapsed = _call_llm(client, model, prompt, "answer", call_num)

        entry = {
            "call_number": call_num,
            "call_type":   "answer",
            "sources":     sources,
            "latency_s":   round(elapsed, 3),
        }

        logger.info(f"\n  Answer generated in {elapsed:.2f}s")

        return {
            "final_answer": raw,
            "call_log":     [entry],
        }

    return generate_answer

# ── Routing ───────────────────────────────────────────────────────────────────

MAX_DEPTH = 5

def _route(state: RetrievalState) -> str:
    if state["confidence"] < 0.3:
        logger.info(f"\n  ✗  Low confidence ({state['confidence']:.0%}) — stopping traversal")
        return "end"
    if state["depth"] >= MAX_DEPTH:
        logger.info(f"\n  ⚠  Max depth ({MAX_DEPTH}) reached — retrieving current node")
        return "retrieve"
    if state["should_descend"] and state["current_node"].children:
        return "descend"
    return "retrieve"

# ── Graph assembly ────────────────────────────────────────────────────────────

def _build_graph(client: OpenAI, model: str) -> Any:
    workflow = StateGraph(RetrievalState)

    workflow.add_node("analyze",  _make_analyze(client, model))
    workflow.add_node("descend",  _make_descend())
    workflow.add_node("retrieve", _make_retrieve())
    workflow.add_node("generate", _make_generate(client, model))

    workflow.set_entry_point("analyze")
    workflow.add_conditional_edges(
        "analyze", _route,
        {"descend": "descend", "retrieve": "retrieve", "end": END},
    )
    workflow.add_edge("descend",  "analyze")
    workflow.add_edge("retrieve", "generate")
    workflow.add_edge("generate", END)

    return workflow.compile()

# ── Visualization ─────────────────────────────────────────────────────────────

def generate_workflow_png(output_path: str = "workflow.png") -> str:
    """
    Generate a PNG visualization of the LangGraph workflow structure.

    Args:
        output_path: Path where the PNG will be saved (default: "workflow.png")

    Returns:
        Path to the generated PNG file
    """
    workflow = StateGraph(RetrievalState)
    
    # Add nodes (dummy functions for structure visualization)
    workflow.add_node("analyze",  lambda state: state)
    workflow.add_node("descend",  lambda state: state)
    workflow.add_node("retrieve", lambda state: state)
    workflow.add_node("generate", lambda state: state)
    
    workflow.set_entry_point("analyze")
    workflow.add_conditional_edges(
        "analyze", lambda state: "retrieve",
        {"descend": "descend", "retrieve": "retrieve", "end": END},
    )
    workflow.add_edge("descend",  "analyze")
    workflow.add_edge("retrieve", "generate")
    workflow.add_edge("generate", END)
    
    graph = workflow.compile()
    graph_image = graph.get_graph().draw_mermaid_png()
    
    with open(output_path, "wb") as f:
        f.write(graph_image)
    
    logger.info(f"Workflow visualization saved to: {output_path}")
    return output_path

# ── Public API ────────────────────────────────────────────────────────────────

def retrieve(query: str, tree: TreeNode, client: OpenAI, model: str = "gpt-4o-mini") -> Dict:
    """
    Navigate the document tree and answer a query, logging every LLM call.

    Console output (INFO):
        Shows the traversal path, each decision, confidence, and reasoning.

    File output (DEBUG → retriever.log):
        Additionally logs the full prompt and raw LLM response for every call.
    """
    logger.info(_box(f"New Query"))
    logger.info(f"\n  Q: {query}\n")

    graph = _build_graph(client, model)

    t_start = time.perf_counter()

    result = graph.invoke({
        "query":             query,
        "current_node":      None,
        "tree":              tree,
        "path_taken":        [],
        "retrieved_content": [],
        "reasoning":         "",
        "confidence":        0.0,
        "should_descend":    True,
        "target_child_id":   None,
        "depth":             0,
        "final_answer":      None,
        "call_log":          [],
    })

    total_s = time.perf_counter() - t_start
    call_log = result.get("call_log", [])
    nav_calls = sum(1 for c in call_log if c["call_type"] == "navigate")
    ans_calls = sum(1 for c in call_log if c["call_type"] == "answer")

    # ── Final summary ──────────────────────────────────────────────────────
    logger.info(f"\n{_SEPARATOR}")
    logger.info("  RETRIEVAL SUMMARY")
    logger.info(_SEPARATOR)
    logger.info(f"  Total LLM calls : {len(call_log)}  "
                f"({nav_calls} navigate + {ans_calls} answer)")
    logger.info(f"  Path taken      : {' → '.join(result.get('path_taken', []))}")
    logger.info(f"  Total latency   : {total_s:.2f}s")
    logger.info(_SEPARATOR)

    return {
        "answer":     result.get("final_answer") or "No answer generated (low confidence).",
        "path":       result.get("path_taken", []),
        "reasoning":  result.get("reasoning", ""),
        "confidence": result.get("confidence", 0.0),
        "sources":    result.get("retrieved_content", []),
        "call_log":   call_log,
    }
```

Let’s now define `main.py` to stitch both files together.

```c
"""
main.py
-------
Vectorless RAG — LangGraph Agent + PDF Tree (no PageIndex)

Flow:
  1. Download Bigtable PDF
  2. Parse PDF → DocumentTree  (one-time, cached to JSON)
  3. For each question: agent traverses the tree → retrieves sections → generates answer

Install:
  pip install PyMuPDF openai langgraph pydantic python-dotenv

.env:
  OPENAI_API_KEY=sk-...
"""

import json
import os
import urllib.request
from pathlib import Path
from dataclasses import asdict

from dotenv import load_dotenv
from openai import OpenAI

from questions import QUESTIONS
from retriever import retrieve, generate_workflow_png
from tree import parse_pdf, TreeNode

load_dotenv()

# ── Config ────────────────────────────────────────────────────────────────────
PDF_URL = (
    "https://static.googleusercontent.com/media/research.google.com"
    "/en//archive/bigtable-osdi06.pdf"
)
PDF_PATH        = Path("bigtable-osdi06.pdf")
TREE_CACHE_PATH = Path("results/document_tree.json")
MODEL           = "gpt-4o-mini"

# ── Init client (one instance, shared across tree.py and retriever.py) ────────
if not os.environ.get("OPENAI_API_KEY"):
    raise SystemExit(
        "OPENAI_API_KEY not set.\n"
        "Create a .env file with:  OPENAI_API_KEY=sk-..."
    )

client = OpenAI(api_key=os.environ["OPENAI_API_KEY"])

# ── Step 1: Download PDF ──────────────────────────────────────────────────────
def download_pdf() -> None:
    if PDF_PATH.exists():
        print(f"[✓] PDF already present: {PDF_PATH}")
        return
    print("[↓] Downloading Bigtable paper …")
    urllib.request.urlretrieve(PDF_URL, PDF_PATH)
    print(f"[✓] Saved → {PDF_PATH}")

# ── Step 2: Build / load tree ─────────────────────────────────────────────────
def dict_to_treenode(data: dict) -> TreeNode:
    """Recursively reconstruct TreeNode from dictionary."""
    children = [
        dict_to_treenode(child) for child in data.get("children", [])
    ]
    data_copy = data.copy()
    data_copy["children"] = children
    return TreeNode(**data_copy)

def get_tree() -> TreeNode:
    """
    Load cached TreeNode from JSON, or build and cache it fresh.
    """
    TREE_CACHE_PATH.parent.mkdir(parents=True, exist_ok=True)

    if TREE_CACHE_PATH.exists():
        print(f"[✓] Loading cached tree from {TREE_CACHE_PATH}")
        with open(TREE_CACHE_PATH) as f:
            data = json.load(f)
        # Reconstruct TreeNode from cached dict (extract root from DocumentTree)
        tree = dict_to_treenode(data.get("root", data))
        print(f"    {len(tree.children)} sections loaded")
        return tree

    print("[~] Building tree (first run — takes ~10–30 sec with PyMuPDF4LLM) …")
    tree = parse_pdf(str(PDF_PATH))

    with open(TREE_CACHE_PATH, "w") as f:
        json.dump(asdict(tree), f, indent=2, default=str)
    print(f"[✓] Tree cached → {TREE_CACHE_PATH}")
    return tree

# ── Step 3: Ask a question ────────────────────────────────────────────────────
def ask(question: str, tree: TreeNode) -> dict:
    print(f"\n{'─'*70}")
    print(f"  Q: {question}")
    print(f"{'─'*70}")

    # Pass the LLM client to retrieve function
    result = retrieve(question, tree, client)

    print(f"\n  [Reasoning]  {result['reasoning']}")
    print(f"  [Confidence] {result['confidence']:.0%}")
    print(f"  [Path]       {' → '.join(result['path'])}")

    if result["sources"]:
        print(f"\n  [Sources]")
        for src in result["sources"][:2]:
            print(f"    {src.splitlines()[0]}")   # just the header line

    print(f"\n  [Answer]\n{result['answer']}")
    return result

# ── Main ──────────────────────────────────────────────────────────────────────
def main() -> None:
    download_pdf()
    
    # Load or build the tree
    tree = get_tree()    
    # Generate workflow visualization
    TREE_CACHE_PATH.parent.mkdir(parents=True, exist_ok=True)
    workflow_png_path = TREE_CACHE_PATH.parent / "workflow.png"
    generate_workflow_png(output_path=str(workflow_png_path))
    print(f"[✓] Workflow diagram saved → {workflow_png_path}")
    print(f"\n{'═'*70}")
    print("  Vectorless RAG — Google Bigtable (no PageIndex)")
    print(f"{'═'*70}")

    results = []
    for i, question in enumerate(QUESTIONS, 1):
        print(f"\n[{i}/{len(QUESTIONS)}]")
        try:
            result = ask(question, tree)
            results.append({"question": question, "result": result, "ok": True})
        except Exception as e:
            print(f"  [ERROR] {e}")
            results.append({"question": question, "error": str(e), "ok": False})

    ok = sum(r["ok"] for r in results)
    print(f"\n{'═'*70}")
    print(f"  Done: {ok}/{len(results)} questions answered successfully")
    print(f"{'═'*70}\n")

if __name__ == "__main__":
    main()
```

In your terminal, please run below command:

```c
((.venv)) python main.py
```

It first extracts text from the pdf and creates a tree structure using `pymupdf4llm` library. Here is a sample of the data:

```c
{
  "document_name": "bigtable-osdi06",
  "root": {
    "id": "root",
    "title": "bigtable-osdi06.pdf",
    "level": 0,
    "page_start": 1,
    "page_end": 13,
    "content": "",
    "children": [
      {
        "id": "Bigtable_A_Distribut_0",
        "title": "**Bigtable: A Distributed Storage System for Structured Data**",
        "level": 1,
        "page_start": 1,
        "page_end": 13,
        "content": "\n\nFay Chang, Jeffrey Dean, Sanjay Ghemawat, Wilson C. Hsieh, Deborah A. Wallach Mike Burrows, Tushar Chandra, Andrew Fikes, Robert E. Gruber \n\@google.com">n{fay,jeff,sanjay,wilsonh,kerr,m3b,tushar,fikes,gruber}@google.com \n\n_Google, Inc._",
        "children": [
          {
            "id": "Abstract_8",
            "title": "**Abstract**",
            "level": 2,
            "page_start": 1,
            "page_end": 1,
            "content": "\n\nBigtable is a distributed storage system for managing structured data that is designed to scale to a very large size: petabytes of data across thousands of commodity servers. Many projects at Google store data in Bigtable, including web indexing, Google Earth, and Google Finance. These applications place very different demands on Bigtable, both in terms of data size (from URLs to web pages to satellite imagery) and latency requirements (from backend bulk processing to real-time data serving). Despite these varied demands, Bigtable has successfully provided a flexible, high-performance solution for all of these Google products. In this paper we describe the simple data model provided by Bigtable, which gives clients dynamic control over data layout and format, and we describe the design and implementation of Bigtable.",
            "children": [],
            "heading_type": "unknown",
            "summary": "Bigtable is a distributed storage system for managing structured data that is designed to scale to a very large size: petabytes of data across thousands of commodity servers. Many projects at Google store data in Bigtable, including web indexing, Google Earth, and Google Finance. These applications "
          },
          {
            "id": "1_Introduction_12",
            "title": "**1 Introduction**",
            "level": 2,
            "page_start": 1,
            "page_end": 1,
            "content": "\n\nOver the last two and a half years we have designed, implemented, and deployed a distributed storage system for managing structured data at Google called Bigtable. Bigtable is designed to reliably scale to petabytes of data and thousands of machines. Bigtable has achieved several goals: wide applicability, scalability, high performance, and high availability. Bigtable is used by more than sixty Google products and projects, including Google Analytics, Google Finance, Orkut, Personalized Search, Writely, and Google Earth. These products use Bigtable for a variety of demanding workloads, which range from throughput-oriented batch-processing jobs to latency-sensitive serving of data to end users. The Bigtable clusters used by these products span a wide range of configurations, from a handful to thousands of servers, and store up to several hundred terabytes of data. \n\nIn many ways, Bigtable resembles a database: it shares many implementation strategies with databases. Parallel databases [14] and main-memory databases [13] have \n\nachieved scalability and high performance, but Bigtable provides a different interface than such systems. Bigtable does not support a full relational data model; instead, it provides clients with a simple data model that supports dynamic control over data layout and format, and allows clients to reason about the locality properties of the data represented in the underlying storage. Data is indexed using row and column names that can be arbitrary strings. Bigtable also treats data as uninterpreted strings, although clients often serialize various forms of structured and semi-structured data into these strings. Clients can control the locality of their data through careful choices in their schemas. Finally, Bigtable schema parameters let clients dynamically control whether to serve data out of memory or from disk. \n\nSection 2 describes the data model in more detail, and Section 3 provides an overview of the client API. Section 4 briefly describes the underlying Google infrastructure on which Bigtable depends. Section 5 describes the fundamentals of the Bigtable implementation, and Section 6 describes some of the refinements that we made to improve Bigtable\u2019s performance. Section 7 provides measurements of Bigtable\u2019s performance. We describe several examples of how Bigtable is used at Google in Section 8, and discuss some lessons we learned in designing and supporting Bigtable in Section 9. Finally, Section 10 describes related work, and Section 11 presents our conclusions.",
            "children": [],
            "heading_type": "unknown",
            "summary": "Over the last two and a half years we have designed, implemented, and deployed a distributed storage system for managing structured data at Google called Bigtable. Bigtable is designed to reliably scale to petabytes of data and thousands of machines. Bigtable has achieved several goals: wide applica"
          },

}
```

Then it also generates the image of the `langgraph` flow in the `results` folder in the repo.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Drv1Kx4O5K9N2FIBgJh4zg.png)

Vectorless RAG Flow

Here is the terminal output, where the answer of a question is also mentioned.

```c
((.venv) ) (base) user@AS-MAC- vectorless-rag % python main.py
[✓] PDF already present: bigtable-osdi06.pdf
[~] Building tree (first run — takes ~10–30 sec with PyMuPDF4LLM) …
🔍 Parsing bigtable-osdi06.pdf with PyMuPDF4LLM...
=== Document parser messages ===
Using Tesseract for OCR processing.

=== Document parser messages ===
Using Tesseract for OCR processing.

✅ Parsed in 6.80s: 14 pages, 37 nodes
[✓] Tree cached → results/document_tree.json
Workflow visualization saved to: results/workflow.png
[✓] Workflow diagram saved → results/workflow.png

══════════════════════════════════════════════════════════════════════
  Vectorless RAG — Google Bigtable (no PageIndex)
══════════════════════════════════════════════════════════════════════

[1/1]

──────────────────────────────────────────────────────────────────────
  Q: What is Bigtable and what problem does it solve?
──────────────────────────────────────────────────────────────────────

═════════════════════════════════════════════════════════════════
  New Query
═════════════════════════════════════════════════════════════════

  Q: What is Bigtable and what problem does it solve?

┌─ Depth 0 | Node: "bigtable-osdi06.pdf"
│  id=root  pages=1-13
│  children=['**Bigtable: A Distributed Storage System for Structured Data**']

─────────────────────────────────────────────────────────────────
  LLM Call #1  [NAVIGATE]
─────────────────────────────────────────────────────────────────
  Model    : gpt-4o-mini
  Latency  : 3.50s
  Tokens   : 310 in / 77 out
│
│  Decision   : ↓ descend
│  Confidence : 85%
│  Next node  : Bigtable_A_Distribut_0
│  Reasoning  : The child node is titled 'Bigtable: A Distributed Storage System for Structured Data', which suggests it will provide a detailed explanation of what Bigtable is and the problems it addresses.
└─ (3.50s)

  ➜  Descending into: "**Bigtable: A Distributed Storage System for Structured Data**"

  ┌─ Depth 1 | Node: "**Bigtable: A Distributed Storage System for Structured Data**"
  │  id=Bigtable_A_Distribut_0  pages=1-13
  │  children=['**Abstract**', '**1 Introduction**', '**2 Data Model**', '**Rows**', '**Column Families**', '**Timestamps**', 'Figure 2: Writing to Bigtable.', '**3 API**', 'Figure 3: Reading from Bigtable.', '**4 Building Blocks**', '**5 Implementation**', '**5.1 Tablet Location**', '**5.2 Tablet Assignment**', '**5.3 Tablet Serving**', '**5.4 Compactions**', '**6**', '**Locality groups**', '**Caching for read performance**', '', '**Compression**', '**Commit-log implementation**', '**Speeding up tablet recovery**', '**Exploiting immutability**', '**7 Performance Evaluation**', '**Single tablet-server performance**', '**Scaling**', '**8 Real Applications**', '**8.1 Google Analytics**', '**8.2 Google Earth**', '**8.3 Personalized Search**', '**9 Lessons**', '**10 Related Work**', '**Acknowledgements**', '**References**', '**11 Conclusions**']

─────────────────────────────────────────────────────────────────
  LLM Call #2  [NAVIGATE]
─────────────────────────────────────────────────────────────────
  Model    : gpt-4o-mini
  Latency  : 2.14s
  Tokens   : 2481 in / 48 out
  │
  │  Decision   : ↓ descend
  │  Confidence : 85%
  │  Next node  : 1_Introduction_12
  │  Reasoning  : The Introduction section directly addresses what Bigtable is.
  └─ (2.14s)

    ➜  Descending into: "**1 Introduction**"

    ┌─ Depth 2 | Node: "**1 Introduction**"
    │  id=1_Introduction_12  pages=1-1
    │  children=none (leaf)

─────────────────────────────────────────────────────────────────
  LLM Call #3  [NAVIGATE]
─────────────────────────────────────────────────────────────────
  Model    : gpt-4o-mini
  Latency  : 3.18s
  Tokens   : 369 in / 56 out
    │
    │  Decision   : → retrieve
    │  Confidence : 85%
    │  Reasoning  : The Introduction section directly addresses what Bigtable is and the problems it solves, making it sufficient for the query.
    └─ (3.18s)

      ✦  Retrieving content from: "**1 Introduction**"
         Pages 1–1 | 2539 chars

─────────────────────────────────────────────────────────────────
  Generating answer from 1 retrieved section(s):
    • === ****1 Introduction**** (Pages 1-1) ===

─────────────────────────────────────────────────────────────────
  LLM Call #4  [ANSWER]
─────────────────────────────────────────────────────────────────
  Model    : gpt-4o-mini
  Latency  : 6.77s
  Tokens   : 564 in / 199 out

  Answer generated in 6.77s

═════════════════════════════════════════════════════════════════
  RETRIEVAL SUMMARY
═════════════════════════════════════════════════════════════════
  Total LLM calls : 4  (3 navigate + 1 answer)
  Path taken      : root → Bigtable_A_Distribut_0 → 1_Introduction_12
  Total latency   : 15.60s
═════════════════════════════════════════════════════════════════

  [Reasoning]  The Introduction section directly addresses what Bigtable is and the problems it solves, making it sufficient for the query.
  [Confidence] 85%
  [Path]       root → Bigtable_A_Distribut_0 → 1_Introduction_12

  [Sources]
    === ****1 Introduction**** (Pages 1-1) ===

  [Answer]
Bigtable is a distributed storage system designed for managing structured data at Google. It addresses the need for a system that can reliably scale to petabytes of data and thousands of machines while achieving goals such as wide applicability, scalability, high performance, and high availability. It is utilized by over sixty Google products and projects for various demanding workloads, including both throughput-oriented batch-processing jobs and latency-sensitive data serving to end users (Section 1 Introduction, Pages 1-1).

Bigtable resembles a database but does not support a full relational data model. Instead, it offers a simple data model that allows clients to control data layout and format dynamically, as well as manage data locality. Data is indexed using arbitrary strings for row and column names, and it treats data as uninterpreted strings, enabling clients to serialize structured and semi-structured data. Clients can also influence data locality through schema choices and control whether data is served from memory or disk (Section 1 Introduction, Pages 1-1).

══════════════════════════════════════════════════════════════════════
  Done: 1/1 questions answered successfully
```

You can refer to complete end to end code at my github repo here.

## Practical Aspects of Vectorless RAG

From the implementation and execution trace above, a few practical considerations stand out when building a vectorless retrieval system.

### 1\. Structure Quality Matters

Everything depends on how well the document is parsed into a tree.

- Clean headings → better navigation
- Noisy PDFs → weaker traversal decisions
- Missing hierarchy → flat, less effective retrieval

In practice, investing in **good parsing (layout + headers)** has a direct impact on retrieval quality.

### 2\. Node Granularity is a Key Trade-off

How you define nodes affects both accuracy and performance:

- **Too coarse (large sections)**  
	→ less precise answers
- **Too fine (tiny chunks)**  
	→ deeper traversal, more LLM calls

A balanced hierarchy (section → subsection → leaf) works best.

### 3\. Traversal Depth vs Latency

From the run:

```c
Total LLM calls : 4  (3 navigate + 1 answer)
Total latency   : 15.60s
```

Each navigation step adds latency.

In real systems, you’ll want to:

- Limit max depth
- Tune stopping thresholds (confidence)
- Avoid unnecessary exploration

### 4\. Prompt Design Controls Behavior

The quality of traversal depends heavily on the **navigation prompt**:

- Clear instructions → better decisions
- Ambiguous prompts → random traversal

Small changes (e.g., how you define *“should\_descend”*) can significantly impact results.

### 5\. Logging is Not Optional

One of the biggest advantages here is visibility:

- You can see **exactly where the system went**
- You can debug *why* it made a decision
- You can tune behavior based on real traces

Without logs like:

```c
Decision   : ↓ descend
Reasoning  : The Introduction section directly addresses the query
```

…it becomes very hard to improve the system.

### 6\. Works Best for Structured Documents

This approach performs well when:

- Documents have clear sections (papers, reports, docs)
- Information is logically organized

It is less effective when:

- Content is unstructured (logs, chats, messy text)
- There is no meaningful hierarchy to follow

### 7\. You Still Need Good Content

This sounds obvious, but matters more here:

- If the right information is not in a well-defined section
- The system has no “semantic fallback”

So content organization becomes part of system design.

Vectorless RAG shifts the focus from *searching everywhere* to *navigating intelligently*.

## Conclusion

Vectorless RAG reframes retrieval as a guided process rather than a one-shot lookup. By preserving document structure and navigating it step by step, the system builds answers through explicit decisions — where to go, when to stop, and what to extract. The result is a pipeline that is not only effective for structured data, but also transparent and easy to reason about.

In practice, this isn’t about choosing between traditional RAG and vectorless RAG. They represent different architectural choices. Depending on the problem, one may complement the other, or even coexist within the same system. What this approach highlights is that retrieval doesn’t have to rely solely on similarity; it can also emerge from structure, navigation, and controlled reasoning.

## References:

- [PageIndex Framework (Vectorless RAG)](https://github.com/VectifyAI/PageIndex).
- [Vectorless RAG](https://www.geeksforgeeks.org/artificial-intelligence/vectorless-rag-pageindex/)
- [Bigtable: A Distributed Storage System for Structured Data](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf)
- [Alpha Iterations Vectorless RAG Repo](https://github.com/alphaiterations/agentic-ai-usecases/tree/main/advanced/vectorless-rag)

Thank you for reading the article.

The learning curve is steep, but the view is worth it. [Follow along](https://medium.com/@alphaiterations) if you enjoy the climb.

You can also follow me on [Linkedin](https://www.linkedin.com/in/jainvijendra/) to get regular updates or further collaboration.

And if your curiosity is still running (like a loop without a break condition), check out my other articles:

1. [Build Agentic RAG using LangGraph](https://medium.com/p/b568aa26d710)
2. [Practical Guide to Using ChromaDB for RAG and Semantic Search](https://medium.com/@alphaiterations/chromadb-end-to-end-tutorial-c18202fa66a2)
3. [Reading Images with GPT-4o: The Future of Visual Understanding with AI](https://medium.com/@alphaiterations/reading-images-with-gpt-4o-the-future-of-visual-understanding-with-ai-7d4a60c02ccb)
4. [Agentic AI Project: Build Mini Perplexity AI Chatbot: Step by Step Guide \[Code Included\]](https://medium.com/data-science-collective/build-mini-perplexity-step-by-step-guide-e9b3c81cbbf6)
5. [Agentic AI: Build ReAct Agent using LangGraph](https://medium.com/@alphaiterations/agentic-ai-build-react-agent-using-langgraph-facac8ae6031)
6. [Agentic AI Project: Build a multi-agent system with LangGraph and OpenAI API](https://medium.com/towards-artificial-intelligence/agentic-ai-project-build-a-multi-agent-system-with-langgraph-and-open-ai-344ab768caac)
7. [Building an AI Agent with Model Context Protocol (MCP): A Complete Guide](https://medium.com/towards-artificial-intelligence/building-an-ai-agent-with-model-context-protocol-mcp-a-complete-guide-37b8f6cd7b2b)
8. [TOON vs JSON: A Comprehensive Performance Comparison](https://medium.com/towards-artificial-intelligence/toon-vs-json-a-comprehensive-performance-comparison-446a2fb82f20)
9. [Building an Intelligent Resume Transformation Agent Powered by LangGraph and gpt-4o-mini](https://medium.com/towards-artificial-intelligence/building-an-intelligent-resume-transformation-agent-powered-by-langgraph-and-gpt-4o-mini-2fbb3004dcd3)
10. [Agentic AI Project: Build a Customer Service Chatbot for a Clinic](https://medium.com/towards-artificial-intelligence/agentic-ai-project-build-a-customer-service-chatbot-for-a-clinic-9744ef4a5b25)