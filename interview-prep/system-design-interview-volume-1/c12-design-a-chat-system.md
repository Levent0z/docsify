# Design a Chat System

> This is a summary of Chapter 2 1of [System Design Interview Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/).

## Requirements

- 1-1 or group-based?
- Mobile/web/both
- Scale (DAU)
- Limits:
  - Group-chat members?
  - Message length?
- Features? Text-only, files, online indicator, encryption?
- Message persistence?

## High-level Design

sender --> chat service --> receiver

Chat service stores and relays the mssage

For client-initiated messages, HTTP with **keep-alive** is enough.
For server-initiated messages, can use polling (by the client), long-polling (keep open until a response, then ask aagain) or WebSocket

Long-polling may not be suitable because:
- HTTP servers are typically stateless and the server that receives a message may be different than the one the receiver is connected to.
- Server has no good way to tell if client is disconnected.
- inefficient

WS is great for communication for messages but not everything needs to be WS.

Service discovery: provides a list of DNS host names of destinations
