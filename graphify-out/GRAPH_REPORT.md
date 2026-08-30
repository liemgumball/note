# Graph Report - .  (2026-08-13)

## Corpus Check
- Large corpus: 184 files · ~915,208 words. Semantic extraction will be expensive (many Claude tokens). Consider running on a subfolder, or use --no-semantic to run AST-only.

## Summary
- 407 nodes · 522 edges · 26 communities detected
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 42 edges (avg confidence: 0.78)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Web Dev Beginner Path|Web Dev Beginner Path]]
- [[_COMMUNITY_Backend Frameworks (DjangoExpress)|Backend Frameworks (Django/Express)]]
- [[_COMMUNITY_AWS Deploy & CICD|AWS Deploy & CI/CD]]
- [[_COMMUNITY_Docker & Containers|Docker & Containers]]
- [[_COMMUNITY_JSTS Types & Classes|JS/TS Types & Classes]]
- [[_COMMUNITY_React State & Hooks|React State & Hooks]]
- [[_COMMUNITY_Claude Code  Coding Agents|Claude Code / Coding Agents]]
- [[_COMMUNITY_NestJS & Decorators|NestJS & Decorators]]
- [[_COMMUNITY_Kubernetes & ML Infra|Kubernetes & ML Infra]]
- [[_COMMUNITY_DOM & Events|DOM & Events]]
- [[_COMMUNITY_Java Fundamentals|Java Fundamentals]]
- [[_COMMUNITY_Rust Toolchain|Rust Toolchain]]
- [[_COMMUNITY_AI Resume Reviewer Project|AI Resume Reviewer Project]]
- [[_COMMUNITY_CSS Grid & Responsive|CSS Grid & Responsive]]
- [[_COMMUNITY_Java Compilation Flow|Java Compilation Flow]]
- [[_COMMUNITY_Dynamic Programming|Dynamic Programming]]
- [[_COMMUNITY_React 19 Features|React 19 Features]]
- [[_COMMUNITY_Open APIs & Resources|Open APIs & Resources]]
- [[_COMMUNITY_Workspace Config|Workspace Config]]
- [[_COMMUNITY_Git Tracking|Git Tracking]]
- [[_COMMUNITY_BookMovie APIs|Book/Movie APIs]]
- [[_COMMUNITY_mkdocs Dependency|mkdocs Dependency]]
- [[_COMMUNITY_Blogs Index|Blogs Index]]
- [[_COMMUNITY_Java Memory Diagram|Java Memory Diagram]]
- [[_COMMUNITY_Git Remotes Diagram|Git Remotes Diagram]]
- [[_COMMUNITY_Gym Plan|Gym Plan]]

## God Nodes (most connected - your core abstractions)
1. `JavaScript Language Reference` - 23 edges
2. `Node.js` - 20 edges
3. `Class Notes Learning Index` - 16 edges
4. `React` - 15 edges
5. `TypeScript` - 14 edges
6. `Mongoose` - 12 edges
7. `MongoDB` - 11 edges
8. `Claude Code in Action (Course)` - 10 edges
9. `React Advanced Guides` - 10 edges
10. `Web Security` - 10 edges

## Surprising Connections (you probably didn't know these)
- `Class and Object` --semantically_similar_to--> `TypeScript Classes`  [INFERRED] [semantically similar]
  raw/Web Technical/Java/Java OOP.md → raw/Web Technical/TypeScript/Classes.md
- `GitHub Integration Flow (HTML Visual)` --semantically_similar_to--> `GitHub Integration Sequence Diagram`  [INFERRED] [semantically similar]
  raw/Coding Agents/attachments/github-integration-flow.html → raw/Excalidraw/github-integration-flow.excalidraw.md
- `Higher-Order Components (HOC)` --conceptually_related_to--> `TanStack / React Query`  [AMBIGUOUS]
  raw/Web Technical/React advanced.md → raw/Web Technical/TanStack Query.md
- `ECMAScript Modules` --semantically_similar_to--> `JavaScript Modules`  [INFERRED] [semantically similar]
  raw/Web Technical/NodeJS/Developing modules.md → raw/Web Technical/JavaScript.md
- `Reference Types` --semantically_similar_to--> `JavaScript`  [INFERRED] [semantically similar]
  raw/Web Technical/Java/Java.md → raw/Web Technical/TypeScript/TypeScript.md

## Hyperedges (group relationships)
- **CI/CD Pipeline: Dockerfile build to EC2 deploy** — cicd_dockerfile, cicd_ci_job, cicd_cd_job, cicd_env_file [EXTRACTED 0.90]
- **AWS Native Deployment Stack (EC2 + Nginx + PM2)** — awsdeploy_ec2_setup, awsdeploy_nginx, awsdeploy_pm2 [EXTRACTED 0.90]
- **Notion Planning Template Set (Brainstorm, PRD, Tech Spec)** — examplebrainstorm_doc, exampleprd_doc, exampletechspec_doc [INFERRED 0.80]
- **Claude Code GitHub Actions Agentic Flow** — githubintegrationflow_ex_github, githubintegrationflow_ex_actions, githubintegrationflow_ex_runner, githubintegrationflow_ex_claudecode [INFERRED 0.85]
- **Java Compile-and-Run Pipeline** — javacompile_ex_source, javacompile_ex_compiler, javacompile_ex_bytecode, javajvm_ex_jvm, javajvm_ex_native [INFERRED 0.80]
- **Claude Code Hook Lifecycle** — claudecodeinaction_pretooluse, claudecodeinaction_posttooluse, claudecodeinaction_notification_hook, claudecodeinaction_stop_hook [INFERRED 0.80]
- **Node.js Asynchronous Foundation** — node_async_model, node_event_loop, node_libuv [INFERRED 0.85]
- **JavaScript Async Evolution** — js_async_callbacks, js_promises, js_async_await [INFERRED 0.85]
- **Node.js Microservice Deployment Pipeline** — node_microservices, node_docker_container, node_kubernetes [INFERRED 0.80]
- **TypeScript Handbook Topics** — typescript_typescript, tsnarrowing_narrowing, tsfunction_more_on_function, tsobject_object_type, tsclasses_classes, tsenums_enums [INFERRED 0.85]
- **Mongoose Data Modeling Stack** — mongoose_schema, mongoose_model, mongoose_document, mongoose_subdocuments [INFERRED 0.80]
- **Docker MongoDB + Mongo-Express Deployment** — docker_network, mongodb_mongodb, docker_mongo_express [INFERRED 0.80]
- **React State Management Flow** — react_state_lifecycle, react_queueing_updates, react_rerendering_commit, react_managing_state [INFERRED 0.80]
- **MLOps Streaming Stack** — k8s_kubernetes, k8s_kubeflow, k8s_kafka, k8s_spark_streaming [EXTRACTED 0.90]
- **NestJS DI via Decorators** — decorator_metadata, nestjs_dependency_injection, nestjs_providers [INFERRED 0.80]

## Communities

### Community 0 - "Web Dev Beginner Path"
Cohesion: 0.06
Nodes (52): Agility IO Internship, Class Notes Learning Index, Phase 5: Backend Basics with Node.js + Express, Phase 3: DOM & Interactivity, Phase 2: JavaScript Fundamentals, Phase 4: Git, GitHub & React Fundamentals, Phase 1: Web Basics, Web Development Beginner Course (+44 more)

### Community 1 - "Backend Frameworks (Django/Express)"
Cohesion: 0.06
Nodes (45): Django, Django Models, Django REST Framework, EJS View Engine, Express Framework, Express Middleware, Express Routing, Docker (+37 more)

### Community 2 - "AWS Deploy & CI/CD"
Cohesion: 0.06
Nodes (41): Native Deployment with AWS, EC2 Instance Setup (git, Node, MySQL), Nginx Reverse Proxy, PM2 Process Manager (keep app alive), CD Job (deploy to AWS EC2 via SSH), CI Job (build & push image to DockerHub), CICD Notes, Dockerfile (Node 18 build) (+33 more)

### Community 3 - "Docker & Containers"
Cohesion: 0.06
Nodes (40): Docker Compose, Container, Docker, Dockerfile, DockerHub, Docker Image, Mongo Express UI, Docker Network (+32 more)

### Community 4 - "JS/TS Types & Classes"
Cohesion: 0.06
Nodes (39): JavaScript, Reference Types, Abstract Classes and Members, TypeScript Classes, Generic Classes, Member Visibility (public/protected/private), Static members cannot reference type parameters (types erased at runtime), this Types and this-based Type Guards (+31 more)

### Community 5 - "React State & Hooks"
Cohesion: 0.09
Nodes (36): React State Batching, Built-in React Hooks, Class vs Functional Components, React Component, Passing Data Deeply with Context, Custom Hooks, Event Propagation and Bubbling, Immutable State Updates (Objects and Arrays) (+28 more)

### Community 6 - "Claude Code / Coding Agents"
Cohesion: 0.11
Nodes (23): GitHub Actions Runner VM, /clear Command, /compact Command, Claude Code in Action (Course), Custom Commands, GitHub Integration Flow, Hook Matchers, Hooks (+15 more)

### Community 7 - "NestJS & Decorators"
Cohesion: 0.14
Nodes (18): Decorator, Metadata Attachment via Reflect-metadata, Decorator Types (Class, Property, Method, Parameter), Wrap or Replace Logic, Nest CLI, NestJS Controllers, Dependency Injection, NestJS (+10 more)

### Community 8 - "Kubernetes & ML Infra"
Cohesion: 0.15
Nodes (16): Kubernetes Cluster Components, Container Deployment vs Traditional Deployment, Dependency Hell, DStreams (Input, Transformations, Output), Apache Kafka, Kubeflow, Kubeflow Katib (Hyperparameter Tuning), Kubeflow KServe (Model Serving) (+8 more)

### Community 9 - "DOM & Events"
Cohesion: 0.13
Nodes (15): DOM (Document Object Model), Finding DOM Elements, Event Bubbling vs Capturing, DOM Events & addEventListener, Modifying Attributes, Classes, Styles, DOM Navigation (node tree), Git Begin, CSS (+7 more)

### Community 10 - "Java Fundamentals"
Cohesion: 0.15
Nodes (14): Type Casting, Java, Java Compiler (javac), Java Runtime Environment (JRE), Basic Literals & Primitive Types, Scanner (Reading Input), Write Once Run Anywhere (WORA), Class and Object (+6 more)

### Community 11 - "Rust Toolchain"
Cohesion: 0.21
Nodes (12): Cargo, Compiler as gatekeeper (safety), Rust Getting Started, Rust, rust-analyzer, rustfmt, Channel (stable/beta/nightly), Component (+4 more)

### Community 12 - "AI Resume Reviewer Project"
Cohesion: 0.25
Nodes (9): User Authentication (NextAuth.js/JWT), Job Match Score, NestJS (Back-end), Next.js (Front-end), OpenAI API (GPT-4-turbo), PostgreSQL, AI Resume Reviewer, AI-Powered Resume Analysis (+1 more)

### Community 13 - "CSS Grid & Responsive"
Cohesion: 0.28
Nodes (9): Grid Auto Placement, CSS Grid Layout, Grid Terminology, Responsive Web Design, Breakpoints, Grid vs Flexbox, CSS Media Queries, Meta Viewport (+1 more)

### Community 14 - "Java Compilation Flow"
Cohesion: 0.43
Nodes (7): Byte code (*.class), Java compiler, Java Compilation Flow (diagram), Source code (*.java), Java Bytecode-to-Native Flow (diagram), Java Virtual Machine, Native code (MacOS, Linux...)

### Community 15 - "Dynamic Programming"
Cohesion: 0.33
Nodes (7): Bottom-up DP, Dynamic Programming, House Robber, Longest Increasing Subsequence, Optimal Substructure, Overlapping Subproblems, Top-down DP (Memoization)

### Community 16 - "React 19 Features"
Cohesion: 0.29
Nodes (7): Actions & useActionState, React Compiler removes need for manual performance hooks (useCallback/useMemo/memo), React 19, React Compiler, ref as prop (removing forwardRef), Server Components, use Hook

### Community 17 - "Open APIs & Resources"
Cohesion: 0.33
Nodes (6): List Template, Open APIs and Data Resource, Google Books API, OMDb API (Open Movie Database), AI Resume Reviewer Project, Technical Resource Index

### Community 18 - "Workspace Config"
Cohesion: 1.0
Nodes (2): Graphify Knowledge Graph Rules, Personal Notes Workspace (CLAUDE.md)

### Community 19 - "Git Tracking"
Cohesion: 1.0
Nodes (2): Why .gitignore Doesn't Stop Tracked Files, git rm --cached (stop tracking without deleting)

### Community 20 - "Book/Movie APIs"
Cohesion: 1.0
Nodes (2): Google Books API, OMDb API

### Community 21 - "mkdocs Dependency"
Cohesion: 1.0
Nodes (1): mkdocs-material Dependency

### Community 22 - "Blogs Index"
Cohesion: 1.0
Nodes (1): liemgumball's Blogs Index

### Community 23 - "Java Memory Diagram"
Cohesion: 1.0
Nodes (1): Java RAM / Object Reference (diagram)

### Community 24 - "Git Remotes Diagram"
Cohesion: 1.0
Nodes (1): Git Remotes (diagram)

### Community 25 - "Gym Plan"
Cohesion: 1.0
Nodes (1): 3-Month Gym Plan for Beginner

## Ambiguous Edges - Review These
- `TanStack / React Query` → `Higher-Order Components (HOC)`  [AMBIGUOUS]
  raw/Web Technical/React advanced.md · relation: conceptually_related_to

## Knowledge Gaps
- **194 isolated node(s):** `Personal Notes Workspace (CLAUDE.md)`, `Graphify Knowledge Graph Rules`, `mkdocs-material Dependency`, `Problem Statement / Goals / Non-goals`, `Proposed Solution (Architecture, Data Model, UI)` (+189 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `Workspace Config`** (2 nodes): `Graphify Knowledge Graph Rules`, `Personal Notes Workspace (CLAUDE.md)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Git Tracking`** (2 nodes): `Why .gitignore Doesn't Stop Tracked Files`, `git rm --cached (stop tracking without deleting)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Book/Movie APIs`** (2 nodes): `Google Books API`, `OMDb API`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `mkdocs Dependency`** (1 nodes): `mkdocs-material Dependency`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Blogs Index`** (1 nodes): `liemgumball's Blogs Index`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Java Memory Diagram`** (1 nodes): `Java RAM / Object Reference (diagram)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Git Remotes Diagram`** (1 nodes): `Git Remotes (diagram)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Gym Plan`** (1 nodes): `3-Month Gym Plan for Beginner`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `TanStack / React Query` and `Higher-Order Components (HOC)`?**
  _Edge tagged AMBIGUOUS (relation: conceptually_related_to) - confidence is low._
- **Why does `JavaScript` connect `JS/TS Types & Classes` to `React 19 Features`, `DOM & Events`, `Docker & Containers`?**
  _High betweenness centrality (0.179) - this node is a cross-community bridge._
- **Why does `React` connect `Web Dev Beginner Path` to `React 19 Features`, `DOM & Events`?**
  _High betweenness centrality (0.149) - this node is a cross-community bridge._
- **Why does `DOM (Document Object Model)` connect `DOM & Events` to `Web Dev Beginner Path`, `JS/TS Types & Classes`?**
  _High betweenness centrality (0.145) - this node is a cross-community bridge._
- **What connects `Personal Notes Workspace (CLAUDE.md)`, `Graphify Knowledge Graph Rules`, `mkdocs-material Dependency` to the rest of the system?**
  _194 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Web Dev Beginner Path` be split into smaller, more focused modules?**
  _Cohesion score 0.06 - nodes in this community are weakly interconnected._
- **Should `Backend Frameworks (Django/Express)` be split into smaller, more focused modules?**
  _Cohesion score 0.06 - nodes in this community are weakly interconnected._