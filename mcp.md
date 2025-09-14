# Model Context Protocol (MCP)

## What is MCP?



## 


## Latest Update on the Specification

Model Context Protocol (MCP) is moving away from using Server-Sent Events (SSE) for its transport layer and is adopting Streamable HTTP. This change was introduced in the recent MCP specification update, which also included other improvements like an authorization framework and support for JSON-RPC batching. 

Why the Change?
- Simplified Transport:
Streamable HTTP uses a single, bidirectional endpoint, simplifying the communication model compared to SSE, which requires separate channels for sending and receiving data. 
- Improved Reliability:
Streamable HTTP offers more reliable connections and better error handling compared to the older SSE implementation. 
- Bidirectional Communication:
Streamable HTTP natively supports bidirectional communication, while SSE is primarily unidirectional (server-to-client). 
- Reduced Resource Usage:
Streamable HTTP can be more efficient in terms of resource usage, especially when dealing with long-lived connections. 
- Support for Stateless Servers:
Streamable HTTP enables the implementation of stateless MCP servers, where the server doesn't need to maintain persistent state between requests. 
- Better for Remote Hosting:
Streamable HTTP is better suited for remote hosting scenarios, as it allows for more flexible and efficient communication with remote MCP servers. 


## References

- https://arxiv.org/html/2504.16736v2#S4
