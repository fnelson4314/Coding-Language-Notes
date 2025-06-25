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


