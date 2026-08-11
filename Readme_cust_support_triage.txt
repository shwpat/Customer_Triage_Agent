I selected Customer triage for this project and used orders.csv and return_policy.txt for synthetic data as per instructions not to hard code the values. I created virtual environment using python -m venv .venv command and then activated virtual environment using .\.ven\Scripts\Activate.ps1. Next I installed required packages using this command pip install langchain, langchain-deepseek. Next I imported all the required packages using import command which is shown in 1st cell of my Jupyter notebook. Now I am all set. Then I gave the location of the file by setting the path shown in cell 2 of Jupyter Notebook. BASE_DIR finds the folder where the Python program is located. Then I created a login function for tracking the agent's actions shown in cell 3. Logging helps us see:
Which tool was used
What information was given to the tool
What result the tool returned. The information is saved in tool_log.txt. I decided to create 3 tools. 

First one is: lookup_order. The customer provides an order ID, the tool opens the CSV file the program checks each row in the CSV then the program compares the customer's order ID with the order IDs in the CSV until it finds the matching order. When an order is found, the program creates a readable result.After finding the order, the tool records the action. And saves the tool name, order ID, and result in tool_log.txt. This tool is shown in cell 4 of my notebook. If the order is not found the tool returns order not found. The @tool decorator tells LangChain that this function can be used by the AI agent.

Second tool is: check_return_policy. This tool answers questions about company policies like returns, refunds, cancellations, shipping etc. The tool reads the actual policy file. Instead of hardcoding the company's policy in the Python code, the policy is stored separately in return_policy.txt which makes it easier to update the policy later. The customer's question and the policy are combined.The tool then logs the result and the policy information is returned to the AI agent. The code is in cell no 5 of the notebook.

Third tool is:request_refund. This tool handles refund requests.  
Refunds are considered a high-risk action. So I added human approval to the program. If the user enters "yes" then only the request can be approved. The code is in cell no 6 of Jupyter Notebook.

Then I set up the Deep-Seek Model. Code is in cell 7 of notebook
Then I created the agent using the code which connects the Deep-Seek model with the three tools. Code is shown in cell 8 of notebook.
Then I set up the system prompt. The system prompt tells the AI how it should behave. Then I set up the rules, because the system prompt provides the agent with its role and rules, it helps the agent select the correct tool.
The project includes a function called:"def print_trace(messages)", this displays what happened during the agent's execution. The trace helps us understand the agent's workflow. Code is in cell 9 of the notebook.
The code checks whether the AI requested a tool with this code: "if getattr(message, "tool_calls", None):". If a tool was requested, it prints the tool name and arguments. This shows that the AI selected the correct tool. The code also checks for a ToolMessage using this code "elif label == "ToolMessage":". It displays the result returned by the tool. Then the main() function starts the application. The program asks the customer for input. The question is stored in:"user_input". Then the question is sent to the agent using "agent.invoke". The AI analyzes the question and decides which tool to use. Then the final answer is displayed. Code is shown in cell 10 of the notebook.  Then I created the final main() function to run the program in cell 11 of Jupyter notebook. The tool activity is saved in tool_log.txt which is automatically generated when the tool is called. 

Overall workflow: 
Customer -> Question -> Deepseek AI Agent -> Choose Tool -> lookup_order(orders.csv)?/ check_return_policy(return_policy.txt)?/ request_refund (yes/no)[Human Apprval]?     -> Tool Result -> DeepSeek -> Final Answer -> Customer.

 To conclude, I built a LangChain customer support agent using DeepSeek that can look up synthetic order information from a CSV file, answer policy questions from a text file, and handle refund requests with human approval.
