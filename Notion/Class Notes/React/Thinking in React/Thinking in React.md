In ==**React**==, a component is a self-contained, reusable piece of ==**UI**== that encapsulates a specific functionality or view. Components are the building blocks of a React application, and they enable you to break down the ==user interface== into smaller, manageable parts

  

![[Notion/Class Notes/React/Thinking in React/attachments/Untitled.png|Untitled.png]]

  

## Composing Components

Components can refer to other components in their output. This lets us use the same ==component abstraction== for any level of detail. A button, a form, a dialog, a screen: in React apps, all those are commonly expressed as components.

  

## Extracting Component

> [!important] Don’t be afraid to split components into smaller components.

  

## **Props are Read-Only**

React is pretty flexible but it has a single strict rule

> [!important] **All**
> 
> ==**React**== **components must act like** ==**pure**== **functions with respect to their props.**

  

# Thinking in React

> [!info] Thinking in React – React  
> A JavaScript library for building user interfaces  
> [https://legacy.reactjs.org/docs/thinking-in-react.html](https://legacy.reactjs.org/docs/thinking-in-react.html)  

One of the many great parts of ==**React**== is how it makes you think about apps as you build them. In this document, we’ll walk you through the thought process of building a searchable product data table using React.

![[Notion/Class Notes/React/Thinking in React/attachments/Untitled 1.png|Untitled 1.png]]

## Step 1: **Break The UI Into A Component Hierarchy**

==**UI**== and **==data models==** tend to adhere to the same ==_information architecture_==. Separate your UI into components, where each component matches one piece of your data model.

![[Notion/Class Notes/React/Thinking in React/attachments/Untitled 2.png|Untitled 2.png]]

1. `**FilterableProductTable**` **(orange):** contains the entirety of the example
2. `**SearchBar**` **(blue):** receives all _user input_
3. `**ProductTable**` **(green):** displays and filters the _data collection_ based on _user input_
4. `**ProductCategoryRow**` **(turquoise):** displays a heading for each _category_
5. `**ProductRow**` **(red):** displays a row for each _product_

## **Step 2: Build A Static Version in React**

The easiest way is to build a version that takes your ==**data model**== and renders the ==**UI**== but has ==no interactivity==.

![[Notion/Class Notes/React/Thinking in React/attachments/Untitled 3.png|Untitled 3.png]]

## **Step 3: Identify The Minimal (but complete) Representation Of UI State**

To make your ==**UI**== interactive, you need to be able to trigger changes to your underlying data model. React achieves this with ==**state**==.

> [!important] The key here is 
> 
> ==**DRY**== _Don’t Repeat Yourself_

Figure out the absolute minimal representation of the state your application needs and compute everything else you need on-demand.

## **Step 4: Identify Where Your State Should Live**

OK, so we’ve identified what the minimal set of app ==state== is. Next, we need to identify which component ==mutates==, or ==_owns_==, this state.

> [!important] **This is often the most challenging part for newcomers to understand**

## **Step 5: Add Inverse Data Flow**

==**React**== makes this data flow explicit to help you understand how your program works, but it does require a little more typing than traditional ==two-way== data binding.