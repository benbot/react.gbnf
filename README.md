# Hi there!

This repository contains a specialized grammar file designed specifically for use with llama.cpp. The primary purpose of this grammar file is to restrict and guide the output of llama.cpp to adhere strictly to a React prompt format. This ensures that the outputs are not only syntactically correct but also contextually aligned with the requirements of React-based applications.


## Langchain example
```
import os
from grammar import grammar
from langchain_community.llms import LlamaCpp
from langchain_community.tools.wikipedia.tool import WikipediaQueryRun
from langchain_community.utilities.wikipedia import WikipediaAPIWrapper
from langchain import hub
from langchain.agents import create_react_agent, AgentExecutor

grammar_path = "/path/to/react.gbnf"

prompt = hub.pull("hwchase17/react")

llm = LlamaCpp(grammar_path=grammar_path, model_path="/path/to/model.gguf")

tools = [WikipediaQueryRun(api_wrapper=WikipediaAPIWrapper())]
agent = create_react_agent(llm, tools, prompt)

executor = AgentExecutor(agent=agent, tools=tools, verbose=True)

resp = executor.invoke({"input": "What is a platypus?"})
print(resp)
```

## Citations
```
@misc{yao2023react,
      title={ReAct: Synergizing Reasoning and Acting in Language Models}, 
      author={Shunyu Yao and Jeffrey Zhao and Dian Yu and Nan Du and Izhak Shafran and Karthik Narasimhan and Yuan Cao},
      year={2023},
      eprint={2210.03629},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```
