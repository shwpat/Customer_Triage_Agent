### A simple way to explain the coding steps in the presentation

I can summarize my code in **8 steps**:

1. **Import packages** → Bring in LangChain, CSV, and file-path tools.
2. **Set file paths** → Tell Python where `order.csv`, `return_policy.txt`, and `tool_log.txt` are.
3. **Create logging** → Record every tool call.
4. **Create tools** → Build order lookup, policy lookup, and refund tools.
5. **Add human approval** → Require a person to approve refunds.
6. **Create the agent** → Give the LLM access to all three tools.
7. **Take customer input** → Send the customer's question to the agent.
8. **Show the result and trace** → Display the final answer and what tools the agent used.
