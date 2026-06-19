# LLM
- [Advanced Prompting Techniques](#advanced_prompting_techniques)
- [Agent system testing](#agent_system_testing)
- [LangGraph](#langgraph)

## Advanced Prompting Techniques <a name="advanced_prompting_techniques"></a>
- Few-Shot Learning - you give model a few examples
- Chain-of-Thought - the method involves guiding the model through step-by-step reasoning to help it solve complex tasks more effectively
- Role-playing - assigning a specific role to the model and/or defining the user’s role or target audience.
- Temperature, Top-p - Temperature controls how boldly the model chooses between possible outputs (higher = more creative), while top-p controls how many possible outputs are considered in the first place.

## Agent system testing <a name="agent_system_testing"></a>
- Task-based evaluation - Evaluate whether an agent correctly completes predefined tasks from input to final output, usually using a golden dataset.
- Tool-use validation - Check whether the agent correctly selects and calls tools (APIs, functions, databases), including correct arguments and execution order.
- Adversarial testing - Test robustness of agents against malicious, ambiguous, or edge-case inputs (e.g., prompt injection, misleading instructions).

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