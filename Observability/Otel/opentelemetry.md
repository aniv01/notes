## What is Otel? OpenTracing + OpenCensus = :yellow_heart:

#### Why OpenTelemetry?
---
- Applications should be able to describe themselves in a standard way.
- Increased Observablity in a standard way.

### Data Sources
---
- Otel supports multiple data sources traces, metrics, logs (more will be added in future)

#### Traces
---
- Traces track the progression of a single request, called a trace, as it is handled by services that make up an application.
- Distributed tracing is a form of tracing that traverses process, network and security boundaries.
- Each unit of work in a trace is called a span; a trace is a tree of spans.
- A trace is comprised of the single root span and any number of child spans, which represent operations taking place as part of the request.
- Each span contains metadata about the operation, such as its name, start and end timestamps, attributes, events, and status.
- To create and manage spans in OpenTelemetry, the OpenTelemetry API provides the tracer interface.

#### Instrumentation
---
- In order to use OpenTelemetry your code has to be instrumented properly by using API's.
- There are instrumentation plugins available for common frameworks, http clients etc., they are called as auto instrumentation plugins.

#### What is the difference between the OpenTelemetry SDK and OpenTelemetry API?
---
- We install the OpenTelemetry SDK first in order to use OpenTelemetry.
- Then we have an API layer which contains only interfaces, we only interact with the SDK via the API.
- SDK implements the API.
- One advantage of this approach is that API the part remains intact even when the lower level SDK changes.
- We will not be touching the SDK part after installation, everything will go via API.

#### Transaction
---
- OpenTelemetry is all about distributed transactions.
- The core concept is context propagation.

#### What is a context propagation
---
- It is a way of propagating/sending context from one end to other.
- For example, we serialize and inject (eg: http headers) at one application, then on the other end we extact the context and use them and so on.. 

#### Tracing headers to HTTP spec (WIP)

- Work being done on W3C side to standardize http headers for tracing (Tracing headers)
- 