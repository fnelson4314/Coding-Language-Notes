# Bootstrap

## Getting Started

- Place **\<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.1.3/dist/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">** in your head section
- Can also add these for javascript which you will place right before closing the body tag


## Layout

- container:	Responsive centered content with horizontal padding
  - Can use container-fluid for a full width container, spanning the entire width of the viewport.
- card:	Card component with background, border, and rounded corners
- row: Starts a new row
  - align-items-(center, start, end): Vertically aligns all columns in the row
  - justify-content-(start, center, end, around, between): Horizontally align items in row
- col: Used to create columns
  - Sizing of columns can be done multiple ways:
    - A row can hold up to 12 columns but if there becomes more, the rest will flow over onto a new line
    - Can be done using **col-lg**. This can also be xs, sm, md, lg, or xl
    - You can also just put col by itself in a row to auto adjust the width.
      - Let's say one div of three had **col-6** while the others just had **col**. The other two would automatically have three boxes each
    - You can also do **col-4** to specify the exact amount of boxes out of 12 you'd like to use up
  - align-self-(start, center, end): Used to vertically align specified column in the row
  - offset-(size)-(n): Moves the column n boxes over to the right


## Utilities

For a list of all utilities, visit [https://getbootstrap.com/docs/4.1/utilities/borders/](https://getbootstrap.com/docs/4.1/utilities/borders/)
