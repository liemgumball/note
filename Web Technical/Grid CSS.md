---
Created: 2023-06-22T09:28
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://web.dev/learn/css/grid/
Reviewed: true
Edited: 2025-05-10T14:45
---
# **Grid**

> _CSS Grid Layout provides a two dimensional layout system, controlling layout in rows and columns. In this module discover everything grid has to offer._

  

## Grid terminology

- Grid line
- Grid track
- Grid Cell
- Grid area
- Gaps
- Grid container
    
    ```CSS
    .container {
    	display: grid;
    }
    ```
    
- Grid Item
    
    ```HTML
    <div class="container">
      <div class="item"></div>
      <div class="item"></div>
      <div class="item"></div>
    </div>
    ```
    

  

## Rows and Columns

```CSS
.container {
    display: grid;
    grid-template-columns: 5em 100px 30%;
    grid-template-rows: 200px auto;
    gap: 10px;
}
```

- **Intrinsic sizing keywords**
    
    In addition to the length and percentage dimensions as described in the section on **==[sizing units](https://web.dev/learn/css/sizing)====,==** grid tracks can use intrinsic sizing keywords.
    
    - min-content
    - max-content
    - fix-content()
- The `fr` unit
- `minmax()` function
- `repeat()` function
- `auto-fill` and `auto-fit`

  

### Auto placement

- Placing items in columns
    - `auto-grid-flow:` `row` or `column`
    - `writing-mode:` `horizontal-tb` or `vertical-lr` or `vertical-rl`
- Filling gaps
    
    An auto-placed layout with some items spanning multiple tracks may result in a grid with some ==unfilled cells==. The default behavior of grid layout with a fully auto-placed layout is to always progress forward. If there is not enough space to fit an item, grid will ==leave a gap== and ==move to the next track==.
    
    `grid-auto-flow: dense`With this value in place, grid will take items later in the layout and use them to ==fill gaps.==
    

## Placing items

|Property|Description|
|---|---|
|column-gap|Specifies the gap between the columns|
|gap|A shorthand property for the row-gap and the column-gap properties|
|grid|A shorthand property for the grid-template-rows, grid-template-columns, grid-template-areas, grid-auto-rows, grid-auto-columns, and the grid-auto-flow properties|
|grid-area|Either specifies a name for the grid item, or this property is a shorthand property for the grid-row-start, grid-column-start, grid-row-end, and grid-column-end properties|
|grid-auto-columns|Specifies a default column size|
|grid-auto-flow|Specifies how auto-placed items are inserted in the grid|
|grid-auto-rows|Specifies a default row size|
|grid-column|A shorthand property for the grid-column-start and the grid-column-end properties|
|grid-column-end|Specifies where to end the grid item|
|grid-column-gap|Specifies the size of the gap between columns|
|grid-column-start|Specifies where to start the grid item|
|grid-gap|A shorthand property for the grid-row-gap and grid-column-gap properties|
|grid-row|A shorthand property for the grid-row-start and the grid-row-end properties|
|grid-row-end|Specifies where to end the grid item|
|grid-row-gap|Specifies the size of the gap between rows|
|grid-row-start|Specifies where to start the grid item|
|grid-template|A shorthand property for the grid-template-rows, grid-template-columns and grid-areas properties|
|grid-template-areas|Specifies how to display columns and rows, using named grid items|
|grid-template-columns|Specifies the size of the columns, and how many columns in a grid layout|
|grid-template-rows|Specifies the size of the rows in a grid layout|
|row-gap|Specifies the gap between the grid rows|

## Related

- [[Responsive web design]] - Using Grid for responsive layouts
- [[HTML-CSS training]] - CSS fundamentals