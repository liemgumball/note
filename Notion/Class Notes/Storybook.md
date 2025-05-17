Created: October 9, 2023 1:49 PM
Class: Agility IO InternShip
Type: Front-end
Materials: https://storybook.js.org/tutorials/intro-to-storybook/react/en/simple-component/
Reviewed: Yes
Edited: March 5, 2024 4:49 PM

<aside>
<img src="https://www.notion.so/icons/drafts_pink.svg" alt="https://www.notion.so/icons/drafts_pink.svg" width="40px" /> **Storybook** runs alongside your app in development mode. It helps you build **UI** components isolated from the business logic and context of your app.

</aside>

## Get started

<aside>
💡 **Storybook** can not be create in an *empty project*

</aside>

```bash
pnpm create vite@latest my-react-app --template react-ts-swc
```

```bash
cd my-react-app

# Init storybook
pnpx sb init -s

# Install dependencies
pnpm install

# Run storybook
pnpm run storybook
```

## Get set up

[GitHub - liemgumball/internship_AlgilityIO at feature/react-advanced](https://github.com/liemgumball/internship_AlgilityIO/tree/feature/react-advanced)

## ArgTypes

ArgTypes specify the behavior of args. By specifying the type of an arg, you constrain the values that it can accept and provide information about args that are not explicitly set

![Untitled](Notion/Class%20Notes/Storybook/Untitled.png)

[ArgTypes](https://storybook.js.org/docs/react/api/arg-types)