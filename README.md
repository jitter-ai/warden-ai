# Warden AI

## Executive summary

Warden AI watches every <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/argo-cd.svg" width="18" alt=""> [Argo CD](https://argo-cd.readthedocs.io) deployment event on a self-hosted Kubernetes cluster and keeps problems from sitting unseen: each event is sent to the <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/victorialogs.svg" width="18" alt=""> [VictoriaLogs](https://victoriametrics.com/products/victorialogs/) log store with every hop on the way checked, so a broken one is named, and a <img src="https://cdn.simpleicons.org/langgraph" width="18" alt=""> [LangGraph](https://langchain-ai.github.io/langgraph/) team of seven agent roles (receive, analyze, research, respond, fix, review, log), with <img src="https://cdn.simpleicons.org/langchain" width="18" alt=""> [LangChain](https://python.langchain.com) tool calls into <img src="https://cdn.simpleicons.org/modelcontextprotocol" width="18" alt=""> [Model Context Protocol](https://modelcontextprotocol.io) tools, reads it. Healthy events are logged and dropped, and problems are researched, given a proposed fix and reviewed before a person is asked to act; nothing risky happens on its own.

- **Mission Control** lists the open problems worst first, shows each event moving through the seven agent roles, and stores every step in <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/opensearch.svg" width="18" alt=""> [OpenSearch](https://opensearch.org) so any decision can be traced afterward.

## In action

**Watch deployment events move through the agents.** Each event passes the seven <img src="https://cdn.simpleicons.org/langgraph" width="18" alt=""> [LangGraph](https://langchain-ai.github.io/langgraph/) agent roles on Mission Control.

![Deployment events moving through the seven LangGraph agents on Mission Control](assets/mission-control-demo.gif)

The clip is recorded on demo data.

## Architecture

Warden AI is one web page on a self-hosted Kubernetes cluster, kept in step with git by <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/argo-cd.svg" width="18" alt=""> [Argo CD](https://argo-cd.readthedocs.io), which also deploys the <img src="https://cdn.simpleicons.org/langgraph" width="18" alt=""> [LangGraph](https://langchain-ai.github.io/langgraph/) and <img src="https://cdn.simpleicons.org/langchain" width="18" alt=""> [LangChain](https://python.langchain.com) agents and the <img src="https://cdn.simpleicons.org/modelcontextprotocol" width="18" alt=""> [Model Context Protocol](https://modelcontextprotocol.io) tools they call through the <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/toolhive.svg" width="18" alt=""> [ToolHive](https://github.com/stacklok/toolhive) gateway:

- **Web UI.** The <img src="https://cdn.simpleicons.org/react" width="18" alt=""> [React](https://vite.dev) page and its <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/fastapi.svg" width="18" alt=""> [FastAPI](https://fastapi.tiangolo.com) backend ship together to Kubernetes through <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/argo-cd.svg" width="18" alt=""> [Argo CD](https://argo-cd.readthedocs.io).
- **Data pipeline.** <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/argo-cd.svg" width="18" alt=""> [Argo CD](https://argo-cd.readthedocs.io) sends each deployment event to <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/victorialogs.svg" width="18" alt=""> [VictoriaLogs](https://victoriametrics.com/products/victorialogs/), which holds the event logs, and <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/opensearch.svg" width="18" alt=""> [OpenSearch](https://opensearch.org) stores every agent step.
- **AI.** <img src="https://cdn.simpleicons.org/langgraph" width="18" alt=""> [LangGraph](https://langchain-ai.github.io/langgraph/) and <img src="https://cdn.simpleicons.org/langchain" width="18" alt=""> [LangChain](https://python.langchain.com) run the seven agent roles, and the <img src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/toolhive.svg" width="18" alt=""> [ToolHive](https://github.com/stacklok/toolhive) gateway fronts the <img src="https://cdn.simpleicons.org/modelcontextprotocol" width="18" alt=""> [Model Context Protocol](https://modelcontextprotocol.io) tool servers they call.
- **Credentials.** Every key comes from a password manager at run time; none is in the code or the images.

## License

PolyForm Noncommercial 1.0.0 with a required notice from Haya Tech LLC. Noncommercial use is free; any commercial use, including resale, hosting for others, or a paid product, needs a written license from Haya Tech LLC first. See [LICENSE](LICENSE).
