# Graph Report - .  (2026-04-11)

## Corpus Check
- Large corpus: 181 files · ~903,946 words. Semantic extraction will be expensive (many Claude tokens). Consider running on a subfolder, or use --no-semantic to run AST-only.

## Summary
- 343 nodes · 196 edges · 158 communities detected
- Extraction: 87% EXTRACTED · 13% INFERRED · 0% AMBIGUOUS · INFERRED: 25 edges (avg confidence: 0.84)
- Token cost: 0 input · 0 output

## God Nodes (most connected - your core abstractions)
1. `Claude Code in Action Course` - 11 edges
2. `React Developer Interview Questions` - 9 edges
3. `Notes Index` - 8 edges
4. `AI Resume Reviewer Project` - 8 edges
5. `Class Notes Index (Web Technical)` - 8 edges
6. `Claude Code Hooks` - 7 edges
7. `Built-in React Hooks` - 7 edges
8. `Front-end Developer Interview Questions` - 6 edges
9. `Dynamic Programming` - 6 edges
10. `TypeScript Language` - 6 edges

## Surprising Connections (you probably didn't know these)
- `Claude Code Hook Lifecycle Sequence Diagram` --references--> `Claude Code Hooks`  [EXTRACTED]
  Excalidraw/attachments/Pasted image 20260325215354.png → claude-code-in-action.md
- `Docker CI/CD Pipeline with Jenkins and Git` --conceptually_related_to--> `CI/CD Pipeline Workflow`  [INFERRED]
  Web Technical/Docker/attachments/Untitled.png → Note/CICD.md
- `Phase 4: Git, GitHub, and React Fundamentals (Weeks 13-20)` --conceptually_related_to--> `React`  [INFERRED]
  Teaching/Web/Front-end/Course.md → Web Technical/Class Notes.md
- `React 19` --references--> `React 19 New Features`  [INFERRED]
  Web Technical/React 19/attachments/image 14.png → Web Technical/React 19/React 19.md
- `Personal Notes Workspace` --references--> `Claude Code in Action Course`  [EXTRACTED]
  CLAUDE.md → claude-code-in-action.md

## Hyperedges (group relationships)
- **AWS Native Deployment Stack** — native_aws_ec2, native_aws_nginx, native_aws_pm2, native_aws_mysql [EXTRACTED 0.95]
- **CI/CD Docker + AWS Deployment Pipeline** — cicd_dockerfile, cicd_pipeline, cicd_dockerhub, cicd_aws_ec2_deploy [EXTRACTED 0.95]
- **Claude Code Hook Lifecycle** — claude_code_pretooluse_hook, claude_code_posttooluse_hook, claude_code_notification_hook, claude_code_stop_hook [EXTRACTED 0.95]
- **AI Resume Reviewer MVP Core** — ai_resume_feature_upload, ai_resume_feature_analysis, ai_resume_feature_job_match [INFERRED 0.90]
- **FocusFlow AI-Powered Video Production Pipeline** — focusflow_tools_chatgpt, focusflow_tools_elevenlabs, focusflow_tools_runwayml [EXTRACTED 0.95]
- **Dynamic Programming Problem Characteristics** — dp_concept, dp_overlapping_subproblems, dp_optimal_substructure [EXTRACTED 1.00]
- **Node.js Data Persistence Stack** — nodejs_sql_databases, nodejs_nosql_databases, nodejs_redis [INFERRED 0.85]
- **React Advanced Patterns** — react_advanced_hoc, react_advanced_code_splitting, react_advanced_error_boundaries [INFERRED 0.80]
- **Node.js Microservice Deployment Stack** — nodejs_loopback, nodejs_docker_container, nodejs_kubernetes [EXTRACTED 0.90]
- **Node.js Security Stack** — nodejs_securing_helmet, nodejs_securing_bcrypt, nodejs_securing_express_session [EXTRACTED 0.95]
- **TypeScript Core Type System** — ts_classes, ts_object_type, ts_narrowing, ts_more_on_function [INFERRED 0.85]
- **Docker + Node.js + MongoDB Deployment Stack** — docker_docker, docker_compose, mongoose_mongoose [EXTRACTED 0.90]
- **React State Management Ecosystem** — react_state, react_usestate, react_usereducer, react_context, react_managing_state [INFERRED 0.85]
- **NestJS Core Building Blocks** — nestjs_controllers, nestjs_providers, nestjs_modules, nestjs_dependency_injection, nestjs_decorator [EXTRACTED 0.95]
- **MongoDB Data Access Patterns** — mongodb_crud_operations, mongodb_aggregation_pipeline, mongodb_indexes, indexing_indexing [INFERRED 0.80]

## Communities

### Community 0 - "React & Redux Ecosystem"
Cohesion: 0.08
Nodes (27): DOM addEventListener, HTML DOM (Document Object Model), DOM Event Propagation (Bubbling and Capturing), DOM Node Tree Navigation, DOM Tree Structure Diagram, React Components, React Context API, React Context - Prop Drilling Through Component Tree (+19 more)

### Community 1 - "Templates & Interview Prep"
Cohesion: 0.1
Nodes (21): Example Brainstorm Template, Example PRD Template, Example Tech Spec Template, CORS (Cross-Origin Resource Sharing), CSS Concepts, HTML Concepts, Front-end Developer Interview Questions, JavaScript Concepts (+13 more)

### Community 2 - "Claude Code Tooling"
Cohesion: 0.11
Nodes (19): /clear Command, /compact Command, Custom Slash Commands, GitHub Integration with Claude Code, Claude Code Hooks, Claude Code in Action Course, Notification Hook, Claude Code Permission Management (+11 more)

### Community 3 - "Web Dev Course & Node.js"
Cohesion: 0.14
Nodes (14): Phase 1: Web Basics (Weeks 1-4), Phase 2: JavaScript Fundamentals (Weeks 5-8), Phase 3: DOM & Interactivity (Weeks 9-12), Phase 4: Git, GitHub, and React Fundamentals (Weeks 13-20), Phase 5: Backend Basics with Node.js + Express (Weeks 21-24), Web Development Beginner Course (Weeks 1-24), Django REST Framework, Docker Container for Node.js (+6 more)

### Community 4 - "TypeScript & Java OOP"
Cohesion: 0.15
Nodes (13): Java Programming Language, Java OOP Principles, TypeScript Classes, TypeScript Abstract Classes, TypeScript Generic Classes, TypeScript Enums, TypeScript Mixins Pattern, TypeScript Type Narrowing (+5 more)

### Community 5 - "CI/CD & AWS Deployment"
Cohesion: 0.17
Nodes (12): Nginx Welcome Page Screenshot - AWS Deployment, AWS EC2 Deployment, Dockerfile Configuration, DockerHub Registry, CI/CD Notes, CI/CD Pipeline Workflow, Docker CI/CD Pipeline with Jenkins and Git, Native Deployment with AWS (+4 more)

### Community 6 - "AI Resume Reviewer & APIs"
Cohesion: 0.18
Nodes (12): AI-Powered Resume Analysis, Resume Upload & Parsing (PDF/DOC), AI Resume Reviewer Project, Docker & AWS (Infrastructure), NestJS (Backend), Next.js (Frontend), OpenAI API (GPT-4-turbo), PostgreSQL (Database) (+4 more)

### Community 7 - "NestJS & Advanced TypeScript"
Cohesion: 0.2
Nodes (10): NestJS Controllers, NestJS Dependency Injection, NestJS Resume Module File Structure, NestJS Modules, NestJS Framework, NestJS Providers, TypeScript Conditional and Mapped Types, TypeScript Generics (+2 more)

### Community 8 - "Class Notes Index"
Cohesion: 0.22
Nodes (9): Docker, Class Notes Index (Web Technical), JavaScript, MongoDB, NestJS, NodeJS, React, Redux (+1 more)

### Community 9 - "Web & Node.js Security"
Cohesion: 0.29
Nodes (8): bcrypt Password Hashing, Cross-Site Request Forgery (CSRF) Defense, Helmet.js HTTP Security Headers, Node.js Application Security, Cross-Site Scripting (XSS) Attack Prevention, Cross-Site Request Forgery (CSRF), Malware Types (Worm, Ransomware, Botnet), Web Security Fundamentals

### Community 10 - "Dynamic Programming"
Cohesion: 0.33
Nodes (7): Bottom-Up DP (Tabulation), Dynamic Programming, Optimal Substructure (DP Characteristic), Overlapping Subproblems (DP Characteristic), House Robber Problem, Longest Increasing Subsequence Problem, Top-Down DP (Memoization)

### Community 11 - "Docker Platform"
Cohesion: 0.29
Nodes (7): Docker Compose, Docker Container, Docker Container Components Diagram, Docker Containerization Platform, Dockerfile Blueprint, DockerHub Public Repository, Docker Image

### Community 12 - "Data Structures & Algorithms"
Cohesion: 0.33
Nodes (6): Algorithms Overview, Binary Search Tree, Binary Search Tree Node Insert Implementation, Data Structures Overview, Hash Table, Merge Sort (Preferred)

### Community 13 - "React 19 Features"
Cohesion: 0.33
Nodes (6): React 19, React Actions and useActionState, React Compiler, React 19 New Features, React Server Components, React use() Hook

### Community 14 - "MongoDB & Indexing"
Cohesion: 0.33
Nodes (6): Database Indexing, BSON Document Format, MongoDB Collections, Structure of an Index in Database, MongoDB Indexes, MongoDB

### Community 15 - "Shell, Git & HTML/CSS"
Cohesion: 0.4
Nodes (5): Git Version Control Basics, CSS Layout (Flexbox, Float, Position), Git Commands (stash, reset, revert, rebase), Shell Commands, Git, HTML & CSS Reference, HTML Structure & Semantic Elements

### Community 16 - "FocusFlow YouTube Channel"
Cohesion: 0.5
Nodes (4): FocusFlow Content Plan (First Month), FocusFlow YouTube Channel Research & Plan, ElevenLabs (AI Voiceover), RunwayML (AI Visuals)

### Community 17 - "TanStack Query"
Cohesion: 0.5
Nodes (4): Query Keys, TanStack Query (React Query) Overview, useMutation Hook, useQuery Hook

### Community 18 - "Responsive Design"
Cohesion: 0.5
Nodes (4): CSS Media Queries, Mobile-First Design Approach, Rationale: Why Mobile-First, Responsive Web Design

### Community 19 - "ES Modules"
Cohesion: 0.67
Nodes (3): ES6 Module Import/Export, JavaScript Modules (import/export), ECMAScript Modules (ESM) in Node.js

### Community 20 - "Git Tips"
Cohesion: 1.0
Nodes (2): git rm --cached Command, Git .gitignore Tracking Issue

### Community 21 - "CSS Grid"
Cohesion: 1.0
Nodes (2): CSS Grid Layout, Grid Terminology (line, track, cell, area, gap)

### Community 22 - "Promises & Async"
Cohesion: 1.0
Nodes (2): ES6 Promises, JavaScript Promises and Async/Await

### Community 23 - "Testing (Jest)"
Cohesion: 1.0
Nodes (2): Testing with Jest (Node.js), React Testing (Jest, React Testing Library, Vitest)

### Community 24 - "Package Managers"
Cohesion: 1.0
Nodes (2): Yarn Package Manager, npm (Node Package Manager)

### Community 25 - "Java Spring Boot"
Cohesion: 1.0
Nodes (2): Java Learning Plan (8-12 Weeks), Spring Boot (Java Web Framework)

### Community 26 - "Mongoose ODM"
Cohesion: 1.0
Nodes (2): Mongoose ODM for MongoDB, Mongoose Schema

### Community 27 - "TypeScript Decorators"
Cohesion: 1.0
Nodes (2): TypeScript Decorator, Reflect Metadata

### Community 28 - "New Brainstorm Template"
Cohesion: 1.0
Nodes (1): New Brainstorm Template

### Community 29 - "List Template"
Cohesion: 1.0
Nodes (1): List Template

### Community 30 - "New Product Spec (PRD) Template"
Cohesion: 1.0
Nodes (1): New Product Spec (PRD) Template

### Community 31 - "PRD Problem Section"
Cohesion: 1.0
Nodes (1): PRD Problem Section

### Community 32 - "PRD Proposal Section"
Cohesion: 1.0
Nodes (1): PRD Proposal Section

### Community 33 - "PRD Plan / Launch Checklist"
Cohesion: 1.0
Nodes (1): PRD Plan / Launch Checklist

### Community 34 - "New Brainstorm Template"
Cohesion: 1.0
Nodes (1): New Brainstorm Template

### Community 35 - "AI Resume Reviewer Goal: Job Seekers Imp"
Cohesion: 1.0
Nodes (1): AI Resume Reviewer Goal: Job Seekers Improve Resumes

### Community 36 - "Job Match Score Feature"
Cohesion: 1.0
Nodes (1): Job Match Score Feature

### Community 37 - "Resume Analysis Dashboard"
Cohesion: 1.0
Nodes (1): Resume Analysis Dashboard

### Community 38 - "NextAuth.js with JWT"
Cohesion: 1.0
Nodes (1): NextAuth.js with JWT

### Community 39 - "FocusFlow YouTube Channel Setup"
Cohesion: 1.0
Nodes (1): FocusFlow YouTube Channel Setup

### Community 40 - "FocusFlow Brand Identity"
Cohesion: 1.0
Nodes (1): FocusFlow Brand Identity

### Community 41 - "Soundraw.io (AI Music)"
Cohesion: 1.0
Nodes (1): Soundraw.io (AI Music)

### Community 42 - "ChatGPT (Scriptwriting)"
Cohesion: 1.0
Nodes (1): ChatGPT (Scriptwriting)

### Community 43 - "Canva (Thumbnails & Branding)"
Cohesion: 1.0
Nodes (1): Canva (Thumbnails & Branding)

### Community 44 - "FocusFlow Monetization Strategy"
Cohesion: 1.0
Nodes (1): FocusFlow Monetization Strategy

### Community 45 - "FocusFlow Growth Strategy"
Cohesion: 1.0
Nodes (1): FocusFlow Growth Strategy

### Community 46 - "HTML Basics Questions"
Cohesion: 1.0
Nodes (1): HTML Basics Questions

### Community 47 - "Semantic HTML Elements"
Cohesion: 1.0
Nodes (1): Semantic HTML Elements

### Community 48 - "HTML Forms"
Cohesion: 1.0
Nodes (1): HTML Forms

### Community 49 - "TanStack Query"
Cohesion: 1.0
Nodes (1): TanStack Query

### Community 50 - "React Advanced"
Cohesion: 1.0
Nodes (1): React Advanced

### Community 51 - "ES5 vs ES6"
Cohesion: 1.0
Nodes (1): ES5 vs ES6

### Community 52 - "DOM"
Cohesion: 1.0
Nodes (1): DOM

### Community 53 - "Grid CSS"
Cohesion: 1.0
Nodes (1): Grid CSS

### Community 54 - "Responsive Web Design"
Cohesion: 1.0
Nodes (1): Responsive Web Design

### Community 55 - "Storybook"
Cohesion: 1.0
Nodes (1): Storybook

### Community 56 - "HTML-CSS Training"
Cohesion: 1.0
Nodes (1): HTML-CSS Training

### Community 57 - "Django"
Cohesion: 1.0
Nodes (1): Django

### Community 58 - "Query Invalidation"
Cohesion: 1.0
Nodes (1): Query Invalidation

### Community 59 - "Infinite Queries (useInfiniteQuery)"
Cohesion: 1.0
Nodes (1): Infinite Queries (useInfiniteQuery)

### Community 60 - "Parallel Queries"
Cohesion: 1.0
Nodes (1): Parallel Queries

### Community 61 - "Dependent Queries"
Cohesion: 1.0
Nodes (1): Dependent Queries

### Community 62 - "Grid Auto Placement"
Cohesion: 1.0
Nodes (1): Grid Auto Placement

### Community 63 - "ES6 Arrow Functions"
Cohesion: 1.0
Nodes (1): ES6 Arrow Functions

### Community 64 - "ES6 let and const (Block Scope)"
Cohesion: 1.0
Nodes (1): ES6 let and const (Block Scope)

### Community 65 - "ES6 Spread Operator"
Cohesion: 1.0
Nodes (1): ES6 Spread Operator

### Community 66 - "ES6 Object Destructuring"
Cohesion: 1.0
Nodes (1): ES6 Object Destructuring

### Community 67 - "ES6 Template Literals"
Cohesion: 1.0
Nodes (1): ES6 Template Literals

### Community 68 - "React Accessibility (WCAG, ARIA)"
Cohesion: 1.0
Nodes (1): React Accessibility (WCAG, ARIA)

### Community 69 - "React Code Splitting (React.lazy, Suspen"
Cohesion: 1.0
Nodes (1): React Code Splitting (React.lazy, Suspense)

### Community 70 - "React Error Boundaries"
Cohesion: 1.0
Nodes (1): React Error Boundaries

### Community 71 - "Higher-Order Components (HOC)"
Cohesion: 1.0
Nodes (1): Higher-Order Components (HOC)

### Community 72 - "React Performance Optimization (memo, Pr"
Cohesion: 1.0
Nodes (1): React Performance Optimization (memo, Profiler)

### Community 73 - "HTML-CSS Training: Git Branch & PR Conve"
Cohesion: 1.0
Nodes (1): HTML-CSS Training: Git Branch & PR Conventions

### Community 74 - "CSS @import Performance Issue"
Cohesion: 1.0
Nodes (1): CSS @import Performance Issue

### Community 75 - "JavaScript Syntax and Variables"
Cohesion: 1.0
Nodes (1): JavaScript Syntax and Variables

### Community 76 - "JavaScript Arrays and Methods"
Cohesion: 1.0
Nodes (1): JavaScript Arrays and Methods

### Community 77 - "JavaScript Classes and OOP"
Cohesion: 1.0
Nodes (1): JavaScript Classes and OOP

### Community 78 - "JavaScript Generator Functions"
Cohesion: 1.0
Nodes (1): JavaScript Generator Functions

### Community 79 - "JavaScript Performance Tips"
Cohesion: 1.0
Nodes (1): JavaScript Performance Tips

### Community 80 - "Django Project Setup"
Cohesion: 1.0
Nodes (1): Django Project Setup

### Community 81 - "Django REST Swagger (drf-yasg)"
Cohesion: 1.0
Nodes (1): Django REST Swagger (drf-yasg)

### Community 82 - "Node.js File System Module (fs)"
Cohesion: 1.0
Nodes (1): Node.js File System Module (fs)

### Community 83 - "Node.js TCP/UDP Sockets"
Cohesion: 1.0
Nodes (1): Node.js TCP/UDP Sockets

### Community 84 - "Node.js Event Emitter"
Cohesion: 1.0
Nodes (1): Node.js Event Emitter

### Community 85 - "Node.js Debugging"
Cohesion: 1.0
Nodes (1): Node.js Debugging

### Community 86 - "Working with SQL Databases (MySQL, Postg"
Cohesion: 1.0
Nodes (1): Working with SQL Databases (MySQL, PostgreSQL)

### Community 87 - "Persisting Data with Redis"
Cohesion: 1.0
Nodes (1): Persisting Data with Redis

### Community 88 - "Jest Mock Functions"
Cohesion: 1.0
Nodes (1): Jest Mock Functions

### Community 89 - "Jest with MongoDB"
Cohesion: 1.0
Nodes (1): Jest with MongoDB

### Community 90 - "Web Protocols with Node.js (HTTP, WebSoc"
Cohesion: 1.0
Nodes (1): Web Protocols with Node.js (HTTP, WebSocket, SMTP)

### Community 91 - "WebSocket Server (ws module)"
Cohesion: 1.0
Nodes (1): WebSocket Server (ws module)

### Community 92 - "SMTP Email Server (Node.js)"
Cohesion: 1.0
Nodes (1): SMTP Email Server (Node.js)

### Community 93 - "Working with NoSQL Databases (MongoDB, M"
Cohesion: 1.0
Nodes (1): Working with NoSQL Databases (MongoDB, Mongoose)

### Community 94 - "Mongoose ODM"
Cohesion: 1.0
Nodes (1): Mongoose ODM

### Community 95 - "Express.js Middleware"
Cohesion: 1.0
Nodes (1): Express.js Middleware

### Community 96 - "Express.js EJS View Engine"
Cohesion: 1.0
Nodes (1): Express.js EJS View Engine

### Community 97 - "Node Version Manager (nvm)"
Cohesion: 1.0
Nodes (1): Node Version Manager (nvm)

### Community 98 - "LoopBack Microservice Generator"
Cohesion: 1.0
Nodes (1): LoopBack Microservice Generator

### Community 99 - "GraphQL API (Node.js microservices)"
Cohesion: 1.0
Nodes (1): GraphQL API (Node.js microservices)

### Community 100 - "express-session Authentication"
Cohesion: 1.0
Nodes (1): express-session Authentication

### Community 101 - "JSON Pollution Attack Prevention"
Cohesion: 1.0
Nodes (1): JSON Pollution Attack Prevention

### Community 102 - "HTTP Parameter Pollution Defense"
Cohesion: 1.0
Nodes (1): HTTP Parameter Pollution Defense

### Community 103 - "npm audit Vulnerability Detection"
Cohesion: 1.0
Nodes (1): npm audit Vulnerability Detection

### Community 104 - "Storybook UI Component Workshop"
Cohesion: 1.0
Nodes (1): Storybook UI Component Workshop

### Community 105 - "Storybook ArgTypes"
Cohesion: 1.0
Nodes (1): Storybook ArgTypes

### Community 106 - "Data Leakage Channels"
Cohesion: 1.0
Nodes (1): Data Leakage Channels

### Community 107 - "Session Riding Attacks"
Cohesion: 1.0
Nodes (1): Session Riding Attacks

### Community 108 - "TypeScript Class Member Visibility (publ"
Cohesion: 1.0
Nodes (1): TypeScript Class Member Visibility (public/protected/private)

### Community 109 - "TypeScript Interface"
Cohesion: 1.0
Nodes (1): TypeScript Interface

### Community 110 - "TypeScript Intersection Types"
Cohesion: 1.0
Nodes (1): TypeScript Intersection Types

### Community 111 - "TypeScript Tuple Types"
Cohesion: 1.0
Nodes (1): TypeScript Tuple Types

### Community 112 - "TypeScript Functions (Overloads, Generic"
Cohesion: 1.0
Nodes (1): TypeScript Functions (Overloads, Generics, Callbacks)

### Community 113 - "TypeScript Union Types"
Cohesion: 1.0
Nodes (1): TypeScript Union Types

### Community 114 - "TypeScript Type Aliases"
Cohesion: 1.0
Nodes (1): TypeScript Type Aliases

### Community 115 - "TypeScript Literal Types"
Cohesion: 1.0
Nodes (1): TypeScript Literal Types

### Community 116 - "SEO Best Practices (HTML/CSS)"
Cohesion: 1.0
Nodes (1): SEO Best Practices (HTML/CSS)

### Community 117 - "React useOptimistic Hook"
Cohesion: 1.0
Nodes (1): React useOptimistic Hook

### Community 118 - "Switching JDK Version on macOS"
Cohesion: 1.0
Nodes (1): Switching JDK Version on macOS

### Community 119 - "MongoDB Query API"
Cohesion: 1.0
Nodes (1): MongoDB Query API

### Community 120 - "MongoDB CRUD Operations"
Cohesion: 1.0
Nodes (1): MongoDB CRUD Operations

### Community 121 - "MongoDB Aggregation Pipelines"
Cohesion: 1.0
Nodes (1): MongoDB Aggregation Pipelines

### Community 122 - "MongoDB Sessions and Transactions"
Cohesion: 1.0
Nodes (1): MongoDB Sessions and Transactions

### Community 123 - "MongoDB Schema Validation"
Cohesion: 1.0
Nodes (1): MongoDB Schema Validation

### Community 124 - "Index Search Key"
Cohesion: 1.0
Nodes (1): Index Search Key

### Community 125 - "Index Data Reference Pointer"
Cohesion: 1.0
Nodes (1): Index Data Reference Pointer

### Community 126 - "HTMLCollection"
Cohesion: 1.0
Nodes (1): HTMLCollection

### Community 127 - "NodeList"
Cohesion: 1.0
Nodes (1): NodeList

### Community 128 - "NestJS ORM (Object-Relational Mapping)"
Cohesion: 1.0
Nodes (1): NestJS ORM (Object-Relational Mapping)

### Community 129 - "React Re-rendering and Commit"
Cohesion: 1.0
Nodes (1): React Re-rendering and Commit

### Community 130 - "React State Update Batching"
Cohesion: 1.0
Nodes (1): React State Update Batching

### Community 131 - "useRef Hook"
Cohesion: 1.0
Nodes (1): useRef Hook

### Community 132 - "React Custom Hooks"
Cohesion: 1.0
Nodes (1): React Custom Hooks

### Community 133 - "Redux Saga"
Cohesion: 1.0
Nodes (1): Redux Saga

### Community 134 - "Keycloak Authentication"
Cohesion: 1.0
Nodes (1): Keycloak Authentication

### Community 135 - "Binary Search Tree Balanced vs Unbalance"
Cohesion: 1.0
Nodes (1): Binary Search Tree Balanced vs Unbalanced Diagram

### Community 136 - "HTML DOM Tree Structure Diagram"
Cohesion: 1.0
Nodes (1): HTML DOM Tree Structure Diagram

### Community 137 - "FocusFlow Logo - Productivity/Focus Bran"
Cohesion: 1.0
Nodes (1): FocusFlow Logo - Productivity/Focus Brand

### Community 138 - "Financial Independence Spectrum Chart"
Cohesion: 1.0
Nodes (1): Financial Independence Spectrum Chart

### Community 139 - "LoopBack Bookstore App UI"
Cohesion: 1.0
Nodes (1): LoopBack Bookstore App UI

### Community 140 - "npm audit Security Report with Vulnerabi"
Cohesion: 1.0
Nodes (1): npm audit Security Report with Vulnerabilities

### Community 141 - "Helmet HTTP Security Headers Response"
Cohesion: 1.0
Nodes (1): Helmet HTTP Security Headers Response

### Community 142 - "Node.js DevTools Inspect Panel in Edge B"
Cohesion: 1.0
Nodes (1): Node.js DevTools Inspect Panel in Edge Browser

### Community 143 - "Storybook Button Component Args Table"
Cohesion: 1.0
Nodes (1): Storybook Button Component Args Table

### Community 144 - "Docker Network with MongoDB and Mongo Ex"
Cohesion: 1.0
Nodes (1): Docker Network with MongoDB and Mongo Express

### Community 145 - "Docker Host-to-Container Port Mapping Di"
Cohesion: 1.0
Nodes (1): Docker Host-to-Container Port Mapping Diagram

### Community 146 - "Web Security Terminology Table"
Cohesion: 1.0
Nodes (1): Web Security Terminology Table

### Community 147 - "Session Riding Attack Overview"
Cohesion: 1.0
Nodes (1): Session Riding Attack Overview

### Community 148 - "TypeScript with Express Autocomplete Dem"
Cohesion: 1.0
Nodes (1): TypeScript with Express Autocomplete Demo

### Community 149 - "HTML Semantic Layout Diagram"
Cohesion: 1.0
Nodes (1): HTML Semantic Layout Diagram

### Community 150 - "React.use Hook"
Cohesion: 1.0
Nodes (1): React.use Hook

### Community 151 - "React Suspense"
Cohesion: 1.0
Nodes (1): React Suspense

### Community 152 - "SSR Hydration"
Cohesion: 1.0
Nodes (1): SSR Hydration

### Community 153 - "Java Primitive Types as Containers"
Cohesion: 1.0
Nodes (1): Java Primitive Types as Containers

### Community 154 - "React Thinking in React - Component Hier"
Cohesion: 1.0
Nodes (1): React Thinking in React - Component Hierarchy Diagram

### Community 155 - "React Context - Context Broadcasting to "
Cohesion: 1.0
Nodes (1): React Context - Context Broadcasting to All Descendants

### Community 156 - "React Single Page Application Diagram"
Cohesion: 1.0
Nodes (1): React Single Page Application Diagram

### Community 157 - "TypeScript NonNullable Utility Type"
Cohesion: 1.0
Nodes (1): TypeScript NonNullable Utility Type

## Knowledge Gaps
- **266 isolated node(s):** `Claude Code Planning Mode`, `Claude Code Thinking Mode`, `Rewinding Conversations`, `/compact Command`, `/clear Command` (+261 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `Git Tips`** (2 nodes): `git rm --cached Command`, `Git .gitignore Tracking Issue`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `CSS Grid`** (2 nodes): `CSS Grid Layout`, `Grid Terminology (line, track, cell, area, gap)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Promises & Async`** (2 nodes): `ES6 Promises`, `JavaScript Promises and Async/Await`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Testing (Jest)`** (2 nodes): `Testing with Jest (Node.js)`, `React Testing (Jest, React Testing Library, Vitest)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Package Managers`** (2 nodes): `Yarn Package Manager`, `npm (Node Package Manager)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Java Spring Boot`** (2 nodes): `Java Learning Plan (8-12 Weeks)`, `Spring Boot (Java Web Framework)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Mongoose ODM`** (2 nodes): `Mongoose ODM for MongoDB`, `Mongoose Schema`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Decorators`** (2 nodes): `TypeScript Decorator`, `Reflect Metadata`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `New Brainstorm Template`** (1 nodes): `New Brainstorm Template`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `List Template`** (1 nodes): `List Template`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `New Product Spec (PRD) Template`** (1 nodes): `New Product Spec (PRD) Template`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `PRD Problem Section`** (1 nodes): `PRD Problem Section`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `PRD Proposal Section`** (1 nodes): `PRD Proposal Section`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `PRD Plan / Launch Checklist`** (1 nodes): `PRD Plan / Launch Checklist`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `New Brainstorm Template`** (1 nodes): `New Brainstorm Template`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `AI Resume Reviewer Goal: Job Seekers Imp`** (1 nodes): `AI Resume Reviewer Goal: Job Seekers Improve Resumes`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Job Match Score Feature`** (1 nodes): `Job Match Score Feature`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Resume Analysis Dashboard`** (1 nodes): `Resume Analysis Dashboard`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `NextAuth.js with JWT`** (1 nodes): `NextAuth.js with JWT`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `FocusFlow YouTube Channel Setup`** (1 nodes): `FocusFlow YouTube Channel Setup`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `FocusFlow Brand Identity`** (1 nodes): `FocusFlow Brand Identity`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Soundraw.io (AI Music)`** (1 nodes): `Soundraw.io (AI Music)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ChatGPT (Scriptwriting)`** (1 nodes): `ChatGPT (Scriptwriting)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Canva (Thumbnails & Branding)`** (1 nodes): `Canva (Thumbnails & Branding)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `FocusFlow Monetization Strategy`** (1 nodes): `FocusFlow Monetization Strategy`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `FocusFlow Growth Strategy`** (1 nodes): `FocusFlow Growth Strategy`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML Basics Questions`** (1 nodes): `HTML Basics Questions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Semantic HTML Elements`** (1 nodes): `Semantic HTML Elements`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML Forms`** (1 nodes): `HTML Forms`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TanStack Query`** (1 nodes): `TanStack Query`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Advanced`** (1 nodes): `React Advanced`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES5 vs ES6`** (1 nodes): `ES5 vs ES6`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `DOM`** (1 nodes): `DOM`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Grid CSS`** (1 nodes): `Grid CSS`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Responsive Web Design`** (1 nodes): `Responsive Web Design`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Storybook`** (1 nodes): `Storybook`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML-CSS Training`** (1 nodes): `HTML-CSS Training`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Django`** (1 nodes): `Django`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Query Invalidation`** (1 nodes): `Query Invalidation`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Infinite Queries (useInfiniteQuery)`** (1 nodes): `Infinite Queries (useInfiniteQuery)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Parallel Queries`** (1 nodes): `Parallel Queries`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Dependent Queries`** (1 nodes): `Dependent Queries`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Grid Auto Placement`** (1 nodes): `Grid Auto Placement`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES6 Arrow Functions`** (1 nodes): `ES6 Arrow Functions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES6 let and const (Block Scope)`** (1 nodes): `ES6 let and const (Block Scope)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES6 Spread Operator`** (1 nodes): `ES6 Spread Operator`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES6 Object Destructuring`** (1 nodes): `ES6 Object Destructuring`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `ES6 Template Literals`** (1 nodes): `ES6 Template Literals`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Accessibility (WCAG, ARIA)`** (1 nodes): `React Accessibility (WCAG, ARIA)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Code Splitting (React.lazy, Suspen`** (1 nodes): `React Code Splitting (React.lazy, Suspense)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Error Boundaries`** (1 nodes): `React Error Boundaries`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Higher-Order Components (HOC)`** (1 nodes): `Higher-Order Components (HOC)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Performance Optimization (memo, Pr`** (1 nodes): `React Performance Optimization (memo, Profiler)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML-CSS Training: Git Branch & PR Conve`** (1 nodes): `HTML-CSS Training: Git Branch & PR Conventions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `CSS @import Performance Issue`** (1 nodes): `CSS @import Performance Issue`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JavaScript Syntax and Variables`** (1 nodes): `JavaScript Syntax and Variables`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JavaScript Arrays and Methods`** (1 nodes): `JavaScript Arrays and Methods`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JavaScript Classes and OOP`** (1 nodes): `JavaScript Classes and OOP`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JavaScript Generator Functions`** (1 nodes): `JavaScript Generator Functions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JavaScript Performance Tips`** (1 nodes): `JavaScript Performance Tips`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Django Project Setup`** (1 nodes): `Django Project Setup`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Django REST Swagger (drf-yasg)`** (1 nodes): `Django REST Swagger (drf-yasg)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node.js File System Module (fs)`** (1 nodes): `Node.js File System Module (fs)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node.js TCP/UDP Sockets`** (1 nodes): `Node.js TCP/UDP Sockets`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node.js Event Emitter`** (1 nodes): `Node.js Event Emitter`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node.js Debugging`** (1 nodes): `Node.js Debugging`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Working with SQL Databases (MySQL, Postg`** (1 nodes): `Working with SQL Databases (MySQL, PostgreSQL)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Persisting Data with Redis`** (1 nodes): `Persisting Data with Redis`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Jest Mock Functions`** (1 nodes): `Jest Mock Functions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Jest with MongoDB`** (1 nodes): `Jest with MongoDB`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Web Protocols with Node.js (HTTP, WebSoc`** (1 nodes): `Web Protocols with Node.js (HTTP, WebSocket, SMTP)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `WebSocket Server (ws module)`** (1 nodes): `WebSocket Server (ws module)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `SMTP Email Server (Node.js)`** (1 nodes): `SMTP Email Server (Node.js)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Working with NoSQL Databases (MongoDB, M`** (1 nodes): `Working with NoSQL Databases (MongoDB, Mongoose)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Mongoose ODM`** (1 nodes): `Mongoose ODM`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Express.js Middleware`** (1 nodes): `Express.js Middleware`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Express.js EJS View Engine`** (1 nodes): `Express.js EJS View Engine`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node Version Manager (nvm)`** (1 nodes): `Node Version Manager (nvm)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `LoopBack Microservice Generator`** (1 nodes): `LoopBack Microservice Generator`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `GraphQL API (Node.js microservices)`** (1 nodes): `GraphQL API (Node.js microservices)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `express-session Authentication`** (1 nodes): `express-session Authentication`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `JSON Pollution Attack Prevention`** (1 nodes): `JSON Pollution Attack Prevention`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTTP Parameter Pollution Defense`** (1 nodes): `HTTP Parameter Pollution Defense`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `npm audit Vulnerability Detection`** (1 nodes): `npm audit Vulnerability Detection`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Storybook UI Component Workshop`** (1 nodes): `Storybook UI Component Workshop`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Storybook ArgTypes`** (1 nodes): `Storybook ArgTypes`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Data Leakage Channels`** (1 nodes): `Data Leakage Channels`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Session Riding Attacks`** (1 nodes): `Session Riding Attacks`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Class Member Visibility (publ`** (1 nodes): `TypeScript Class Member Visibility (public/protected/private)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Interface`** (1 nodes): `TypeScript Interface`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Intersection Types`** (1 nodes): `TypeScript Intersection Types`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Tuple Types`** (1 nodes): `TypeScript Tuple Types`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Functions (Overloads, Generic`** (1 nodes): `TypeScript Functions (Overloads, Generics, Callbacks)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Union Types`** (1 nodes): `TypeScript Union Types`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Type Aliases`** (1 nodes): `TypeScript Type Aliases`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript Literal Types`** (1 nodes): `TypeScript Literal Types`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `SEO Best Practices (HTML/CSS)`** (1 nodes): `SEO Best Practices (HTML/CSS)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React useOptimistic Hook`** (1 nodes): `React useOptimistic Hook`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Switching JDK Version on macOS`** (1 nodes): `Switching JDK Version on macOS`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `MongoDB Query API`** (1 nodes): `MongoDB Query API`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `MongoDB CRUD Operations`** (1 nodes): `MongoDB CRUD Operations`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `MongoDB Aggregation Pipelines`** (1 nodes): `MongoDB Aggregation Pipelines`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `MongoDB Sessions and Transactions`** (1 nodes): `MongoDB Sessions and Transactions`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `MongoDB Schema Validation`** (1 nodes): `MongoDB Schema Validation`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Index Search Key`** (1 nodes): `Index Search Key`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Index Data Reference Pointer`** (1 nodes): `Index Data Reference Pointer`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTMLCollection`** (1 nodes): `HTMLCollection`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `NodeList`** (1 nodes): `NodeList`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `NestJS ORM (Object-Relational Mapping)`** (1 nodes): `NestJS ORM (Object-Relational Mapping)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Re-rendering and Commit`** (1 nodes): `React Re-rendering and Commit`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React State Update Batching`** (1 nodes): `React State Update Batching`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `useRef Hook`** (1 nodes): `useRef Hook`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Custom Hooks`** (1 nodes): `React Custom Hooks`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Redux Saga`** (1 nodes): `Redux Saga`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Keycloak Authentication`** (1 nodes): `Keycloak Authentication`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Binary Search Tree Balanced vs Unbalance`** (1 nodes): `Binary Search Tree Balanced vs Unbalanced Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML DOM Tree Structure Diagram`** (1 nodes): `HTML DOM Tree Structure Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `FocusFlow Logo - Productivity/Focus Bran`** (1 nodes): `FocusFlow Logo - Productivity/Focus Brand`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Financial Independence Spectrum Chart`** (1 nodes): `Financial Independence Spectrum Chart`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `LoopBack Bookstore App UI`** (1 nodes): `LoopBack Bookstore App UI`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `npm audit Security Report with Vulnerabi`** (1 nodes): `npm audit Security Report with Vulnerabilities`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Helmet HTTP Security Headers Response`** (1 nodes): `Helmet HTTP Security Headers Response`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Node.js DevTools Inspect Panel in Edge B`** (1 nodes): `Node.js DevTools Inspect Panel in Edge Browser`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Storybook Button Component Args Table`** (1 nodes): `Storybook Button Component Args Table`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Docker Network with MongoDB and Mongo Ex`** (1 nodes): `Docker Network with MongoDB and Mongo Express`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Docker Host-to-Container Port Mapping Di`** (1 nodes): `Docker Host-to-Container Port Mapping Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Web Security Terminology Table`** (1 nodes): `Web Security Terminology Table`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Session Riding Attack Overview`** (1 nodes): `Session Riding Attack Overview`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript with Express Autocomplete Dem`** (1 nodes): `TypeScript with Express Autocomplete Demo`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `HTML Semantic Layout Diagram`** (1 nodes): `HTML Semantic Layout Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React.use Hook`** (1 nodes): `React.use Hook`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Suspense`** (1 nodes): `React Suspense`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `SSR Hydration`** (1 nodes): `SSR Hydration`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Java Primitive Types as Containers`** (1 nodes): `Java Primitive Types as Containers`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Thinking in React - Component Hier`** (1 nodes): `React Thinking in React - Component Hierarchy Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Context - Context Broadcasting to `** (1 nodes): `React Context - Context Broadcasting to All Descendants`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `React Single Page Application Diagram`** (1 nodes): `React Single Page Application Diagram`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `TypeScript NonNullable Utility Type`** (1 nodes): `TypeScript NonNullable Utility Type`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Notes Index` connect `Templates & Interview Prep` to `Data Structures & Algorithms`, `CI/CD & AWS Deployment`?**
  _High betweenness centrality (0.010) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `React Developer Interview Questions` (e.g. with `JavaScript Concepts` and `Front-end Developer Interview Questions`) actually correct?**
  _`React Developer Interview Questions` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Claude Code Planning Mode`, `Claude Code Thinking Mode`, `Rewinding Conversations` to the rest of the system?**
  _266 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `React & Redux Ecosystem` be split into smaller, more focused modules?**
  _Cohesion score 0.08 - nodes in this community are weakly interconnected._
- **Should `Templates & Interview Prep` be split into smaller, more focused modules?**
  _Cohesion score 0.1 - nodes in this community are weakly interconnected._
- **Should `Claude Code Tooling` be split into smaller, more focused modules?**
  _Cohesion score 0.11 - nodes in this community are weakly interconnected._
- **Should `Web Dev Course & Node.js` be split into smaller, more focused modules?**
  _Cohesion score 0.14 - nodes in this community are weakly interconnected._