---
Created by: liemgumball
Created time: 2024-06-25T15:27
tags:
  - Frontend
  - Interview
URL: https://www.geeksforgeeks.org/front-end-developer-interview-questions/
---
# Front-end Developer Interview Questions

## Front-end development

It is creating ==**UI**== for web pages. It deals with displaying data which sent by back-end in an ==interactive== and ==easy-to-read== format.

  

### Interview Question for ==Fresher==

1. What is ==**HTML**==?
    
    **HTML** stands for ==**Hyper Text Markup Language**== consist with different tags to define a structure of the web page.
    
2. What is ==**Semantic**== ==elements== in **HTML**?
    
    Semantic elements that ==contain the meaning== of the content and the structure of the HTML document. These elements contain content that is ==related to their names== or ==reflects their names==: `header` `main` `footer` `section` `article` `aside` etc.
    
3. Empty elements
    
    Elements that don’t require and closing tag followed by the opening tag
    
    `img` `input` `br` `hr`
    

4. Differentiate between the ==**Inline**== and the ==**Block**== elements in **HTML**

The Block elements automatically start from a new line and take up the hole view port width. `div` `h1` `p` etc.

The Inline element does not start from a new line ( the `margin` and `padding` may ==not== have the expected effect) `a` `strong` `input` `img` etc.

1. List in **HTML**
    1. ==Unordered list==: `ul` `li` , by default it presents items in bulleted dot
    2. ==Ordered list==: `ol` `li` , be default it presents items in numeric digits
    3. Definition list: a special kind of list which is used to list the or terms with their definitions. It can be defined using the `dl`, `dt` and `dd` tags. `dt` – definition term, `dd` – definition description
        
        ```HTML
        <dl>
            <dt>First  term</dt>
            <dd>Definition 1</dd>
        
            <dt>Second term</dt>
            <dd>Definition 2</dd>
        
            <dt>Third term</dt>
            <dd>Definition 3</dd>
        </dl>
        ```
        
2. **HTML5** structure
    
    > [!info] Stop using so many divs! An intro to semantic HTML  
    > Sure, divs are great and all, but they give no information about their purpose within the document structure.  
    > [https://dev.to/kenbellows/stop-using-so-many-divs-an-intro-to-semantic-html-3i9i](https://dev.to/kenbellows/stop-using-so-many-divs-an-intro-to-semantic-html-3i9i)  
    
3. Different between `div` and `span`
    
    |`**<div>**`|`**<span>**`|
    |---|---|
    |It is a ==block== element.|It is an ==inline== element.|
    |It can be used to group and structure the content of the web page.|It is mainly used to interact and style the particular part of the web page.|
    |It represents a bigger section of the web page.|It is used to target small parts of the web page.|
    |It starts from a new line and takes up the full width available.|It does not starts from a new line and takes up only the required width as taken by the content.|
    
4. Why the `<meta charset="UFT-8">` tag is used?
    
    It is used to set the ==character encoding== of the characters for the document to **UTF-8** to properly display the text and the special characters on the web page.
    
5. What is **CSS**?
    
    **CSS** stands for the ==Cascading Style Sheets==. It helps to design and style the web page to make it attractive for users. **CSS** provides us a lot of ==selectors== to select the HTML elements and style them according to the requirements.
    
6. **CSS** selectors
    - ID selector
    - Class selector
    - Element selector
    - Pseudo selector
    - Attribute selector `input[type="text"]`
7. `box-sizing` in **CSS**
    
    It is used to determine the way of ==calculating== the ==height== and ==width== of a element. It determines whether the ==border== and ==padding== will be ==included or not== to calculate the height and width of the element. The common values are `**content-box**`**(**_**default)**_ and `**border-box.**`
    
8. **CSS** ==**pre-processors**== and their advantage over pure **CSS**?
    
    A ==**CSS preprocessor**== is created using a scripting language that ==extends== the **CSS** rules and processed in the regular **CSS** by creating a file with `**.css**` extension. Mostly used **CSS** preprocessors are ==**SASS**== and ==**SCSS**==**.**
    
9. **Media Queries in CSS**
    
    Media queries are the block of **CSS** code defined for a ==particular width== or ==range of the width==. These can be defined using the `@media` keyword with screen to specify styles for a particular width or range of width. They are used very commonly to create ==responsive designs==.
    
10. **CSS sprites**
    
    It’s a technique that is used to ==compress multiple images== available on the web page into ==a single image file==. It arranges all the images in a grid-like layout. The `**background-position**` property of **CSS** can be used to display the different parts of the combined image ==as background== for different elements. 
    
    It ==improves the web performance== by reducing the server requests as the website has to ==request only a single image== now instead of requesting multiple images.
    

  

### Interview Questions for Experienced

1. **What is JavaScript?**
2. What is difference between `==` and `===` in **JavaScript**?
    
    The `==` operator checks ==only for the values== of the operands and return true if the values are same.
    
    On the other hand, the `===` operator not only checks for the ==values== of the operands but ==also for the types== of the operands.
    
    ```JavaScript
    3 == "3" // Returns true
    3 === "3" // Returns false
    ```
    
3. What is **DOM?**
    
    **DOM** stands for ==**Document Object Model**==**,** it is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The **DOM** represents the document ==as== ==**nodes**== and ==**objects**==; that way, programming languages can ==interact with the page.==
    
    ![[Note/Front-end developer interview questions/attachments/Untitled.png|Untitled.png]]
    
4. Defer an element’s event handler if it depends on an external script that takes some time to load?
    
    In order to **defer** the event handler of an element if it depends on an ==external script== that takes some time to load. We can use the `**defer**` attribute inside the script tag while adding the external **JavaScript** file. The `**defer**` attribute confirms that the script will be executed ==after the== ==**HTML**== ==gets parsed==
    
    ```HTML
    <script src='external-script-file.js' defer></script>
    ```
    
    Now, we need to attach the event listener to the element dynamically. In order to ==wait for the external script file load==, we can attach the ==**load**== or the ==**DOMContentLoaded**== events before executing the script and once the loading is completed
    
    ```JavaScript
    document.addEventListener('DOMContentLoaded', () => {
    	app()
    })
    ```
    
5. Difference between `null` and `undefined` in **JS**
    
    |`undefined`|`null`|
    |---|---|
    |It’s a the default value that is assigned to a variable which is declared but not initialized|It can be assigned to a variable to make it an empty value|
    |It’s also a default return value of a function|It represent that the accessing variable is not present in the code.|
    |When we try to access some value that is not in a part of an object, it’ll return `undefined`||
    
6. What are different ==Data types== in **JS**?
    - Primitive types: `**string**`**,** `**number**`**,** `**boolean**`**,** `**undefined**`**,** `**null**`**,** `**BigInt**` etc
    - Non-Primitive types: `array` , `object`
7. Explain `**call()**` `**apply()**` and `**bind()**` methods in **JavaScript**
    - `**call()**`**:** used to call the functions with a specified `**this**` identifier value and individual multiple arguments
        
        ```JavaScript
        let myObj = {
        	implementCall: function(name, desc) {
        		this.name = name;
        		this.decs = decs;
        		console.log("implemented");
        	}
        }
        
        let func = myObj.implementCall;
        func.call(this, "Liem", "male"); // `this` of `func` variable
        ```
        
    - `apply()`: almost same as `call()` but it allows you to pass multiple arguments together to the function in the form of an array
        
        ```JavaScript
        func.apply(this, ["Liem", "male"]);
        ```
        
    - `bind()`: The `call()` and `apply()` methods invokes the function immediately after the application, but the `bind()` is used to bind a function to some variable with the passed parameters and the scope of `**this**` identifier, so that the function can ==be called later== when we need to call it.
        
        ```JavaScript
        let func = myObj.implementCall.bind(myObj, "Liem", "male");
        
        func();
        ```
        
8. What is “use strict” in **JavaScript**?
    
    The **use strict** directive is used to write the ==clean== **JavaScript** code which is ==less prone to errors==. It catches common coding errors like assigning a variable without declaring it or passing different parameters with same names to a function etc.
    
9. What is ==event propagation== in **JavaScript**?
    
    Event propagation defines the behavior how the events will propagate when they are attached with the child and the parent elements. There are two ways in which events can propagate.
    
    - **Event Bubbling**
    - **Event Capturing**
10. Describe the concept of **CORS**?
    
    **CORS** stands for ==**Cross-Origin Resource Sharing**==. It is a technique ==used by the browsers== to make our web page more secure. The web browsers use this feature to ==prevent requests== from one domain to another domain.