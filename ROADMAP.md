# Roadmap

The plan: all lessons, in learning order.
Progress is tracked in [PROGRESS.md](PROGRESS.md), not here.

Lesson ID = `tier.area.lesson` (e.g. `1.03.04`). The folder is `<tier folder>/<area folder>/<NN>-<kebab-case-title>/`.

| Tier | What it is | Lessons |
|---|---|---|
| 1 · Core | Used almost every day. Learn deeply, in order. | 83 |
| 2 · Growth | What takes you from junior to mid and senior. | 123 |
| 3 · Awareness | Know it exists and when it matters. Short lessons. | 64 |
| **Total** | | **270** |

**Suggested pace:** 1–2 lessons per weekday.
- Tier 1 takes about 2–3 months.
- Tier 2 runs alongside real work after that.
- Tier 3 is for whenever you're curious or a topic shows up at work.

---

# Tier 1 · Core
`tier-1-core/`

### 1.01 Computer basics
`tier-1-core/01-computer-basics/`
- **1.01.01** How a computer runs a program: CPU, memory, storage, and what "running code" really means.
- **1.01.02** Bits, bytes and text: how numbers and text (Unicode, UTF-8) are stored as bytes.
- **1.01.03** Operating systems, processes and threads: what the OS does and how many programs run at once.

### 1.02 Developer tools
`tier-1-core/02-developer-tools/`
- **1.02.01** The terminal and the shell: running commands, moving around folders, pipes and redirection.
- **1.02.02** Files, permissions and environment variables: paths, who can read/write/run, and settings passed to programs.
- **1.02.03** Installing tools with mise: install and pin versions of languages and CLI tools per project.
- **1.02.04** Code editor essentials: navigating, searching and editing code fast in a modern editor.
- **1.02.05** Markdown: writing READMEs, docs and notes (like these lessons).
- **1.02.06** Git basics: repositories, commits and history, and why version control matters.
- **1.02.07** Git branches, merging and rebasing: working in parallel and resolving conflicts.
- **1.02.08** GitHub and pull requests: remotes, push/pull, pull requests and issues.

### 1.03 Python
`tier-1-core/03-python/`
- **1.03.01** First steps in Python: running code, values, variables, basic types and strings.
- **1.03.02** Control flow: if/else, loops and boolean logic.
- **1.03.03** Functions: parameters, return values, scope and small focused functions.
- **1.03.04** Built-in collections: lists, tuples, dicts and sets, and when to use each.
- **1.03.05** Errors and exceptions: raising, catching and designing helpful errors.
- **1.03.06** Modules, packages and dependencies: imports, project layout, pyproject.toml, virtual environments and uv.
- **1.03.07** Classes and objects: object-oriented basics, and composition vs inheritance.
- **1.03.08** Type hints: describing types in code and checking them automatically.
- **1.03.09** Iterators, generators and comprehensions: clean, memory-friendly ways to process data.
- **1.03.10** Files and data formats: reading and writing files, JSON and CSV.
- **1.03.11** Dates and times: UTC, time zones, ISO 8601 and the classic time bugs.

### 1.04 Data structures and algorithms
`tier-1-core/04-data-structures-and-algorithms/`
- **1.04.01** Big-O: how the time and memory a piece of code needs grow with input size.
- **1.04.02** Arrays and lists: how lists work inside and what each operation costs.
- **1.04.03** Hash tables: how dicts and sets find things almost instantly.
- **1.04.04** Stacks and queues: last-in-first-out and first-in-first-out, and where they appear in real systems.
- **1.04.05** Recursion: functions that call themselves, and their limits.
- **1.04.06** Trees: hierarchical data, from file systems to search trees.
- **1.04.07** Graphs, BFS and DFS: modeling connections and searching through them.
- **1.04.08** Sorting and binary search: built-in sorting, stability, and finding things fast in sorted data.

### 1.05 Clean code
`tier-1-core/05-clean-code/`
- **1.05.01** Readable code: naming, small functions, and code that explains itself.
- **1.05.02** Simple design principles: DRY, KISS, YAGNI and separation of concerns.
- **1.05.03** Comments and documentation: what to write down, docstrings and good READMEs.
- **1.05.04** Formatting and linting: automatic style and bug checks (e.g. Ruff).
- **1.05.05** Refactoring basics: improving code safely, in small steps.

### 1.06 Testing
`tier-1-core/06-testing/`
- **1.06.01** Why we test: kinds of tests and the test pyramid.
- **1.06.02** Unit tests with pytest: writing, running and organizing tests.
- **1.06.03** Test doubles: mocks, stubs and fakes, and when not to use them.
- **1.06.04** Integration tests: testing code together with real databases and services.
- **1.06.05** Writing testable code: designing code that is easy to test.

### 1.07 Debugging
`tier-1-core/07-debugging/`
- **1.07.01** Reading errors and stack traces: finding where and why code failed.
- **1.07.02** Using a debugger: breakpoints, stepping through code and inspecting values.
- **1.07.03** A debugging method: reproduce, isolate, form a hypothesis, fix, verify.
- **1.07.04** Logging: log levels, useful messages and structured logs.

### 1.08 Networking and the web
`tier-1-core/08-networking-and-the-web/`
- **1.08.01** How the internet works: IP addresses, ports, packets, TCP and UDP.
- **1.08.02** DNS: how names like github.com become IP addresses.
- **1.08.03** HTTP: requests, responses, methods, status codes and headers.
- **1.08.04** HTTPS and TLS: how encryption and certificates protect traffic.
- **1.08.05** What happens when you open a URL: everything so far, tied together step by step.

### 1.09 APIs
`tier-1-core/09-apis/`
- **1.09.01** What an API is: contracts between programs.
- **1.09.02** JSON and serialization: turning data into text and back.
- **1.09.03** REST API design: resources, methods, status codes and naming.
- **1.09.04** Building an API with FastAPI: a small working web API in Python.
- **1.09.05** Calling APIs from Python: HTTP clients, timeouts, retries and error handling.
- **1.09.06** Pagination, versioning and idempotency: the details that make APIs safe to use and change.

### 1.10 Databases
`tier-1-core/10-databases/`
- **1.10.01** What a database is: why not just files, and the main kinds of databases.
- **1.10.02** Tables, keys and relationships: the relational model.
- **1.10.03** SQL basics: SELECT, WHERE, ORDER BY, INSERT, UPDATE and DELETE.
- **1.10.04** SQL joins and aggregations: combining tables and summarizing data.
- **1.10.05** Indexes: how databases find rows fast, and what indexes cost.
- **1.10.06** Transactions and ACID: keeping data correct when things fail.
- **1.10.07** Database design: normalization, and when to break the rules.
- **1.10.08** Databases from Python: drivers, ORMs, connection pools and the N+1 problem.
- **1.10.09** Schema migrations: changing a live database safely.

### 1.11 Security
`tier-1-core/11-security/`
- **1.11.01** The security mindset: threats, attack surface and the OWASP Top 10.
- **1.11.02** Authentication: passwords, hashing, sessions, tokens and MFA.
- **1.11.03** Authorization: who can do what, with roles and permissions.
- **1.11.04** Common web attacks: injection, XSS and CSRF, and how to stop them.
- **1.11.05** Secrets: keeping API keys and passwords out of code and logs.

### 1.12 Shipping software
`tier-1-core/12-shipping-software/`
- **1.12.01** Environments and configuration: dev, staging, prod, and config that lives outside the code.
- **1.12.02** Containers with Docker: images, containers, Dockerfiles and Compose.
- **1.12.03** Continuous integration: automatic checks on every change (e.g. GitHub Actions).
- **1.12.04** Deployment basics: continuous delivery, releases and rollbacks.
- **1.12.05** Cloud basics: what the cloud is, core services, regions and pricing.

### 1.13 Running in production
`tier-1-core/13-running-in-production/`
- **1.13.01** Observability basics: logs, metrics and traces, and what each one tells you.
- **1.13.02** Monitoring and alerting: knowing something is wrong before users tell you.
- **1.13.03** Handling incidents: what to do when production breaks, and learning from it.

### 1.14 Working in a team
`tier-1-core/14-working-in-a-team/`
- **1.14.01** How software teams work: Agile, Scrum and Kanban in practice.
- **1.14.02** From task to done: breaking work down and estimating it.
- **1.14.03** Code review: reviewing others' code and getting yours reviewed.
- **1.14.04** Writing for engineers: good commits, tickets, PR descriptions and messages.
- **1.14.05** Getting unblocked: asking good questions and learning fast on the job.
- **1.14.06** Working with AI coding assistants: using them well and checking their work.

---

# Tier 2 · Growth
`tier-2-growth/`

### 2.01 Python deeper
`tier-2-growth/01-python-deeper/`
- **2.01.01** How Python runs your code: interpreter, bytecode, memory and garbage collection.
- **2.01.02** Decorators and context managers: reusable wrappers and safe resource handling.
- **2.01.03** Data classes and validation: structured data with dataclasses and Pydantic.
- **2.01.04** Regular expressions: matching and extracting text patterns.
- **2.01.05** Threads and processes in Python: running work in parallel, and the GIL.
- **2.01.06** Async and await: event loops and asyncio for I/O-heavy code.

### 2.02 Algorithms deeper
`tier-2-growth/02-algorithms-deeper/`
- **2.02.01** Heaps and priority queues: top-K problems and scheduling.
- **2.02.02** Problem-solving patterns: two pointers, sliding window and prefix sums.
- **2.02.03** Dynamic programming: solving problems by reusing smaller answers.
- **2.02.04** Greedy algorithms: when the best local choice is also the best overall.

### 2.03 Operating systems and Linux
`tier-2-growth/03-operating-systems-and-linux/`
- **2.03.01** Memory: stack, heap and virtual memory.
- **2.03.02** File systems and I/O: how reads, writes, buffering and fsync really work.
- **2.03.03** Linux for engineers: processes, services, logs and resource tools.
- **2.03.04** Shell scripting: automating tasks safely with Bash.

### 2.04 Concurrency
`tier-2-growth/04-concurrency/`
- **2.04.01** Concurrency vs parallelism: doing many things at once vs at the same time.
- **2.04.02** Race conditions and locks: shared state, mutexes and semaphores.
- **2.04.03** Deadlocks and other traps: deadlock, livelock, starvation and how to avoid them.
- **2.04.04** Producer–consumer and backpressure: keeping fast producers from overwhelming slow consumers.

### 2.05 Software design
`tier-2-growth/05-software-design/`
- **2.05.01** SOLID principles: five rules for code that is easy to change.
- **2.05.02** Design patterns you will actually use: the handful that show up in real codebases.
- **2.05.03** Dependency injection: decoupling code from how its dependencies are created.
- **2.05.04** Functional programming ideas: pure functions, immutability and higher-order functions.
- **2.05.05** Domain-driven design basics: modeling software around the business.
- **2.05.06** Designing good interfaces and libraries: easy-to-use APIs and backward compatibility.
- **2.05.07** Working with legacy code: changing old, untested code safely.
- **2.05.08** Technical debt: when to take it on, how to track it, how to pay it back.

### 2.06 Software architecture
`tier-2-growth/06-software-architecture/`
- **2.06.01** Monoliths and microservices: the trade-offs, and the modular monolith in between.
- **2.06.02** Layered and clean architecture: keeping business logic independent of frameworks.
- **2.06.03** Event-driven architecture: services talking through events.
- **2.06.04** Architecture trade-offs: scalability, reliability, cost and Conway's law.
- **2.06.05** Documenting architecture: decision records (ADRs) and diagrams (C4).

### 2.07 Databases deeper
`tier-2-growth/07-databases-deeper/`
- **2.07.01** Advanced SQL: subqueries, CTEs and window functions.
- **2.07.02** Query performance: reading EXPLAIN plans and fixing slow queries.
- **2.07.03** Isolation levels and locking: concurrent transactions and MVCC.
- **2.07.04** NoSQL databases: key-value, document, wide-column and graph stores.
- **2.07.05** Caching with Redis: cache-aside, TTLs and invalidation.
- **2.07.06** Replication and sharding: copying and splitting data across machines.
- **2.07.07** Backups and disaster recovery: RPO, RTO and restores you have actually tested.
- **2.07.08** Search engines: full-text search and how it differs from SQL.

### 2.08 Distributed systems
`tier-2-growth/08-distributed-systems/`
- **2.08.01** Why distributed systems are hard: the fallacies of distributed computing.
- **2.08.02** CAP and consistency models: strong vs eventual consistency.
- **2.08.03** Message queues and event streaming: queues, topics, Kafka-style logs.
- **2.08.04** Background jobs and scheduled tasks: moving slow work out of requests with workers, task queues and cron.
- **2.08.05** Delivery guarantees and idempotency: at-least-once, exactly-once, and safe retries.
- **2.08.06** Resilience patterns: timeouts, retries with backoff, circuit breakers and load shedding.
- **2.08.07** Rate limiting: protecting services with token buckets and friends.
- **2.08.08** Distributed transactions: sagas and the outbox pattern.
- **2.08.09** Consistent hashing: spreading data across nodes that come and go.

### 2.09 System design
`tier-2-growth/09-system-design/`
- **2.09.01** How to approach system design: requirements, estimates and trade-offs.
- **2.09.02** Scaling: vertical vs horizontal, stateless services and load balancers.
- **2.09.03** Caching at every layer: browser, CDN, application and database.
- **2.09.04** High availability: redundancy, failover and multi-region.
- **2.09.05** Case study: URL shortener, a full design from start to end.
- **2.09.06** Case study: notification system, with queues, retries and fan-out in practice.
- **2.09.07** Cost-aware design: building systems the business can afford.

### 2.10 APIs deeper
`tier-2-growth/10-apis-deeper/`
- **2.10.01** API specs and contract-first design: OpenAPI and generated clients.
- **2.10.02** GraphQL: client-shaped queries, and when it fits.
- **2.10.03** gRPC and Protocol Buffers: fast, typed service-to-service calls.
- **2.10.04** Webhooks: event callbacks with signing and retries.
- **2.10.05** Real-time communication: WebSockets, Server-Sent Events and polling.

### 2.11 Cloud and infrastructure
`tier-2-growth/11-cloud-and-infrastructure/`
- **2.11.01** Core cloud services: compute, storage, databases and queues on a major cloud.
- **2.11.02** Cloud networking: VPCs, subnets, security groups and private access.
- **2.11.03** Identity and access management: least privilege in the cloud.
- **2.11.04** Infrastructure as code: defining infrastructure in files (e.g. Terraform/OpenTofu).
- **2.11.05** Kubernetes basics: pods, deployments, services and why teams use it.
- **2.11.06** Serverless: functions as a service, and when they fit.

### 2.12 Delivery deeper
`tier-2-growth/12-delivery-deeper/`
- **2.12.01** Deployment strategies: rolling, blue-green and canary releases.
- **2.12.02** Feature flags: separating deploy from release.
- **2.12.03** Versioning and releases: semantic versioning, changelogs and release processes.
- **2.12.04** Monorepos and polyrepos: organizing code across many projects.

### 2.13 Reliability and observability
`tier-2-growth/13-reliability-and-observability/`
- **2.13.01** Metrics and dashboards: what to measure (RED, USE) and how to show it.
- **2.13.02** Distributed tracing: following one request across services (OpenTelemetry).
- **2.13.03** SLIs, SLOs and error budgets: defining "reliable enough".
- **2.13.04** On-call and alerting: alerts worth waking up for, and runbooks.
- **2.13.05** Blameless postmortems: learning from failures without blaming people.
- **2.13.06** Health checks and graceful degradation: staying partly up when parts fail.

### 2.14 Performance
`tier-2-growth/14-performance/`
- **2.14.01** Profiling: finding where code spends time and memory.
- **2.14.02** Latency and bottlenecks: percentiles (p50/p95/p99) and finding the real constraint.
- **2.14.03** Load testing: checking how a system behaves under heavy traffic.
- **2.14.04** Memory leaks: finding and fixing memory that keeps growing.

### 2.15 Security deeper
`tier-2-growth/15-security-deeper/`
- **2.15.01** OAuth 2.0 and OpenID Connect: "log in with…" and delegated access.
- **2.15.02** Cryptography for engineers: hashing, encryption, signatures, and what not to build yourself.
- **2.15.03** Threat modeling: finding security risks during design.
- **2.15.04** Supply chain security: dependencies, scanning, SBOMs and signed builds.
- **2.15.05** Privacy and GDPR: handling personal data responsibly.

### 2.16 Testing deeper
`tier-2-growth/16-testing-deeper/`
- **2.16.01** Test-driven development: writing the test first, and when it helps.
- **2.16.02** End-to-end tests: testing full user flows in a real browser.
- **2.16.03** Contract testing: making sure services agree on their APIs.
- **2.16.04** Property-based testing: letting the computer generate test cases.
- **2.16.05** Flaky tests: why tests fail randomly and how to fix them.

### 2.17 Frontend essentials
`tier-2-growth/17-frontend-essentials/`
- **2.17.01** HTML, CSS and JavaScript: the building blocks of web pages.
- **2.17.02** How browsers render pages: from HTML to pixels.
- **2.17.03** Frontend frameworks: components and state, with React as the example.
- **2.17.04** Browser security: same-origin policy, CORS, CSP and cookies.
- **2.17.05** Web performance: Core Web Vitals and making pages fast.
- **2.17.06** Accessibility: building apps everyone can use.

### 2.18 Data engineering
`tier-2-growth/18-data-engineering/`
- **2.18.01** Data pipelines: ETL and ELT.
- **2.18.02** Batch and stream processing: processing data in chunks vs as it arrives.
- **2.18.03** Data warehouses and lakehouses: storing data for analytics.
- **2.18.04** Analytics and A/B testing: tracking events and running experiments correctly.

### 2.19 AI engineering
`tier-2-growth/19-ai-engineering/`
- **2.19.01** How LLMs work: tokens, context windows and generation.
- **2.19.02** Prompt engineering: getting reliable results from models.
- **2.19.03** Embeddings and vector search: finding things by meaning.
- **2.19.04** Retrieval-augmented generation: grounding answers in your own data.
- **2.19.05** AI agents and tool use: function calling, MCP and multi-step agents.
- **2.19.06** Evaluating AI features: measuring quality with evals.
- **2.19.07** AI risks: hallucination, prompt injection and data leaks.

### 2.20 Cross-cutting concerns
`tier-2-growth/20-cross-cutting-concerns/`
- **2.20.01** Internationalization and localization: languages, formats and Unicode done right.
- **2.20.02** Money and numbers: floats vs decimals, and rounding.
- **2.20.03** Audit logs and data retention: who did what, and how long to keep data.

### 2.21 Technical leadership
`tier-2-growth/21-technical-leadership/`
- **2.21.01** Ownership: caring about outcomes, end to end.
- **2.21.02** Thinking in trade-offs: there are no perfect solutions, only good choices.
- **2.21.03** Design docs and RFCs: proposing and reviewing big changes in writing.
- **2.21.04** Technical writing: clear docs that people actually read.
- **2.21.05** Talking to non-engineers: explaining technical things in business terms.
- **2.21.06** Prioritization: impact vs effort, and saying no.
- **2.21.07** Planning bigger projects: milestones, risks and estimates you can trust.
- **2.21.08** Influence without authority: getting alignment across teams.
- **2.21.09** Mentoring: helping other engineers grow.
- **2.21.10** Feedback: giving and receiving it well.

### 2.22 Product and business
`tier-2-growth/22-product-and-business/`
- **2.22.01** How the business makes money: why engineers should understand it.
- **2.22.02** Metrics that matter: KPIs and measuring the impact of your work.
- **2.22.03** Build vs buy: when not to write code.

---

# Tier 3 · Awareness
`tier-3-awareness/`

### 3.01 Computer science theory
`tier-3-awareness/01-computer-science-theory/`
- **3.01.01** CPU caches and computer architecture: why memory access patterns matter for speed.
- **3.01.02** Compilers and interpreters: how source code becomes something a machine runs.
- **3.01.03** Automata and formal languages: the theory behind regex and parsers.
- **3.01.04** P vs NP: why some problems have no known fast solution.
- **3.01.05** Math for engineers: the probability, statistics and linear algebra you'll meet.

### 3.02 Advanced data structures
`tier-3-awareness/02-advanced-data-structures/`
- **3.02.01** Tries: prefix trees for autocomplete.
- **3.02.02** Union-find: tracking groups that merge.
- **3.02.03** Bloom filters and sketches: approximate answers using tiny memory.
- **3.02.04** B-trees and LSM trees: the structures inside databases.
- **3.02.05** Skip lists: a simple alternative to balanced trees.
- **3.02.06** Segment trees and Fenwick trees: fast range queries.
- **3.02.07** Persistent data structures: data that keeps its old versions.

### 3.03 Advanced algorithms
`tier-3-awareness/03-advanced-algorithms/`
- **3.03.01** Shortest paths and spanning trees: Dijkstra, A* and MST.
- **3.03.02** String algorithms: fast search, edit distance and rolling hashes.
- **3.03.03** Randomized algorithms: using randomness on purpose (sampling, shuffling).
- **3.03.04** Cache eviction: LRU, LFU and friends.

### 3.04 Distributed systems theory
`tier-3-awareness/04-distributed-systems-theory/`
- **3.04.01** Consensus: how Raft and Paxos make machines agree.
- **3.04.02** Time and ordering: clock skew, Lamport and vector clocks.
- **3.04.03** Gossip protocols: spreading information like rumors.
- **3.04.04** CRDTs: data that merges without conflicts.
- **3.04.05** Coordination services: etcd and ZooKeeper for locks and config.
- **3.04.06** Split brain and fencing: when two nodes both think they're the leader.
- **3.04.07** Peer-to-peer and blockchains: networks with no central server, and where blockchains fit.

### 3.05 Architecture patterns
`tier-3-awareness/05-architecture-patterns/`
- **3.05.01** CQRS and event sourcing: separate reads and writes, and state as a log of events.
- **3.05.02** Multi-tenancy: serving many customers from one system.
- **3.05.03** Micro-frontends: splitting a frontend across teams.
- **3.05.04** Plugin architectures: systems others can extend.
- **3.05.05** Service mesh: managing traffic between services.
- **3.05.06** The Twelve-Factor App: classic rules for cloud-ready apps.

### 3.06 Programming languages
`tier-3-awareness/06-programming-languages/`
- **3.06.01** A tour of other languages: what Go, Rust, Java, C# and TypeScript are good at.
- **3.06.02** Type systems: static vs dynamic, strong vs weak, generics.
- **3.06.03** Memory management models: manual, RAII, reference counting and GC.
- **3.06.04** Metaprogramming: code that inspects or writes code.
- **3.06.05** Actors and channels: other ways to do concurrency.

### 3.07 Networking deeper
`tier-3-awareness/07-networking-deeper/`
- **3.07.01** HTTP/2 and HTTP/3: faster HTTP and QUIC.
- **3.07.02** Load balancers in depth: layer 4 vs layer 7.
- **3.07.03** Proxies and reverse proxies: what sits between clients and servers.
- **3.07.04** Network debugging tools: curl, dig, traceroute, tcpdump and Wireshark.
- **3.07.05** IP networking details: subnets, CIDR, NAT and IPv6.

### 3.08 Infrastructure extras
`tier-3-awareness/08-infrastructure-extras/`
- **3.08.01** Virtual machines: hypervisors, and VMs vs containers.
- **3.08.02** Configuration management: tools like Ansible.
- **3.08.03** GitOps: Git as the source of truth for deployments.
- **3.08.04** Chaos engineering: breaking things on purpose to build confidence.

### 3.09 Testing extras
`tier-3-awareness/09-testing-extras/`
- **3.09.01** Mutation testing: testing your tests.
- **3.09.02** Fuzzing: random inputs to find crashes and security bugs.
- **3.09.03** Behavior-driven development: specs in plain language.
- **3.09.04** Snapshot testing: catching unexpected output changes.

### 3.10 Security extras
`tier-3-awareness/10-security-extras/`
- **3.10.01** Zero trust: never trust the network, verify every request.
- **3.10.02** Security testing: SAST, DAST and penetration tests.
- **3.10.03** Compliance frameworks: SOC 2, ISO 27001, PCI DSS and HIPAA in one page.

### 3.11 Data and ML extras
`tier-3-awareness/11-data-and-ml-extras/`
- **3.11.01** Columnar data formats: Parquet and why analytics loves it.
- **3.11.02** Time-series and geospatial databases: storing metrics over time and data on maps.
- **3.11.03** Data quality and lineage: trusting your data.
- **3.11.04** Machine learning basics: training, inference and evaluation.
- **3.11.05** MLOps: deploying and monitoring models.

### 3.12 Other platforms
`tier-3-awareness/12-other-platforms/`
- **3.12.01** Native vs cross-platform: Swift/Kotlin vs Flutter/React Native.
- **3.12.02** Mobile app constraints: app lifecycle, offline use, battery and app-store releases.
- **3.12.03** Embedded, IoT and real-time systems: software on small devices with tight limits on memory, power and timing.
- **3.12.04** WebAssembly and GPUs: fast compiled code in the browser, and massively parallel work on graphics cards.

### 3.13 The engineering profession
`tier-3-awareness/13-engineering-profession/`
- **3.13.01** Open-source licenses: MIT, Apache, GPL and what they require.
- **3.13.02** Engineering ethics: privacy, fairness and the impact of what you build.
- **3.13.03** Hiring and interviewing: how tech interviews work from both sides.
- **3.13.04** Engineering metrics: DORA metrics and their limits.
- **3.13.05** Engineering culture: what makes teams great to work in.
