# Rate Limiter

This repository explores the systems design exercise to build a rate limiter. The limiter can be used to 
limit the amount of requests based on recognizing URI patterns, but also based on other parameters, such as 
originating IP address.

## Desirable Properties

### Highly Available Distributed Setup

We shouldn't have a rate limiter on just one instance to account for server failures or traffic spikes that one 
server couldn't handle anymore.

### Performance Sensitive

The implementation must have a minimal and preferably negligible effect on HTTP response times. If we had freedom of 
choice in our programming language, we should go for the most performant environment, such as C, C++, Rust, etc.

### Security

Optimally, the request is denied in a layer that has reduced data access permissions. If the rate limiter has no 
access no service database, the access to that data can also not be compromised by malicious actors

### Configurable implementation

There are multiple algorithms available that could be chosen:

- token bucket
- leaking bucket
- fixed window counter
- sliding window log
- sliding window counter

## Architecture

### Location

The limiter can be positioned as a proxy, or as an integral part of your API. To make both possible, the core of the 
logic can be implemented as a library that can either be part of a proxy or an API, even though initially we'll 
implement it as part of our API to limit the delay in our services.

