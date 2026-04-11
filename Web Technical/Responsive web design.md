---
Created: 2023-06-21T16:11
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://web.dev/responsive-web-design-basics/#viewport-media-queries
  - https://www.interaction-design.org/literature/topics/grid-systems
  - https://www.w3schools.com/html/html_responsive.asp
  - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries#targeting_media_types
Reviewed: true
Edited: 2025-05-10T14:45
---
  

> **==_The use of mobile devices to surf the web continues to grow at an astronomical pace, and these devices are often constrained by display size and require a different approach to how content is laid out on the screen._==**

  

https://github.com/liemgumball/html-css-training

# Responsive web design

- **Using the meta viewport** value `width=device-width` instructs the page to match the screen's width in device-independent pixels.
- ==[**Some browsers**](https://css-tricks.com/probably-use-initial-scale1/)== keep the page's width constant when rotating to landscape mode, and zoom rather than reflow to fill the screen. Adding the value `initial-scale=1` instructs browsers to establish a 1:1 relationship between CSS pixels and device-independent pixels regardless of device orientation, and allows the page to take advantage of the full landscape width.

> **==_Smartphones are important in responsive web design because they have become a dominant device for accessing the internet._==**

- **Desktop first and mobile first**
    
    - **Desktop first**
        
        Desktop-first is the traditional approach where the website design and development process starts with designing and optimizing for desktop or larger screens. This approach focuses on creating a user experience that is primarily tailored for desktop users.
        
        After the desktop version is designed and developed, the website is then adapted and modified to be responsive for smaller screens, such as tablets and smartphones.
        
    - **Mobile first**
        
        Mobile-first is an approach where the website design and development process starts with designing and optimizing for mobile devices, typically focusing on smaller screens. This approach emphasizes creating a user experience that is tailored for mobile users and their specific needs.
        
        After the mobile version is designed and developed, the website is then progressively enhanced and expanded to accommodate larger screens, such as tablets and desktops.
        
        ==**The feature of the mobile-first process is that we only use the min-width media features and nothing else.**==
        
    
    ### The reason why we should use Mobile-first?
    
    - Focus on the interface on the phone as much as possible because the trend of using the phone is increasing.
    - Avoid rewriting CSS, as a mobile CSS can be reused on desktop. But if you write CSS on the desktop first, in the mobile interface you still have to rewrite it if you want to customize.
    - Easy to deploy and manage, upgrade later.
    - Avoid display errors on the phone due to customizing from CSS on the desktop.
    - And many other reasons
- **Ensure an accessible viewport**
    - `initial-scale`
    - `minimum-scale`
    - `maximum-scale`
    - `user-scalable` : yes or no

- **Images**
    - An image has fixed dimensions and if it is larger than the viewport will cause a scrollbar. A common way to deal with this problem is to give all images a `max-width` of `100%`. This will cause the image to shrink to fit the space it has, should the viewport size be smaller than the image.

- **Layout**
    
    - **Flexbox**
    
    ```CSS
    .items {
      display: flex;
      justify-content: space-between;
    }
    ```
    
    - **[[Grid CSS|Grid Layout]]**
        
        CSS Grid Layout allows for the straightforward creation of flexible grids. If we consider the earlier floated example, rather than creating our columns with percentages, we could use grid layout and the `fr` unit, which represents a portion of the available space in the container.
        
    
    ```CSS
    .container {
      display: grid;
      grid-template-columns: 1fr 3fr;
    }
    ```
    
    - **Multiple-column layout**
        
        For some types of layout you can use Multiple-column Layout (Multicol), which can create responsive numbers of columns with the `column-width` property. In the demo below, you can see that columns are added if there is room for another `200px` column.
        
- **Use CSS media queries for responsiveness**
    
    **Media queries** allow you to apply CSS styles depending on a device's general type (such as print vs. screen) or other characteristics such as screen resolution or browser [viewport](https://developer.mozilla.org/en-US/docs/Glossary/Viewport) width. Media queries are used for the following:
    
    ```HTML
    <!DOCTYPE html>
    <html lang="en">
      <head>
        …
        <link rel="stylesheet" href="print.css" media="print">
        …
      </head>
      …
    ```
    
    **OR**
    
    ```CSS
    @media print {
      /* print styles go here */
    }
    ```
    
    - **Media queries based on viewport size**
        
        Media queries enable us to create a responsive experience where specific styles are applied to small screens, large screens, and anywhere in between. The feature we are detecting here is therefore screen size, and we can test for the following things.
        
        - `width` (`min-width`, `max-width`)
        - `height` (`min-height`, `max-height`)
        - `orientation`
        - `aspect-ratio`
    - **Media queries based on device capability**
        
        - `hover`
        - `pointer`
        - `any-hover`
        - `any-pointer`
        
        **Notice!** Be very careful when using these. Forcing a user to switch to a mouse when they are using their touchscreen is not very friendly! However, `any-hover` and `any-pointer` may be useful if it is important to work out what kind of device a user has. For example, a laptop with a touchscreen and trackpad should match coarse and fine pointers, in addition to the ability to hover.
        
    - **Targeting media types**
        
        Media types describe the general category of a given device. Although websites are commonly designed with screens in mind, you may want to create styles that target special devices such as printers or audio-based screen readers
        
        ```CSS
        @media screen, print {
          /* … */
        }
        ```
        
    - **Targeting media features**
        
        Media features describe the specific characteristics of a given [user agent](https://developer.mozilla.org/en-US/docs/Glossary/User_agent), output device, or environment. For instance, you can apply specific styles to widescreen monitors, computers that use mice, or to devices that are being used in low-light conditions.
        
        ```CSS
        @media (hover: hover) {
          /* … */
        }
        
        @media (max-width: 1250px) {
          /* … */
        }
        ```
        
    - **Combining multiple types or features**
        
        The `and` keyword combines a media feature with a media type _or_ other media features.
        
        ```CSS
        @media screen and (min-width: 30em) and (orientation: landscape) {
          /* … */
        }
        ```
        
    
    - **How to choose breakpoints**
        
        Don't define breakpoints based on device classes. Defining breakpoints based on specific devices, products, brand names, or operating systems that are in use today can result in a maintenance nightmare. Instead, the content itself should determine how the layout adjusts to its container.
        
        - `max-width: 320px` (mobile, vertical display)
        - `max-width: 480px` (mobile, horizental display)
        - `max-width: 600px` (tablet, vertical display)
        - `max-width: 800px` (tablet, horizental display)
        
        - `max-width: 768px` (big tablet, vertical display)
        
        - `max-width: 1024px` (big tablet, horizental display)
        - `min-width: 1025px` (normal desktop).
        
        To insert a breakpoint at `600px`, create two media queries at the end of your CSS for the component, one to use when the browser is `600px` and below, and one for when it is wider than `600px`.
        
        ```CSS
        @media (max-width: 600px) {
        
        }
        
        @media (min-width: 601px) {
        
        }
        ```
        
    
    - **Pick minor breakpoint when necessary**
        
        ```CSS
        @media (min-width: 360px) {
          body {
            font-size: 1.0em;
          }
        }
        
        @media (min-width: 500px) {
          .seven-day-fc .temp-low,
          .seven-day-fc .temp-high {
            display: inline-block;
            width: 45%;
          }
        
          .seven-day-fc .seven-day-temp {
            margin-left: 5%;
          }
        
          .seven-day-fc .icon {
            width: 64px;
            height: 64px;
          }
        }
        ```
        
    - **Optimize text for reading**
        
        On smaller screens, the Roboto font at `1em` works perfectly giving 10 words per line, but larger screens require a breakpoint. In this case, if the browser width is greater than `575px`, the ideal content width is `550px`.
        
        ```CSS
        @media (min-width: 575px) {
          article {
            width: 550px;
            margin-left: auto;
            margin-right: auto;
          }
        }
        ```
        
    - **Syntax improvements in Level 4**
        
        The Media Queries Level 4 specification includes some syntax improvements to make media queries using features that have a "range" type, for example width or height, less verbose.
        
        ```CSS
        @media (30em <= width <= 50em) {
          /* … */
        }
        ```
        

## QUESTION & ANSWER

1. How to configure css only to work on devices?
    
    Use media queries to configure styles that only apply to specific devices or screen sizes
    
    ```CSS
    @media (max-width: 768px) {
      /* CSS rules for tablets */
      /* Example: */
      body {
        font-size: 16px;
      }
    }
    ```
    
    CSS media queries can also be used to target specific ==device orientations== (==portrait== or ==landscape==) and ==printing conditions==
    
    ```CSS
    @media (orientation: portrait) {
      body {
        background-color: lightblue;
      }
    }
    
    @media (orientation: landscape) {
      body {
        background-color: lightgreen;
      }
    }
    
    @media print {
      body {
        font-size: 12pt;
      }
    }
    ```
    
2. How to use media query: min-width, max-width?
    
    Combining `**min-width**` and `**max-width**` media queries allows you to create responsive designs that adapt to different screen sizes. By defining specific styles for different width ranges, you can optimize the layout and appearance of your website for various devices and ensure a better user experience across different screen sizes.
    
    ```CSS
    @media (min-width: 480px) and (max-width: 767px) {
      body {
        font-size: 14px;
      }
    }
    ```
    
3. Write a media query have conditional “or” and “and”
    
    Can not use `or` as a logical operator in CSS media queries. Instead, we use a comma `,`
    
    ```CSS
    @media (min-width: 480px) and (max-width: 767px),
    (min-height: 320px) and (max-height: 599px) {
      body {
        background-color: lightgreen;
      }
    }
    ```
    
      
    
4. What is the grid system?
    
    Grid systems are aids designers use to build designs, arrange information and make consistent user experiences. They include rule of thirds, golden section (golden ratio), single-column, multi-column, modular, baseline and responsive grid systems.
    
    > One must learn how to use the grid. It is an art that requires practice.
    > 
    > _― Josef Müller-Brockmann, Graphic designer, author, educator and International Typographic Style pioneer_
    
      
    
5. Compare grid and flex?
    
    - **Grid**
        
        CSS Grid layout is a ==two-dimensional== grid-based layout system with rows and columns, making it easier to design web pages ==without having to use floats and positioning.==
        
    - **Flexbox**
        
        The CSS Flexbox offers a ==one-dimensional== layout. It is helpful in allocating and aligning the space among items in a container (made of grids). It works with all kinds of display devices and screen sizes.
        
    
    > ==**This means Flexbox can work on either row or columns at a time, but Grids can work on both.**==
    
      
    
    - **The major Uniqueness between Flexbox and Grids is that the** ==**former**== **works on ==content== while the latter is based on the ==layout==**
        
        The Flexbox layout is best suited to application components and small-scale layouts, while the Grid layout is designed for larger-scale layouts that are not linear in design.
        
          
        
    
    |Property|Grid|Flexbox|
    |---|---|---|
    |Dimension|Two – Dimensional|One – Dimensional|
    |Features|Can flex combination of items through space-occupying Features|Can push content element to extreme alignment|
    |Support Type|Layout First|Content First|
    
6. How to use icon font?
    
    - Search for the Icon font, Choose an icon font library, such as Font Awesome or Material Icons
    - Include the Font file to the project
    
    ```HTML
    <link rel="stylesheet" href="path/to/icon-font/font-awesome.min.css">
    <link rel="stylesheet" href="<https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css>">
    ```
    
    - Add icon markup to the HTML file: use the appropriate CSS class or HTML element provided by the icon font library to display the desired icon.
    - Style and Customize the Icon

  

## Some useful knowledges when writing CSS Responsive

- In addition to the breakpoint unit of `px`, the length units in the website should be ==percent==. Or rather, use ==relative units==.
- It is recommended to use `max-width` instead of `width` to avoid fixed width.
- Use `display: none` for the elements that need to be hidden on each device that you want to hide. And `display: block` on devices that need to be displayed.
- Use the `!important` option if you need to override ==CSS.==

## Related

- [[Grid CSS]] - CSS Grid layout system
- [[HTML-CSS training]] - HTML and CSS fundamentals