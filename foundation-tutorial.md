# Foundation Walkthrough Practice

## Getting Started  

```no-highlight
et get foundation-tutorial
cd foundation-tutorial
bundle
```

We're going to practice using the Foundation framework by implementing a design from a wireframe. As a developer, you'll often get or make wireframes that sketch out the approximate look of a web page, like [this one](https://s3.amazonaws.com/horizon-production/images/qBALeUA.png). (This wireframe was created using [Balsamiq](https://balsamiq.com/).)

In this tutorial, you'll use the files provided to walk through the process of creating a website that looks like this:

- [Normal view](https://s3.amazonaws.com/horizon-production/images/qBALeUA.png)
- [Mobile view](https://s3.amazonaws.com/horizon-production/images/J2WzwVP.png)

Once you have downloaded the exercise, do note that we are using a `layout.erb` file, as well as `index.erb`. Anything that we want to show up on *every* page - such as the top navigation bar - should be put in `layout.erb`, and page-specific content, for now, should be put in `index.erb`.

### 1. Include Foundation

There are several different ways to get Foundation working in your project.

For this example, we are going to use CDN links as a way to access the styling framework that Foundation provides. A CDN (content distribution network) is essentially a network of servers with the purpose of delivering some content. _Due to the fact that CDN links require requests to an external server for information, your Foundation CSS will not work if you are offline or without internet._

Visit the [CDN Links](https://get.foundation/sites/docs/installation.html#cdn-links) found in the Installation section of the Foundation Website. Currently, our `layout.erb` file links and imports our custom `style.css`. Add the `<link>` tag from the Foundation CDN right above this, so that any styling we do in `style.css` overwrites Foundation.

```html
...
  <!-- stylesheets -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/foundation-sites@6.4.3/dist/css/foundation.min.css" integrity="sha256-GSio8qamaXapM8Fq9JYdGNTvk/dgs+cMLgPeevOYEx0= sha384-wAweiGTn38CY2DSwAaEffed6iMeflc0FMiuptanbN4J+ib+342gKGpvYRWubPd/+ sha512-QHEb6jOC8SaGTmYmGU19u2FhIfeG+t/hSacIWPpDzOp5yygnthL3JwnilM7LM1dOAbJv62R+/FICfsrKUqv4Gg==" crossorigin="anonymous">
  <link rel="stylesheet" href="public/stylesheets/style.css">
</head>
...
```

Because some of the features of Foundation require both CSS and JavaScript, such as dropdown menus, we need the CDN links for both! Add the `<script>` below the script tag for jQuery (which is dependency that Foundation relies on).

```html
...
  <!-- javascript -->
  <script src="https://code.jquery.com/jquery-3.4.1.min.js" integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
  
</body>
...
```

Since we added Foundation for JavaScript, we need to initialize the Foundation scripts. The `.foundation()` function will import Foundation after our page has loaded the HTML. After the Foundation script we included, we can add:

```html
  ...
  <script>
    $(document).foundation();
  </script>
</body>
```

### 2. Make the Top Bar

When making a **Top Bar**, we can start by copy-and-pasting from Foundation's docs. Visit [https://get.foundation/sites/docs/](https://get.foundation/sites/docs/) and click "Navigation" along the side bar to view the relevant documentation.

The navbar shown under the **Top Bar** section looks pretty similar to what we're going for:

![Top Bar Example](https://s3.amazonaws.com/horizon-production/images/9Ohf675.png)

To use it, let's click on the "Top Bar" link along the left side of the Foundation page, and then copy and paste the provided code example, then edit it to suit our needs. Copy that code and paste it in `layout.erb`, right inside the opening `body` tag (and above the line that says `<%= yield %>`).

Run the server (`ruby server.rb`) and navigate to <http://localhost:4567/> to see Foundation in action in your app! We're going to modify this to look more like our wireframe.

Now let's edit that code, piece by piece:

```html
<body>
  <div class="top-bar">
    <div class="top-bar-left">
      <ul class="dropdown menu" data-dropdown-menu>
        <li class="menu-text">Site Title</li>

        <!-- ... -->
```

The above section sets the title of the site. First of all, let's change "Site Title" to the actual title of our site. Pick anything you want!

If we look at this first chunk of code in a larger context:

```html
<div class="top-bar">
  <div class="top-bar-left">
    <ul class="dropdown menu" data-dropdown-menu>
      <li class="menu-text">Foundation Funtimes</li>
      <li>
        <a href="#">One</a>
        <ul class="menu vertical">
          <li><a href="#">One</a></li>
          <li><a href="#">Two</a></li>
          <li><a href="#">Three</a></li>
        </ul>
      </li>
      <li><a href="#">Two</a></li>
      <li><a href="#">Three</a></li>
    </ul>
  </div>

  <!-- ... -->

</div>
```

This code inside `"top-bar-left"` creates all the links on the left hand side of our top bar, and there's a bunch of stuff there we don't need. First, there are several more links shown here than we have in our designs. Second, Foundation has provided us with code for a **Dropdown Menu**, which is not in our designs.

Let's get rid of that extra code! We can delete the class of "dropdown" from the `ul`, along with the attribute "data-dropdown-menu." Make sure you keep the "menu" class. After the `li` for our "menu-text", we only need one other `li` for a link to our "About" page.

Also, because — according to our design -- we don't need a vertical menu in our top-bar, delete the `ul` that has a class of "menu vertical" (and its contents).

Next up:

```html
<div class="top-bar">

  <!-- ... -->

  <div class="top-bar-right">
    <ul class="menu">
      <li><input type="search" placeholder="Search"></li>
      <li><button type="button" class="button">Search</button></li>
    </ul>
  </div>
</div>
```

This section of code sets up the contents of the right side of the top bar. Right now, it's showing a search form, which we don't want. Let's change the contents of the two `li`s so that instead of showing an `input` and `button`, they each contain an `a` (anchor) tag and the text shown in the wireframe design.

Our final navbar HTML should look like this in `layout.erb`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Foundation Funtimes</title>

    <!-- stylesheets -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/foundation-sites@6.4.3/dist/css/foundation.min.css" integrity="sha256-GSio8qamaXapM8Fq9JYdGNTvk/dgs+cMLgPeevOYEx0= sha384-wAweiGTn38CY2DSwAaEffed6iMeflc0FMiuptanbN4J+ib+342gKGpvYRWubPd/+ sha512-QHEb6jOC8SaGTmYmGU19u2FhIfeG+t/hSacIWPpDzOp5yygnthL3JwnilM7LM1dOAbJv62R+/FICfsrKUqv4Gg==" crossorigin="anonymous">
    <link rel="stylesheet" href="public/stylesheets/style.css">
  </head>
  <body>

    <!-- navigation -->
    <div class="top-bar">
      <div class="top-bar-left">
        <ul class="menu">
          <li class="menu-text">My Website</li>
          <li><a href="#">About</a></li>
        </ul>
      </div>

      <div class="top-bar-right">
        <ul class="menu">
          <li><a href="#">Sign up</a></li>
          <li><a href="#">Sign In</a></li>
        </ul>
      </div>
    </div>

    <!-- main content -->
    <%= yield %>

    <!-- javascript -->
    <script src="https://code.jquery.com/jquery-3.4.1.min.js" integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/foundation-sites@6.4.3/dist/js/foundation.min.js" integrity="sha256-mRYlCu5EG+ouD07WxLF8v4ZAZYCA6WrmdIXyn1Bv9Vk= sha384-KzKofw4qqetd3kvuQ5AdapWPqV1ZI+CnfyfEwZQgPk8poOLWaabfgJOfmW7uI+AV sha512-0gHfaMkY+Do568TgjJC2iMAV0dQlY4NqbeZ4pr9lVUTXQzKu8qceyd6wg/3Uql9qA2+3X5NHv3IMb05wb387rA==" crossorigin="anonymous"></script>
    <script>
      $(document).foundation();
    </script>

  </body>
</html>

```

### 3. Adding the Breadcrumbs

![Wireframe Breadcrumbs](https://s3.amazonaws.com/horizon-production/images/tqgd95I.png)

Will you look at that, Foundation has a [section on breadcrumbs](https://get.foundation/sites/docs/breadcrumbs.html)! Good stuff. They don't look exactly like our wireframes, but wireframes are supposed to be approximate, so that's okay.

Let's grab the sample code that Foundation gives us for breadcrumbs, and customize it to look like we want it to! We should put this block in `index.erb`, rather than `layout.erb`, because we want the "current page" attribute to be updated based on what page we're viewing. Next, to customize it, replace the text with your own text and make sure that there aren't any classes like `"disabled"` on list items.

Load the page and check it out!

![Ugly Breadcrumbs](https://s3.amazonaws.com/horizon-production/images/foundation-tutorial-breadcome-screen-cap.png)

Oh no! The breadcrumbs are mushed up right against the edge of the page, instead of having nice gutters like shown in the wireframe.

### 4. Constrain the width of our page content using the XY Grid

Luckily Foundation's XY Grid allows us to customize the alignment of our elements. We can use the [grid-container](https://get.foundation/sites/docs/xy-grid.html#grid-container) class to define the layout of our breadcrumbs. This class defaults to the full width of the screen and adds some nice, equal padding on the left and right to center the container (not its' contents).

As we can see from our designs, we want *all* of the content on our page to have a limited width, and to have these gutters at the sides. Since this will presumably apply to *every* page, let's accomplish this by putting a `grid-container` in our `layout.erb` file. If we wrap the `grid-container` around our `yield` statement, it'll make sure that no contents in our `index.erb` file will extend beyond the desired width!

```html
<!-- main content -->
<div class="grid-container">
  <%= yield %>
</div>
```

Taking a look at our page now, we should see that on a large screen we have some gutters on the left and right, and on a smaller screen there is still some padding to keep our breadcrumbs - and all future content - from being pressed against the edge for any screen size.

### 5. Adding our header text

Let's add in our page headers. Below the breadcrumbs in your `index.erb` file, add an `h1` and an `h3` for the headers:

```html
<nav aria-label="You are here:" role="navigation">
  <ul class="breadcrumbs">
    <li><a href="#">Home</a></li>
    <li><a href="#">Product</a></li>
    <li><a href="#">Xyz</a></li>
    <li>
      <span class="show-for-sr">Current: </span> Features
    </li>
  </ul>
</nav>

<h1>Wow, what an awesome page!</h1>
<h3>Here are some reasons you should fill out our form:</h3>
```

But wait! If we look at our wireframe design, our text isn't centered! Luckily, Foundation has a handful of typography [helper classes](https://get.foundation/sites/docs/typography-helpers.html) to help center text alignment. Adding the helper class `text-center` to something will try to center the text-alignment of all its contents.

This means we *could* add the class `text-center` to both our `h1` and our `h3`, and that would work fine:

```html
<h1 class="text-center">Wow, what an awesome page!</h1>
<h3 class="text-center">Here are some reasons you should fill out our form:</h3>
```

Alternatively we could be a little more efficient, and add a parent `div` around both the `h1` and `h3` and put the class `text-center` on that. This will tell the div to center all its contents at once by having its children elements inherit that styling. Here's what that would look like:

```html
<div class="text-center">
  <h1>Wow, what an awesome page!</h1>
  <h3>Here are some reasons you should fill out our form:</h3>
</div>
```

### 6. Adding the colored boxes

Foundation has handy styles pre-defined for boxes of slightly different colors than their white background, called [callouts](https://get.foundation/sites/docs/callout.html). Looking at the documentation linked here, we can see that making a `div` with the class of `callout` will give it a border, and adding the class `secondary` will give it that nice darker background we're looking for. Let's try that with just one box after our headers:

```html
<div class="callout secondary">
  <h3>Reason #1</h3>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
  </p>
</div>
```

(We'll add the buttons in later.)

When we reload the page, we can see that this looks pretty good, except for one thing - the callout box is stretching all the way across the content area of our page, whereas we only want it to be taking up one third of that space (so we can fit the other two panels).

### 7. Dividing our container

The [Foundation XY Grid](https://get.foundation/sites/docs/xy-grid.html) system provides us with the ability to make our elements take up a set percentage of the width of the container where they reside. The Foundation Grid is divided into 12 columns, so if we want something to take up one third of its' container we would need to tell it to take *4 twelfths*. The other piece of information this class needs is the screen size at which we want this style to be applied. Foundation gives us the options `small`, `medium`, or `large`. If we use `small-4`, we're saying: "Hey Foundation! On a small screen **or larger**, this thing should take up 4/12 the width of its' container."

```html
<div class="callout secondary small-4">
  <h3>Reason #1</h3>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
  </p>
</div>
```

However, our panel is **still** taking up the full width! We should add a parent `div` that will hold all 3 panels with a class of `"grid-x"`. This defines a row along the x-axis within our `grid-container` for all three of our panels to live in. On the elements themselves, we can add the class `cell` to signal that this is an item within the `"grid-x"` row.

```html
<div class="grid-x">
  <div class="callout secondary cell small-4">
    <h3>Reason #1</h3>
    ...
```

So far, so good! Now let's copy and paste that chunk of code so that we end up with three identical panels.

When we reload the page, we can see this is looking...less good. Where is the nice space between our panels?

![](https://s3.amazonaws.com/horizon-production/images/foundation-tutorial-callouts.png)

Foundation callouts have padding that keeps their content from pressing up against their edges, but they don't have any left or right *margins* to keep them from being pressed against each other. As a solution, we can define left and right margins to be applied to each panel with the class `"grid-margin-x"` on the parent `div`. These margins are determined by a unit of measurement called `rem` (a particular type of distance measurement for web dev that is similar to pixels, but dynamic and relative based on device).

Now our `index.erb` file should look like this:

```html
<nav aria-label="You are here:" role="navigation">
  <ul class="breadcrumbs">
    <li><a href="#">Home</a></li>
    <li><a href="#">Product</a></li>
    <li><a href="#">Xyz</a></li>
    <li>
      <span class="show-for-sr">Current: </span> Features
    </li>
  </ul>
</nav>

<div class="text-center">
  <h1>Wow, what an awesome page!</h1>
  <h3>Here are some reasons you should fill out our form:</h3>
</div>

<div class="grid-x grid-margin-x">
  <div class="callout secondary cell small-4">
    <h3>Reason #1</h3>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </div>

  <div class="callout secondary cell small-4">
    <h3>Reason #2</h3>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </div>

  <div class="callout secondary cell small-4">
    <h3>Reason #3</h3>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </div>
</div>
```

Now within this space they will evenly arrange themselves! You can also test out what the layout looks like with a fourth panel - it should arrange itself on a new row!

Reload the page - much better!

### 8. Adding the button to the panel

Foundation has a nice section on how to make [pretty-looking buttons](https://get.foundation/sites/docs/button.html) - pretty much, the secret is to take a link and put the class `button` on it. So let's do that inside each of our panels:

```html
<div class="callout secondary cell small-4">
  <h3>Reason #1</h3>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
  </p>
  <!-- Button -->
  <a href="#" class="button">Learn More</a>
</div>
```

When we reload the page, we can see this is close to our desired look, but the buttons are left-aligned instead of centered.

To fix this, let's first try adding the class `text-center` to the link itself:

```html
  <a href="#" class="button text-center">Learn More</a>
```

When we reload the page, we can see that there isn't any change.

Let's "Inspect Element" on the button to get a closer look.

![](https://horizon-production.s3.amazonaws.com/images/foundation-inspect-button.png)

From this view, we can see that the button is about ~105px wide (~73px for the text content, and ~14px on each side for padding). What `text-center` does is say "For this element, I want to center the alignment of all the element's contents" - but that will only center it within the width of the element itself. For the button and its' text to appear centered in the panel, the button element would need to be the full width of the panel, if this is the approach we're taking.

Instead, let's take a different approach: let's take our button and wrap it in a `div` that has the class `text-center`.

```html
<div class="callout secondary cell small-4">
  <h3>Reason #1</h3>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
  </p>
  <!-- Button -->
  <div class="text-center">
    <a href="#" class="button">Learn More</a>
  </div>
</div>
```

Now, when we reload the page and "Inspect Element," we can see this:

![](https://horizon-production.s3.amazonaws.com/images/foundation-inspect-div-button.png)

By default, `div`s are full-width. Therefore, when we put the class `text-center` on a div, it stretches to take up the full width of its parent container, and *then* tries to center any text elements inside it. That means it successfully centers the button within our parent box.

Go ahead and add a centered button to both of the other panels on our page.

### 9. Making the panels look good on Mobile

We've set things up so that they're looking good on a large screen, but we also have those [mobile designs](https://s3.amazonaws.com/horizon-production/images/J2WzwVP.png) we need to follow. This wireframe is showing us that on small screens, we need the panels to be the full width of the page.

First we need to add a `meta` tag in the `<head>` of our `layout.erb` file.

```html
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ...
```

The `viewport` is the portion of webpage window where we can see content. The `width` property determines the size of this viewport, here we are specifying that the width should adjust to the `devise-width`, and the `initial-scale` refers to the initial zoom when visiting the page (`1.0` does not zoom, but `2.0` will zoom in).

Next, we need to modify the classes we have wrapped around our panels to specify that on small screens, each panel should be the full 12 columns wide, and on medium-to-large screens, each panel should be 4/12 columns wide:

```html
<div class="callout secondary cell small-12 medium-4">
  <h3>Reason #1</h3>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
  </p>

  <div class="text-center">
    <a href="#" class="button">Learn More</a>
  </div>
</div>
```

Add this to each of your panels, reload the page, and we should be looking good!

### 10. Adding the "Resources" section and form

From here, try to use the tools we've gone over above, along with the Foundation documentation, to complete the rest of the wireframe. Specifically check out Foundation's docs on [vertical menus](https://get.foundation/sites/docs/menu.html#vertical-menu) and [forms](https://get.foundation/sites/docs/forms.html). For the form section, make good use of Foundation's grid system.

Tip: you can add a class of `button` to style submit buttons as well, to get them looking good!

### BONUS: Add some bling with your own CSS!

Remember how we added the CDN link to the Foundation stylesheet file in our layout? Take note of the fact that it was added on the line *before* our link to the `style.css` file.

```html
<!-- stylesheets -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/foundation-sites@6.4.3/dist/css/foundation.min.css" integrity="sha256-GSio8qamaXapM8Fq9JYdGNTvk/dgs+cMLgPeevOYEx0= sha384-wAweiGTn38CY2DSwAaEffed6iMeflc0FMiuptanbN4J+ib+342gKGpvYRWubPd/+ sha512-QHEb6jOC8SaGTmYmGU19u2FhIfeG+t/hSacIWPpDzOp5yygnthL3JwnilM7LM1dOAbJv62R+/FICfsrKUqv4Gg==" crossorigin="anonymous">
<link rel="stylesheet" href="stylesheets/style.css">
```

The `style.css` file is where we can add our own custom css! Our `style.css` should be loaded *after* Foundation because we want our custom css to override, or take priority over the Foundation's css. This is just one of the reasons CSS is called *Cascading* Style Sheets. Once you've added css to `style.css`, it will override stylings for similar elements where applicable, and you can begin taking your design in your own unique direction!

Good luck!
