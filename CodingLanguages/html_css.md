# HTML

### Basics to start

- \<!DOCTYPE html> is needed at the top of all code
- Then \<html lang="en-US"> is next
- Then comes \<head><\/head>
  - Can put lots of things in between both of these including headers and paragraphs
  - Should put \<title> for the tab title
  - If you want to style with css externally, add \<link rel="stylesheet" href="nameOfFile.css">
  - This will be the top part of the page
- Then comes \<body><\/body>
  - This will be the bulk of the page
  - Can contain the same things
- Comments are \<!-- Write your comment here -->

### Tags

- [\<p>](https://www.w3schools.com/tags/tag_p.asp) tag is for paragraphs
  - **\<p style="color:red;"> This is a red paragraph. \</p>**
  - Can also do **\<p title="I'm a tooltip"> This is a paragraph \<p>**
    - This is what shows up when hovering over the paragraph
  - Can use \<hr> by itself to break up text and create a horizontal line or horizontal rule
  - Can use \<br> by itself for a line break or just pressing "enter"
- [\<h1-h6>](https://www.w3schools.com/tags/tag_hn.asp) tag is for headers
  - **\<h1 style ="font-size:60px;"> Heading 1\<h1>**
  - The larger the number, the smaller the text
- [\<a>](https://www.w3schools.com/tags/tag_a.asp) tag defines a hyperlink 
  - **\<a href="website hyperlink"> Text that you want<\/a>**
  - Make sure to put quotes around hyperlink but not the text that you want seen
  - the target attribute specifies where to open the linked document
    - \_self - Default. Opens the document in the same window/tab as it was clicked
    - \_blank - Opens te document in a new window or tab
    - \_parent - Opens the doument in the parent frame
    - \_top - Opens the dosument in the full body of the window
  - You can also use an image as a link. Just put the \<img> tag in the \<a> tag
    - **\<a hre"default.asp">\<img src="smiley.gif">\</a>**
- [\<img>](https://www.w3schools.com/tags/tag_img.asp) tag is used to embed an image in an html page. This is considered a self-closing tab since you don't need an ending tag
  - **\<img src="img_girl.jpg" alt="Girl with a jacket" width="500" height="600">**
  - Alt is what is used when an image doesn't load
- [\<pre>](https://www.w3schools.com/tags/tag_pre.asp) tag preserves all preformatted texts including spaces and line breaks
- [\<button>](https://www.w3schools.com/tags/tag_button.asp) tag creates a button that can be used for many purposes
  - **\<button>Sign up!\</button>**
- [\<input>](https://www.w3schools.com/tags/tag_input.asp) tag allows input that can take on many forms and types
  - **\<input type="text" placeholder="Enter username">**
- \<span> tag is an inline element instead of a block display element so that you can apply styling to certain bits of text instead of the whole element

### Classes/Ids

Once you get into styling, it is very important that you have some way to distinguish your different blocks of code.

- The "class" keyword can be used to assign a block of code to a certain class
  - **\<div class="main">
- ids are mainly used for styling elements that will be used once and once only as opposed to classes which are used multiple times.
  - **\<div id="underline">


 ### Formatting

- Put before and after the text you want to be formatted
- \<b> - bold text
- \<strong> - Important text
- \<i> - Italic text
- \<em> - Emphasized text
- \<mark> - Marked text
- \<small> - Smaller text
- \<del> - Deleted text
- \<ins> - Inserted text
- \<sub> - Subscript text
- \<sup> - Superscript text


# CSS

Start your CSS connection by adding **\<link rel="stylesheet" href="nameOfFile.css">** to the head tag of your html file

### Selectors

- With basic tags like body, paragraphs(\<p>), headers, etc., you only need to put the tag name
```css
body {
  color: red;
}
```

- With class tags, you need to add a period then the class name
```css
.main {
  margin-top: 300px;
}
```

 Pound signs are used instead of periods like with classes
```css
#underline {
  border-bottom: 4px solid white;
}
```
 

### Properties

- color: Text color
  - red, blue, yellow, etc.
  - Can also do hexcolor codes such as #8B4513 which is a recipe for how much red, green, and blue is in the color
- background: Background color
  - red, blue, yellow, etc.
  - You can also use the **linear-gradient()** function in order to fade from one color to another
  - **background: linear-gradient(red, blue);**
- background-image: Applies a background image to your page
  - **background-image: url("images/universe.jpg")**
- background-size: Specifies the size of the background image
  - cover: Resize the background image to cover the entire container, even if it has to stretch the image or cut a little bit off one of the edges
  - contain: Resize the background image to make sure the image is fully visible
  - auto: Displayed in its original size
  - Can also do length and percentages
- font-size: Determines the size of your font
  - 0px - 100px and beyond
- font-weight: Dictates the thickness of the font
  - lighter, normal, bold
- font-family: Allows you to change the font style of your text. This is normally done with multiple fonts called a font stack as backups in case your client doesn't have the first font installed
  - **font-family: Verdana, Geneva, Tahoma, sans-serif;**
  - There are two categories of fonts, serif and sans-serif. Serif has decorative strokes on the end of the letters and sans-serif does not
  - You can also do **font-family: inherit** which can be useful since buttons don't automatically inherit from their parents
- If you aren't getting fonts from google fonts but from somewhere else on the web, you can drag the font file into your project and use **@font-face**
```css
@font-face {
  src: url("Corlene.ttf");
  font-family: Corleone;
}
```
- text-align: positions your elements
  - left, center, or right
- text-shadow: Allows you to give a shadowy effect to your text
  - **text-shadow: horizontal-offset vertical-offset blur(optional) shadow-color**
- margins: Add space to the outside of your elements
  - This can be done using pixels, percentage, and auto (which auomatically centers your element when using display: block or eats up the space of the side you choose like margin-left)
  - You can use margin-top, margin-left, margin-bottom, margin-right, or just margin
  - margin with four values is in the form **margin: top right bottom left**
  - margin with three values is **margin: top left/right bottom**
  - margin with two values is **margin: top/bottom left/right**
  - margin with one value is all sides the same
- padding: Add space to the inside of your elements
- border: Allows you to specify certain properties of your element borders
  - **border: border-width border-style border-color**
  - **border: 6px solid red**
  - You can also do **border: none** to fully get rid of the border
- border-radius: Allows you to adjust the sharpness of your corners
  - **border-radius: 5px**
  - You can set it to 100% in order to get a circle
- width/height: Sets width or height
  - Done using pixels, percentages (so the size applies no matter the device or screen size), and auto
- display: Specifies the display behavior (the type of rendering box) of an element.
  - **inline** causes the elements to stack up beside each other in a horizontal line
  - **block** causes elements to stack on top of one another and each image blocks off space to the side of it
  - **flex** allows you to arrange the items as a flexbox
 
### Flexbox

- A flexbox consists of:
  - A flex container which is the parent (container) \<div> element
  - Flex items which are the items inside the container \<div>
- A flexbox only affects the direct children that are contained inside of it 
- Properties:
  - flex-direction: Specifies the display direction of flex items in a container
    - Can be row (default value), column, row-reverse (displays right to left), or column-reverse (displays bottom to top)
  - flex-wrap: Specifies whether the flex items should wrap or not, if there is not enough room for them on one flex line
    - Can be nowrap, wrap, wrap-reverse
  - flex-flow: shorthand property for flex-direction and flex-wrap
    - **flex-flow: flex-direction flex-wrap**
  - justify-content: Used to align the flex items when the do not use all available space on the main-axis (horizontally). This flips when you change the flex-direction
    - Can be center, flex-start (left), flex-end (right), space-around (space on all sides of items), space-between (no space to the outsides), space-evenly
  - align-items: Used to align flex items when they do not use all available space on the cross-axis (vertically)
    - Can be center, flex-start (top), flex-end (bottom), stretch (stretches items so they fill to the bottom), baseline, normal
  - align-content: Like align-items, but instead of aligning flex items, it aligns the flex lines
    - Can be center, stretch (default), flex-start, flex-end, space-around, space-between, space-evenly

### Pseudo-classes

A pseudo-class is used to define a special state of an element.

For example, it can be used to:
- Style an element when a user moves the mouse over it
- Style visited and unvisited links differently
- Style an element when it gets focus
- Style valid/invalid/required/optional form elements

- :hover- Allows you to change certain properties when an element is hovered over
```css
div:hover {
  background: blue;
}
