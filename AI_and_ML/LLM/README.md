# LLM
- [Advanced Prompting Techniques](#advanced_prompting_techniques)
- [Agent system testing](#agent_system_testing)
- [Hybrid search](#hybrid_search)
- [LangGraph](#langgraph)
- [MMR](#mmr)
- [Reranking](#reranking)
- [Scoring](#scoring)

## Advanced Prompting Techniques <a name="advanced_prompting_techniques"></a>
- Few-Shot Learning - you give model a few examples
- Chain-of-Thought - the method involves guiding the model through step-by-step reasoning to help it solve complex tasks more effectively
- Role-playing - assigning a specific role to the model and/or defining the user’s role or target audience.
- Temperature, Top-p - Temperature controls how boldly the model chooses between possible outputs (higher = more creative), while top-p controls how many possible outputs are considered in the first place.

## Agent system testing <a name="agent_system_testing"></a>
- Task-based evaluation - Evaluate whether an agent correctly completes predefined tasks from input to final output, usually using a golden dataset.
- Tool-use validation - Check whether the agent correctly selects and calls tools (APIs, functions, databases), including correct arguments and execution order.
- Adversarial testing - Test robustness of agents against malicious, ambiguous, or edge-case inputs (e.g., prompt injection, misleading instructions).

## Hybrid search <a name="hybrid_search"></a>
Retrieval method that combines results from full-text search (usually BM25), and vector search. It captures both exact keyword matches and semantic similarity.

## LangGraph <a name="langgraph"></a>
LangGraph is a tool for building AI applications as a structured workflow, where each step performs a specific task (node), the application data is stored in a shared memory-like object (state), the transitions between steps define what happens next (edges), and saved progress makes it possible to return to an earlier moment or continue the process later (checkpoint). Key topics:
- state - a shared data object passed between steps in LangGraph:
``` python
class AgentState(TypedDict):
    message: str
    category: str
```

- node - a single step in a process, usually a function that reads the current state, performs a specific action, and returns data that should be added to or updated in the state:
``` python
def classify_message(state: AgentState):
    response = llm.invoke(
        f"Classify this message as technical or general: {state['message']}"
    )

    return {"category": response.content}
```

To exist as part of the workflow, the node must be added to the builder:
``` python
builder = StateGraph(AgentState)

builder.add_node("classify_message", classify_message)
```

- edges - define the flow of a LangGraph workflow. They connect nodes and specify which step should be executed next:
``` python
builder.add_edge("classify_message", "generate_answer") #after the node "classify_message" run the node "generate_answer"
```

there are also conditional edges which define branching logic in a LangGraph workflow. They choose the next node based on the current state:
``` python
def route_by_category(state: AgentState):
    if state["category"] == "technical":
        return "technical"
    return "general"

builder.add_conditional_edges(
    "classify_message",      # after this node, choose the next path
    route_by_category,       # function that checks state and returns a path name
    {
        "technical": "technical_answer",  # if it returns "technical", run node "technical_answer"
        "general": "general_answer",      # if it returns "general", run node "general_answer"
    }
)
```

- checkpoint — a saved snapshot of the current state, progress, and history of a LangGraph workflow during execution.It must be explicitly enabled to work. Once enabled, LangGraph saves checkpoints automatically during workflow execution.:
``` python
checkpointer = InMemorySaver()

graph = builder.compile(checkpointer=checkpointer)
# enables checkpointing
```

## MMR <a name="mmr"></a>
Maximal Marginal Relevance - a post-retrieval selection mechanism that reduces repetitive or highly similar chunks. It selects results that are both relevant to the query and diverse from each other.

## Reranking <a name="reranking"></a>
Reranking is a post-retrieval step in a RAG pipeline. Its purpose is to reorder the candidate documents or chunks returned by the retriever (top-k), from the most to the least relevant to the user’s query. Each user query + document/chunk pair is passed to a reranker, which assigns a relevance score to every pair. Based on these scores, the candidates are sorted again, and only the best-ranked chunks, called top-n results, are selected as context for the LLM. Reranking improves the quality of the final answer because retrieval is usually fast and approximate, while the reranker evaluates more precisely which chunks actually answer the user’s question.

## Scoring <a name="scoring"></a>
Mechanism for combining hybrid search results into one final ranking. An example is RRF (Reciprocal Rank Fusion), which uses document positions in the BM25 and vector search rankings to create a single final ranking.
