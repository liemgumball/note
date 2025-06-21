---
Created: 2024-07-23T15:53
Class: mgm
Type: A12-project
Reviewed: false
Edited: 2024-08-06T20:32
---
# Introduction

## What is A12?

**A12** is an development platform for web-based business applications. It provides developers a set of ==scalable components== as well as ==client/server application== infrastructure.

[[Questions]]

## How does A12 works?

> _From Models to Applications_

A12 is a model-driven approach to business software. It provides a set of concepts, components and tools for creating modern, document-oriented web applications.

> [!important] The core idea of
> 
> **A12** is to encapsulate domain-specific knowledge in models. By using a set of powerful tools, domain experts and business analysts are able to create and modify these models - without the need to touch any code.

### Focus on ==Documents== and ==Forms==

Most business transactions are handled via some kind of documents. These include, for example, _==contracts==, ==purchase orders==, and ==different kinds of requests==_. When it comes to digitizing documents, online forms play a vital role.

They specify the structure of documents and determine which data is needed for the business transaction.

The **A12** tools and components have a strong focus on ==modeling business processes and documents== using a _==form-based approach==_. They provide the means to create complex forms with up to thousands of data fields, dependencies and validation rules and bring them into web applications.

---

# Data First - The Modeling Philosophy of A12

> _**A12** is all about models._

The **A12** platform enables experts and analysts to create and adapt business applications. It aims at building applications much faster than usual and allows for business-driven adjustments on the fly. This is accomplished in large parts thanks to a ==model-based approach==.

  

### The Bedrock of Business Applications: ==Data== and ==Validation== Criteria

The first step of creating application with the **A12** involves the creation of ==**Document Models**==**.**

> [!important] **For example**
> 
>   
> If we want to create a stock management application. We need a structure outline for ==articles==.  
> - An ==articles== has `name`, represented as a `string`  
> - A  
> `serial number`  
> - A  
> `price`

Additionally, there are rules for the validity of data. The `price` ==cannot be negative==…

For conveniently adding and modifying validation criteria, the editor features `autocomplete` and `syntax highlighting` for the [Kernel Language](https://docs.geta12.com/docs/content/2024.06/OVERALL/202406/asciidoc/what_is_a12/index.html#ValidationLanguage).

### Content-Related User Interface Design

The ==**Form Model Editor**== pursues a rather abstract but very powerful way of modeling user interfaces.

This modeling philosophy enables ==business experts to focus on their domain and model complete user interfaces== on their own. The graphical finish is completely decoupled and not specified in the Form Model.

> [!important] Each
> 
> **A12 UI** model refers to ==at least one== **A12 Document Model**.

---

## Plasma Design - UI/UX for Business Applications

> _Interface and interaction design usually take up a lot of time and effort in individual software projects. **Plasma Design** by ==mgm== aims at speeding up the process._

Business applications are driven by ==function== and by the ==necessity== of performing certain tasks. It is more important to give users a reliable tool than to dazzle them with fancy images or flashy design effects. ==Functional considerations== are ==more important== than ==aesthetic considerations== - which are not to say that a reduced, functional design cannot be appealing and elegant in a puristic fashion.

### Benefits of Plasma Design

> _In a nutshell: ==speed==._

Projects can start immediately with a design that is optimized for business applications. No individual design and interaction specifications are required.

---

## Modeling Platform

**A12** provides a set of tools for business experts and analysts. Using these tools, they can create domain-specific models and build their own multilingual business applications. ==Programming skills are not required==. The modeled business logic and structures of user interfaces can be easily reused.

![[Screenshot_2024-07-25_at_11.31.23.png]]

Main Modeling Dimensions (Tools)

---

# Components That Make up A12

**A12** follows a modular approach when it comes to creating business applications. While business logic, validation rules, and the structural layouts of user interfaces are encapsulated in models, the following building blocks are responsible for bringing the A12 applications and their models to life.

![[Screenshot_2024-07-25_at_11.15.23.png]]

Runtime Platform

## **1. Client**

Enabling declaration of core application aspects, modules, navigation, screens, and major interaction patterns. It take care of request handling, data retrieval and processing, state management and orchestration of lower level components like UI engines.

## **2.** ==**Engines**==

==Model driven UI components== based on [[A12 Introduction]] UI/UX concept and the [[A12 Introduction]] library. This cover the current forms, overviews, and trees which require configuration by models but also provide a programming API in TypeScript.

## **3. Widgets**

Reusable, lower level ==UI components== like grids, trees or date-pickers that follow the Plasma Design conventions and UX concepts.

## **4. Kernel**

Definition of documents and Document Model along with modeling tools. A domain-specific language for ==model-based computation== and ==validation== including parser, runtime components and a programming API in various languages.

## **5. Data Services**

Data Service API and implementations to deal with models and documents supporting `creation`, `retrieval`, `update`, `deletion` and `querying`. This is provided in ==**Typescript**== for the client side and ==**Java**== for client and server side.

## **6. Workflows**

**A12 Workflows** provides a lightweight service, which integrates **Business Process Model and Notation (BPMN)** modeling capabilities into **A12**, enabling graphical modeling of server-side workflows and their execution.

## **7. UAA** _**(User Management, Authentication and Authorization)**_

## A12 Architecture

![[Class Notes/A12 Introduction/attachments/Untitled.png|Untitled.png]]

---

# Frontend

> [!info]  
>  
> [https://docs.geta12.com/docs/?release=2024.06#product:overall,artifact:dev_tutorial_intro_intro,content:asciidoc,scene:iMjyF304](https://docs.geta12.com/docs/?release=2024.06#product:overall,artifact:dev_tutorial_intro_intro,content:asciidoc,scene:iMjyF304)