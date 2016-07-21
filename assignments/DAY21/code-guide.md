#Code Guide by Yooncobra

##HTML

Sytax
> Use soft tab with two spaces.
Always use double quotes.

###HTML5 doctype at the beginnig of every HTML page.
<!DOCTYPE html>
<html>
  <head>
  </head>
</html>

###Language attribute
<html lang="en-us">
  <!-- ... -->
</html>

###IE compatibility mode
  <meta http-equiv="X-UA-Compatible" content="IE=Edge">

###Character encoding
  <head>
    <meta charset="UTF-8">
  </head>

###CSS and JavaScript includes
  <!-- External CSS -->
    <link rel="stylesheet" href="code-guide.css">

  <!-- In-document CSS -->
  <style>
    /* ... */
  </style>

  <!-- JavaScript -->
  <script src="code-guide.js"></script>

###Practically over purity
>Use the least amount of markup with the fewest possible.

###Attribute order
>The Class comes first, Id should be more specific name.

###Reducing markup
>Avoid superfluous parent elements.

  <!-- Not so great -->
  <span class="avatar">
    <img src="...">
  </span>

  <!-- Better -->
  <img class="avatar" src="...">



##CSS
Syntax
>1. When grouping selectors, keep individual selectors to a single line.
>2. Include one space before the opening brace of declaration blocks for legibility and after : for each declaration.
>3. Comma-separated property values should include a space after each comma.
>4. Don't include spaces after commas within rgb(), rgba(), hsl(), hsla, rect() values.
>5. Don't prefix property values or color parameters with a leading zero (e.g., .5 instead of 0.5 and -.5px instead of -0.5px).
>6. Lowercase all hex values, e.g., #fff
>7. Use shorthand hex values where available (#ffffff -> #fff).
>8. Avoid specifying units for zero values (margin: 0; instead of margin: 0px;).

  /* Bad CSS */
  .selector, .selector-secondary, .selector[type=text] {
    padding:15px;
    margin:0px 0px 15px;
    background-color:rgba(0, 0, 0, 0.5);
    box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
  }

  /* Good CSS */
  .selector,
  .selector-secondary,
  .selector[type="text"] {
    padding: 15px;
    margin-bottom: 15px;
    background-color: rgba(0,0,0,.5);
    box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
  }

###Declaration order
>Related property declarations should be grouped together following the order:
>
>1. positioning
>2. Box model
>3. Typographic
>4. Visual
>
>Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.
>Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.
  .declaration-order {
    /* Positioning */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;

    /* Box-model */
    display: block;
    float: right;
    width: 100px;
    height: 100px;

    /* Typography */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    text-align: center;

    /* Visual */
    background-color: #f5f5f5;
    border: 1px solid #e5e5e5;
    border-radius: 3px;

    /* Misc */
    opacity: 1;
  }

###Don't use @import
Compared to <link>, @import is slower.
Use multiple <link> elements.

  <!-- Use link elements -->
  <link rel="stylesheet" href="core.css">

  <!-- Avoid @imports -->
  <style>
    @import url("more.css");
  </style>

###Media query placement
Place media queries as close to their relevant eule sets whenever possible. Don't bundle them all in separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future.

  .element { ... }
  .element-avatar { ... }
  .element-selected { ... }

  @media (min-width: 480px) {
    .element { ...}
    .element-avatar { ... }
    .element-selected { ... }
  }

###Single declarations
In instances where a rule set includes only one declaration, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

The key factor here is error detection—e.g., a CSS validator stating you have a syntax error on Line 183. With a single declaration, there's no missing it. With multiple declarations, separate lines is a must for your sanity.

  /* Single declarations on one line */
  .span1 { width: 60px; }
  .span2 { width: 140px; }
  .span3 { width: 220px; }

  /* Multiple declarations, one per line */
  .sprite {
    display: inline-block;
    width: 16px;
    height: 15px;
    background-image: url(../img/sprite.png);
  }
  .icon           { background-position: 0 0; }
  .icon-home      { background-position: 0 -20px; }
  .icon-account   { background-position: 0 -40px; }


###Comments
Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.

  /* Bad example */
  /* Modal header */
  .modal-header {
    ...
  }

  /* Good example */
  /* Wrapping element for .modal-title and .modal-close */
  .modal-header {
    ...
  }

###Class names
* Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., .btn and .btn-danger).
* Avoid excessive and arbitrary shorthand notation. .btn is useful for button, but .s doesn't mean anything.
* Keep classes as short and succinct as possible.
* Use meaningful names; use structural or purposeful names over presentational.
* Prefix classes based on the closest parent or base class.
* Use .js-* classes to denote behavior (as opposed to style), but keep these classes out of your CSS.
* It's also useful to apply many of these same rules when creating Sass and Less variable names.

  /* Bad example */
  .t { ... }
  .red { ... }
  .header { ... }

  /* Good example */
  .tweet { ... }
  .important { ... }
  .tweet-header { ... }

### Selectors (이건 더 생각해 보고 나중에 정리가 필요한 부분)
* Use classes over generic element tag for optimum rendering performance.
* Avoid using several attribute selectors (e.g., [class^="..."]) on commonly occuring components. Browser performance is known to be impacted by these.
* Keep selectors short and strive to limit the number of elements in each selector to three.
* Scope classes to the closest parent only when necessary (e.g., when not using prefixed classes).

  /* Bad example */
  span { ... }
  .page-container #stream .stream-item .tweet .tweet-header .username { ... }
  .avatar { ... }

  /* Good example */
  .avatar { ... }
  .tweet-header .username { ... }
  .tweet .avatar { ... }

###Organization
* Organize sections of code by component.
* Develop a consistent commenting hierarchy.
* Use consistent white space to your advantage when separating sections of code for scanning larger documents.
* When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.

  /*
   * Component section heading
   */

  .element { ... }


  /*
   * Component section heading
   *
   * Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
   */

  .element { ... }

  /* Contextual sub-component or modifer */
  .element-heading { ... }

