---
Created: 2023-10-09T13:49
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://storybook.js.org/tutorials/intro-to-storybook/react/en/simple-component/
Reviewed: true
Edited: 2024-03-05T16:49
---
> [!important] **==Storybook==**
> 
> runs alongside your app in ==development mode==. It helps you build ==**UI**== components isolated from the business logic and context of your app.

## Get started

> [!important] ==**Storybook**==
> 
> can ==not== be create in an _empty project_

  

```Bash
pnpm create vite@latest my-react-app --template react-ts-swc
```

  

```Bash
cd my-react-app

# Init storybook
pnpx sb init -s

# Install dependencies
pnpm install

# Run storybook
pnpm run storybook
```

  

## Get set up

> [!info] GitHub - liemgumball/internship_AlgilityIO at feature/react-advanced  
> Contribute to liemgumball/internship_AlgilityIO development by creating an account on GitHub.  
> [https://github.com/liemgumball/internship_AlgilityIO/tree/feature/react-advanced](https://github.com/liemgumball/internship_AlgilityIO/tree/feature/react-advanced)  

  

## ArgTypes

==ArgTypes== specify the behavior of ==args==. By specifying the type of an arg, you constrain the values that it can accept and provide information about args that are not explicitly set

![[Web Technical/Storybook/attachments/Untitled.png|Untitled.png]]

> [!info] ArgTypes  
> Storybook is a frontend workshop for building UI components and pages in isolation.  
> [https://storybook.js.org/docs/react/api/arg-types](https://storybook.js.org/docs/react/api/arg-types)