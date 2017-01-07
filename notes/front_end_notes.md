### front end notes

* CSS selectors
    - a CSS selector defines which element the defined css properties apply to
    - basic selectors
        - element selector: the element type selector selects based on the html element such as `body`, `article`, `li`, etc
        - class selector: html elements can class applied to them with this syntax with multiple classes delimited by spaces
            - `<p class="bolded">paragraph text here</p>`
            - in the css this element can be selected with the class selector: `bolded { font-weight: bold; }`
        - id selector: html elements can also be assigned an id as follows:
            - `<p id="some-id">paragraph text here</p>`
            - element id's must be unique in the document
            - the hash symbol represents the id selector as in: `#some-id` { padding: 10px; } 
        - attribute selector: chooses nodes based on the value of an attribute assigned to the element
            - html: `<input type="button" value="hello">`
            - css: `input[type="button"]: height: 40px; width: 100px;`
        - universal selector - selects all elements
            - `* border: 1px solid black;`
    - selector combinators
        - adjacent sibling `+`: selects the element that immediately follows the specified element 
            - `div + p { }`: selects all `<p>` elements that immediately follow a `<div>`
        - general sibling `~`: selects all elements of a type that follow an element with in the same parent
            - not necessarily immediately after
            - `div ~ p { }`: select all `<p>` elements that follow a `<div>`, within the same parent
        - descendant: ` `: selects all elements that are child of the first element, not necessarily immediate children
            - `div p {}`: selects all of the `<p>` elements that are inside a div
        - direct child `>`: selects all of the elements that are directly a child of the first element
            - `div > p {}`: selects all `<p>` elements that are directly inside of a `<div>`
        - additional `,`: selects all of the elements in the comma delimited list
            - `div, p, a, .red { }`: properties are applied to all of the selectors
    - pseudo elements
        - pseudo elements are abstractions of the dom tree that provide elements beyond the scope of normal html
        - they allow a way to style these abstracted elements independently
        - syntax: `selector::pseudo-element { property: value }`
        - common pseudo element
            - after: matches an inline (by default) virtual last child of the selected element. often used to add content via css, such as text,
                  a background image or for the clear fix solution.
        - before: matches an inline (by default) virtual first child of the selected element. Often used to add cosmetic content to the element
                   such as a list-item graphic or an icon
        - first-letter: provides for a subset of properties for styling the first letter
        - first-line: provides for a limited subset of properties for styling the first line
        - selection: provides for a limited subset of properites to style user selected text. Such as the `background-color` and  `color`
    - pseudo classes
        - a pseudo class is added to an element and allows that element to be selected based on a certain state
        - common pseudo classes
            - checked: applies to checkbox, radio button and option input elements that can have an 'on' state. 
                   when the element is 'on' then css selector properties are applied to the element
            - first-child: selects the element that is the first child of its parent
            - first-of-type: selects the first element of its type in the list of child elements of the parent.
                - the universal selector is assumed when there is no simple selector as in: `div :first-of-type { }` 
                - first-of-type will select nested children as well
            - nth-child(an+b): 
                - matches an element that has an+b-1 siblings before it for a given positive value for n representing the position of the child in the series.
                - the selector matches a number of child elements whose numeric position in the series of children matches the pattern an+b
                - `an+b`: means match the element at position `b` and then every `a` elements after that
                - `3n+4`: match the 4th element, and then every third one after that
                - `p:nth-child(1n+0)` or `p:nth-child(n)`: match every child element
            - `p:nth-child(2n)`: match `<p>` elements 2, 4, 6, 8 etc
            - `p:nth-child(even)`: match `<p>` elements that are even in the series.  same as above.
            - `p:nth-child(odd)` or `p:nth-child(2n+1)`: match `<p>` elements that are odd in the series.
            - `p:nth-child(3n+4)`: match elements 4, 7, 10, 13, etc.
        - hover
            - allows styling of an element the user positions the mouse pointer over the element
            - can be overridden by other link related pseudo classes.
                - given this, make sure to call these properties in the proper order LVHA
                  :link, :visited, :hover, :active
            - :hover can be applied to :before and :after pseudo elements
        - last-child
            - selects the last child element of the parent
        - last-of-type
            - represents the last sibling of the given type in the list of children for the parent element
            - question: do nested children count toward this list?
        - link
            - selects any link that has not yet been visited
            - be mindful of other pseudo classes and the order in css = :link, :visited, :hover, :active
        - visited
            - selects any link that has been visited
            - be mindful of other pseudo classes and the order in css = :link, :visited, :hover, :active

* box model
    - html elements create a box on the page
    - a box has height and width and z-index (depth)
    - html documents display boxes on the page in order of appearance
    - boxes have width, height, content, padding, border and margin (from inside to out)
        - content is the elements that exist as child elements of the element in question
        - width and height encompass the area of the box and enclose its content
        - padding is inner margin.  It is the space between the margin and content
          padding can be set with padding shorthand: padding: 10px 11px 12px 14px;
          or by setting individual properties: padding-top, padding-bottom, padding-left, padding-right
        - border is distinct layer sitting between the margin and padding
            - border defaults to 0px in width
            - border can be set with a shorthands style as in border: 1px solid black;
            - individual borders can be set with, as example:
                - border-top-style, border-top-width, border-top-color
        - margin represents the space outside of the box.
            - margin will push against other elements in the document flow.
            - margins collapse: when two boxes touch, the distance is the largest of the margins, not the sum.
                - this applies to top and bottom margin only
                - occurs in three circumstances
                    - empty blocks: no border, padding or inline content to separate top and bottom margins
                    - adjacent siblings
                    - parent and first child/last child: if there is no border, padding or inline content to separate the parent and child margin

* style resets
    - different browsers have there own "user agent" style sheet that
      applies a set of standard styles to elements so that unstyled webpages have some basic styling
      to make the content more readable.
    - a css reset removes all of this styling so that design can start from unified base for all browsers

* floats
    - a floated box is positioned in the normal flow, then taken out of the flow and shifted to the right or left.
    - floated elements are taken out of the normal flow in relation to other block elements.
        - a <p> element is a block element and its borders will encompass a floated block since the floated
          block is invisible to other blocks
        - the text inside the <p> element however is inline and will flow around the floated element.
    - inline element content within the normal flow then flows around the floated element.
    - floated elements is shifted to the right or left on the current line.
    - width should always be set on a floated element to avoid unpredictable results.
    - floated elements without a width will fill the containing block horizontally
    - floated elements will behave better if they have a width set
    - if you float more than one element in the same container they will stack 
      up horizontally until they run out of horizontal space
    - floated elements move left or right until they touch the outer edge
      of the containing block or its padding, or the outer edge of another float.
    - surrouding inline content flows around the opposite side of a floated element
        - if the element is floated left, inline content flows to the right side
        - if the element is floated right, inline content flows to the left side.
    - collapsing and clearing
        - the container of a float collapses to 0 height, but when???
    - a float is not in the normal flow therefore:
        - non-positioned and non-floated blocks flow vertically as if the float
          didn't exist.
        - they will appear under the floated elements
    - Inline elements will wrap around the floated element.
    - floated inline elements are converted to block elements
    - to clear a float so that the wrapping does not occur:
        - apply the 'clear' property to the element following the floated element
        - apply `overflow: hidden;` and apply a width to the containing element
            - the disadvantage here is that positioned elements or content may be clipped
      - create an empty div following the cleared elements and apply 'clear: both'
      - create a pseudo after element that has the following:
          - content: " ";
          - clear: both;
          - although this is not the complete fix
            also helpful to generate the content for the before pseudo element as well
      - clear fix is really about float containment:
          - this is a technique for forcing a float-containing block level element
            to span the entire height its floated children.  To "contain" them!
      - the 'clear: both' property forces the element to render below any floats.

* positioning
    - position: relative allows you to move the element around visually, however it
      still occupies the same position in relationship to the normal document flow.
    - position: absolute removes the element from the document flow, and allows you to position 
      the element relative to the coordinate system of the nearest relatively positioned parent
    - position: fixed allows you to position the element relative to the viewport or screen.
      the user will always see this element
    - the position of an element can be modified with the top, bottom, left and right properties
        - top: 10px moves the element 10 pixels down from top edge of the element.
        - top: -10px moves the element 10 pixels up from top
        - bottom: 10px moves the element 10 pixels up from the bottom
        - bottom: -10px moves the element 10 pixels down from the bottom
        - left: 10px  10 px from the left
        - left: -10px to the left of left margin
    - z-index property allows you to set the stacking priority of an element relative to other elements in the same container.
        - css comes with a default stacking order
            - background and borders of root element
            - descendent blocks in the normal flow in order of appearance
            - floating blocks
            - inline descendants in the normal flow
            - descendant positioned elements in the order of appearance
        - to change the z-index, the element must be postioned.
        - the default z-index is 0
        - if any of the elements are positioned, then all of them should be positioned.  
        - otherwise z-index does not work as expect (the positioned element will be on top)
        - stacking context: stacking context can be created in a variety of ways
            - stacking context can be contained in another stacking context, creating a heirarchy
            - a context is completely independent of its siblings: only descendants are considered with processing stacking order.
            - a context is self contained. everything is stacked in the element and then the stacking order of element is considered
              as a whole in the stacking inside its parent
        - context is created in the following ways (although there are others)
            - the <html> element
            - a positioned element in z-index other than auto
            - element with opacity less than 1
            - position: fixed

* display properties such as block, inline, and inline-block
    - the display property defines how a element behaves in the document
    - every element has a default value for display, generally either inline or block
    - there are many properties. the most important are: none, inline, inline-block, block
        - `display: none;` will remove the element and all of its children from the document.
            - this is different from `visibility: hidden;` which simple hides the element while
              it still takes up space in the document
        - `display: block;` elements start a new line take up the entire width of their containing element
            - examples: div, main, p, form, article, section, header, footer, img
        - `display: inline;` the elements `<span>`, `<b>` and `<em>` as well as all text defaults to inline
            - inline elements are stacked left to right on a line until they 
              run out of room, then then wrap to the next line
            - inline elements cannot have top and bottom margin or padding
            - they can have left and right margin and padding
        - `display: inline-block;`
            - makes block elements flow left to right
            - allows setting vertical margin and padding on inline elements
            - `inline-block` adjacent siblings will have a space between them
            - this space can be eliminated by
                - placing a comment between them: `</li><!-- --><li>`
                - put the elements inline in the markup: `<li>foo</li><li>bar</li>`
                - adding a right margin of -4 px: `margin-right: -4px;`
                - applying `font-size: 0;` to the parent element and setting the font size for the child elements explicitly.
        - `inline-block` adjacent siblings are vertically aligned on the bottom.
          this can be fixed with `vertical-align: top;`

* shorthand properties
    - many properties provide for a shorthand version to set multiple properties in one line of code
        - have to be careful, as properties omitted from the shorthand will be set to the initial value
          this may have unexpected consequences
        - `inherit` can only be applied to a shorthand property, but only to the entire property
          not as a keyword for individual properties
        - most shorthand properties attempt to not require an order to the keywords and values
        - properties that set attributes to the sides or corners do require an order and allow for 1, 2, 3 or 4 different values
          the meaning of these values is described below
    - margin and padding are treated similarly:
        - all four sides (top, right, bottom left): `margin: 10px 15px 20px 0;`
        - top/bottom, left/right equal: `margin: 10px 15px;`
        - top/bottom separate, left/right equal: `margin: 10px 20px 15px;` 
        - top/bottom/left/right all equal: `margin: 10px;`
    - border
        - border has 3 properties: width, style (solid, dashed, dotted), color, side
        - `border-right-color: red;` `border-left-width: 10px;` etc.
        - shorthand: `border: 4px solid seagreen;`
        - the values can be in any order
        - shorthand: `border-style: dotted ridge dashed solid;`
    - border-radius
    - background
        - properties: `background-color`, `background-repeat`, `background-position`, `background-image`
    - font
        - the properties should be listed in a specific order
        - at a minimum you must provide `font-size` and `font-family`
        - `font: font-style font-variant font-weight font-size/line-height font-family;`
    - list-style

* sprites
    - sprites are sheets of images that are used on a webpage
    - they reduce the number of requests for assets from the server, improving site performance
    - apply `position: relative;` to the sprite sheet
    - then use the `top`, `right`, `bottom` and `left` properties to move the sprite sheet around

* media queries
    - media queries limit the scope of a style sheet by specifying the conditions that
      would activate the selectors in the style sheet
    - media queries provide a media type and then 0 or more expressions that check the state of a media feature
    - types include things like `screen` and `print`
    - media features are most typically expressions related to the width of the screen or page
    - can be added using the link tag as in: `<link rel="stylesheet" media="(max-width: 600px)"`
    - available expressions that are evaluated to determine if a style sheet applies
        - width
        - height
        - device-width
        - device-height
        - min-width
        - max-width
        - orientation: portrait, landscape    
