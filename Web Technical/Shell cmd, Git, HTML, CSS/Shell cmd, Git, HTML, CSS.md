---
Created: 2023-06-07T10:37
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://docs.google.com/document/d/1HcCIh2Pm4LRm1sinyAnonKkYGj5ZLdMNJM3aSn7ZCcM/edit#
Reviewed: true
Edited: 2025-05-10T14:45
---
# Git

Setup SSH key at company’s computer

- **Git init**
- **Git add, git commit**
- **Git merge, git rebase**
- **Git push, git pull**

- **Git stash**
    
    Is a command used to temporarily save changes that are not ready for implementation. This allows the developer to switch to another branch or work on another feature without having to make incomplete changes to the current branch.
    
    **Notice:** when pop stash it will be in unstage state
    
    - Push: create new stash
    - List
    - Pop: remove from list and apply into working tree status
    - Drop: remove from list
    - Apply: like Pop but not remove from list
    - Clear: remove all stash in list
- **Git reset**
    
    Delete a specific commit and go back to the previous commit.
    
    **Notice**: when reset commit locally, the log of local and remote is different, so you need to **push —force**
    
    - git reset —hard <commit id> : delete all changes of the commit
    - git reset —soft <commit id>: like an undo commit command, delete commit but still keep the changes, status=stage
    - git reset —mixed <commit id>: keep the changes, status=unstage
- **Git revert**
    
    Make a copy of the previous commit
    
    **Notice:** revert commit, the newly created commit will have the contents of the previous commit
    
    - git revert <commit id>

## HTML

- Structure
    - <head>
        - <title>
    - <body>
- Text…
    
    - <b> bold
    - <i> italic
    - <sup> superscript
    - <sub> subscript
    - <br /> line break
    - <hr /> break between themes
    - SEMANTIC MARKUP
    
    ==There are some text elements that are not intended to affect the structure of your web pages, but they do add extra information to the pages — they are known as semantic markup==
    
    - <strong> for content that has strong importance
    - <em> indicates emphasis that subtly changes the meaning of a sentence
    - <blockquote> longer quotes that take up an entire paragraph
    - <abbr> If you use an abbreviation or an acronym, then the element can be used. A title attribute on the opening tag is used to specify the full term
    - <cite>
    - <address>
    - <ins>
    - <del>
    
- List
    - <ol> order list
    - <ul> unorder
    - <dl> definition list
        - <dt>
            - <dd>

- Link <a href=”>
- Image <img src=’’ alt=’’ title=’’ height width>

- Table
    - <table>
        - <thead>
        - <tbody>
        - <tfoot>
            - <tr>
                - <th>
                - <td>
- Form
    
    - <label>
    - <input type=text, password, textarea, submit …>
    - <select>
        - <option>
    - <fieldset>
        - <legend>
    
    ```HTML
    <html>
    <head>
     <title>Forms</title>
    </head>
    <body>
     <form action="http://www.example.com/review.php" method="get">
     <fieldset>
     <legend>
     Your Details:
     </legend>
     <label>
     Name:
     <input type="text" name="name" size="30" maxlength="100">
     </label>
     <br />
     <label>
     Email:
     <input type="email" name="email" size="30" maxlength="100">
     </label>
     <br />
     </fieldset>
     <br />
     <fieldset>
     <legend>
     Your Review:
     </legend>
     <p>
     <label for="hear-about">
     How did you hear about us?
     </label>
     <select name="referrer" id="hear-about">
     <option value="google">Google</option>
     <option value="friend">Friend</option>
     <option value="advert">Advert</option>
     <option value="other">Other</option>
     </select>
     </p>
     <p>
    FORMS 172
    3F/;>:3
    4=@;A
     Would you visit again?
     <br />
     <label>
     <input type="radio" name="rating" value="yes" />
     Yes
     </label>
     <label>
     <input type="radio" name="rating" value="no" />
     No
     </label>
     <label>
     <input type="radio" name="rating" value="maybe" />
     Maybe
     </label>
     </p>
     <p>
     <label for="comments">
     Comments:
     </label>
     <br />
     <textarea rows="4" cols="40" id="comments">
     </textarea>
     </p>
     <label>
     <input type="checkbox" name="subscribe" checked="checked" />
     Sign me up for email updates
     </label>
     <br />
     <input type="submit" value="Submit review" />
     </fieldset>
     </form>
    </body>
    </html>
    ```
    
- Extra markup
    
    - Global attributes
        - id
        - class
    - Block elements:
        - <h1>, <p>, <ul>, <li>.
    - Inline elements
        - <span>, <a>, <b>, <em>, <i>, <img>
    - <div>: group texts & elements in a block
    - <span>: an inline version of <div>
    - <iframe>
    - <meta>: lives inside the <head> element and  
        contains information about that web page. It is not visible to users but fulfills a number of purposes such as telling search engines about your page, who created it, and whether or not it is time sensitive. (If the page is time sensitive, it can be set to expire.)  
        
    
    ```HTML
    <!DOCTYPE html PUBLIC
    "-//W3C//DTD HTML 4.01 Transitional//EN"
    "http://www.w3.org/TR/html4/loose.dtd">
    <html> 
    <head>
    	 <meta name="description" content="Telephone, email 
    	 and directions for The Art Bookshop, London, UK" /> 
    	 <title>Contact The Art Bookshop, London UK</title> 
    </head> 
    	<body> 
    	 <div id="header"> 
    		 <h1>The Art Book Shop</h1> 
    		 <ul> 
    			<li><a href="index.html">home</a></li> 
    			<li><a href="index.html">new publications</a>
    			</li> 
    			<li class="current-page">
    				<a href="index.html">contact</a>
    			</li> 
    		 </ul> 
    	 </div><!-- end header --> 
    	 <div id="content"> 
    		 <p>Charing Cross Road, London, WC2, UK</p> 
    		 <p><span class="contact">Telephone</span> 
    		 0207 946 0946</p>
    		 <p><span class="contact">Email</span> 
    			 <a href="mailto:books@example.com">
    		 books@example.com</a></p>
    		 <iframe width="425" height="275" frameborder="0" 
    			 scrolling="no" marginheight="0" marginwidth="0" 
    			 src="http://maps.google.co.uk/maps?f=q&amp;
    			 source=s_q&amp;hl=en&amp;geocode=&amp;
    			 q=charing+cross+road+london&amp;output=embed">
    		 </iframe> 
    		</div><!-- end content --> 
    		 <p>&copy; The Art Bookshop</p> 
    	</body> 
    </html>
    ```
    
- Flash, Video & Audio
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled.png|Untitled.png]]
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled 1.png|Untitled 1.png]]
    

  

# CSS

> The key to understanding how CSS works is to  
> imagine that there is an invisible box around  
> every HTML element.  

### USING EXTERNAL CSS

```HTML
<head>
	<link href="css/styles.css" type="text/css" rel="stylesheet" />
</head>
```

### USING INTERNAL CSS (shouldn’t use)

```HTML
<head>
	 <title>Using Internal CSS</title>
	 <style type="text/css">
		 body {
			 font-family: arial;
			 background-color: rgb(185,179,175);}
		 h1 {
			 color: rgb(255,255,255);}
	 </style>
</head>
```

### **INLINE CSS**

```HTML
<body>
	<h1 style="color:blue;text-align:center;">This is a heading</h1>
	<p style="color:red;">This is a paragraph.</p>
</body>
```

- Color (R,G,B,Opacity)
    - Background-color
    - Text
        - font-family
        - font-size
        - @font-face: allows to use font even if it isn’t installed
        - font-weight
        - font-style
        - text-transform
        - text-decoration
        - line-height
        - letter-spcaing, word-spacing
        - text-align: căn chỉnh
            - left, right, center
            - justify: every line in a paragraph, except the last, must be set to take up the full width of the container.
            - vertical-align: baseline, sub, super, top, text-top, middle, bottom, text-bottom
        - text-indent: indent the first line of text in an element
        - text-shadow
        - :first-letter :first-line
        - :link :visited
        - :hover :active :focus
- Boxes
    - width, height
    - min-width, max-width
    - min-height, max-height
    - overflow: tells the browser what to do if the content contained in a box is larger than the box itself.
        - hidden
        - scroll
    - border
        - border-width
        - border-style
        - border-color
        - shorthand ex: ==border: 3px dotted \#0088dd;==
    - padding: the space between the border of a box and any content contained within it
        - padding-top
        - padding-right
        - padding-left
        - padding-bottom
    - margin
        - margin-top
        - margin-right
        - margin-left
        - margin-bottom
    - CHANGE INLINE/BLOCK
        - display
    - visibility
    - box-shadow
    - border-radius
- LISTS
    - list-style-type
    - list-style-image
    - list-style-position
    - list-style (ex: ul { list-style: inside circle; })
- TABLES
    - empty-cells
    - border-spacing, border-collapse
- FORM
    
    - styling input
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled 2.png|Untitled 2.png]]
    
    - styling submit button
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled 3.png|Untitled 3.png]]
    
    - styling fieldset & legend
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled 4.png]]
    
    - aligning form
    
    ![[Web Technical/Shell cmd, Git, HTML, CSS/attachments/Untitled 5.png]]
    
    - cursor
- LAYOUT
    
    > _KEY CONCEPTS IN POSITIONING ELEMENTS IS ==BUILDING BLOCKS==, ==CONTAINING ELEMENTS== AND ==CONTROLLING THE POSITION OF ELEMENTS==_
    
    - NORMAL FLOW
        - position: static
        - position: relative _moves an element in relation to where it would have been in normal flow._
        - position: absolute _the box is taken out of normal flow and no longer affects the position of other elements on the page. (They act like it is not there.)_
        - position: fixed _It positions the element in relation to the browser window. Therefore, when a user scrolls down the page, it stays in the exact same place._
        - z-index _If you want to control which element sits on top, you can use the z-index property_
    
    - USING FLOAT TO PLACE ELEMENTS SIDE-BY-SIDE
        - float _use the float property, you should also use the width property to indicate how wide the floated element should be. If you do not, results can be inconsistent but the box is likely to take up the full width of the containing element (just like it would in normal flow)_
        - clear _The clear property allows you to say that no element (within the same containing element) should touch the left or right hand sides of a box._
    - PARENTS OF FLOATED ELEMENTS: PROBLEM
        - If a containing element only contains floated elements, some browsers will treat it as if it is zero pixels tall.
    - PARENTS OF FLOATED ELEMENTS: SOLUTION
        
        ![[Untitled 6.png]]
        
    - CREATING MULTI-COLUMN LAYOUTS WITH FLOATS
    - SCREEN SIZES
    - SCREEN RESOLUTION
    - PAGE SIZES
    - FIXED WIDTH LAYOUTS
    - LIQUID LAYOUTS
    - LAYOUT GRIDS: _Many designers use a grid structure to help them position items on a page, and the same is true for web designers_
    - CSS FRAMEWORK
    
      
    
- IMAGE
    - Controlling sizes
    - Aliging images
    - Centering images
    - background-image
    - background-repeat: repeat-x, repeat-y
    - background-attachment: fixed, scroll
    - background-position
    - SHORTHAND
        
        ![[Untitled 7.png]]
        
- HTML5 LAYOUT
    
    ![[Untitled 8.png]]
    
    - <header>
    - <footer>
    - <nav>
    - <article>
    - <aside>
    - <section>
        
        Example: Dividing a long article into distinct sections, such as ==introduction==, ==methods==, ==results==, and ==conclusion==
        
    - <hgroup>
    - <figure> <figcation>
- PROCESS & DESIGN
    - WHO IS THE SITE FOR?
    - WHY PEOPLE VISIT THIS WEBSITE?
    - WHAT YOUR VISITORS ARE TRYING TO ACHIEVE?
    - WHAT INFORMATION YOUR VISITORS NEED?
    - HOW OFTEN PEOPLE WILL VISIT YOUR SITE?
    - SITE MAPS
        
        ![[Untitled 9.png]]
        
    - WIREFRAME
        
        ![[Untitled 10.png]]
        
- PRACTICAL INFORMATION
    - Search engine optimization (SEO)
        
        The practice of trying to help your site appear nearer the top of search engine results when people look for the topics that your website covers. SEO is often split into two areas:
        
        - On-page techniques: _the methods you can use on your web pages to improve their rating in search engines,_ _**==keywords==**__, the text and HTML code for your site in order to help the search engines know that your site covers these topics_
            
            - Page title
            - Heading
            - Image alt text
            - Page descriptions
            
            - Determining which keywords to use on your site can be one of the hardest tasks
        - Off-page techniques: _Search engines help determine how to rank your site by looking at the number of other sites that link to yours._
            - Analytics: learning about visitors. tools for doing this is a free service offered by Google called Google Analytics

  

# OPEN QUESTION

  

1. Should we use tables in HTML? Why?
    
    It depends on the usage in web design. Firstly, tables in HTML are still useful elements displaying information in a structured grid-like format, organizing and presenting tabular data. However, it's important to note that tables should not be used for general page layout purposes because there are some modern CSS techniques more suitable and offer better responsiveness over the design such as flexbox or grid container.
    
      
    
2. What are the HTML tags have property display: inline, block, inline-block?
    
    - Inline tags: <span> <a> <b> <em> <i> <img> …
    - Block tags: <div> <h1 to 6> <ul> <ol> <li> <table> …
    - Inline-block tags: <input> <button> <textarea> <select> <fieldset> …
    
      
    
3. When will we use section, article tags?
    
    These tags help improve the semantics and accessibility of a webpage by providing clear structure, meaning to the content and assist search engines.
    
    - <section>: helps organize the content and provides a clear structure of a document.
        
        Example: Dividing a long article into distinct sections, such as ==introduction==, ==methods==, ==results==, and ==conclusion==
        
    - <article>: denotes a complete piece of content that could be a ==blog post==, ==news article==, ==forum post…==
    
      
    
4. How to use :before, :after CSS properties?
    
    These are pseudo-elements in CSS allow you to insert content before or after an element's actual content.
    
    - ::before: inserts content before the element
    - ::after: inserts content after the element
    
      
    
5. List all units in CSS.
    
    - Absolute units: px, cm, mm, in, pt, pc
    - Relative units: %, em, rem, ex …
    - Viewport-percentage: vw, vh, vmin, vmax
    
      
    
6. What are differences between position: absolute, relative, fixed?
    
    - relative: setting the top, right, bottom, and left properties of a relatively-positioned element
    - fixed: is positioned relative to the viewport and always stays in the same place even if the page is scrolled
    - absolute: position relative with its closest positioned ancesto or the initial cotaining block <body>
    
      
    
7. How to z-index property works?
    
    If boxes do overlap, the elements that appear later in the HTML code sit on top of those  
    that are earlier in the page. If you want to ==control which element sits on top==, you can use the z-index property.
    
      
    
8. How to add a google font to the CSS?
    
    ```HTML
    <head>
    	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Font+Name">
    </head>
    ```
    
      
    
9. What is the level of nesting CSS we should use? Why?
    
    There is no rules for the limit of nesting CSS but excessive nesting can make the CSS code more complex and harder to understand. Generally recommended to keep the level of nesting relatively low, typically within ==2 or 3 levels==
    
      
    
10. Should we use sprite-css? Why?
    
    ==Yes==, When a single image is used for several different parts of an interface. The advantage of using prites is that the web browser only needs to request one image rather than many images, which can ==make the web page load faster==. However, their usage should be considered on a case-by-case basis, evaluating the specific needs.
    
      
    
11. List HTML validation tool you know?
    - [W3C Markup Validation Service](https://validator.w3.org/)
    - [HTML5 Validator](https://html5.validator.nu/)

## Related

- [[Git begin]]
- [[JavaScript]]