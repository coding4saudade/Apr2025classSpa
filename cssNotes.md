CSS Units

px, pixels (absolute):
used for base font size and really small things like border radii
em (relative):
relative to the font size of the parent element; used for font sizes
rem (relative):
relative to the font size of the root element; used for margins, widths, padding

NOTE: To set your "root" element font size, select the body element. it is not considered good practice to target the <HTML> element to set page defaults.

body {
  font-size: 10px;
  font-family: Georgia, serif;
}
...and set the font-size value. The font-family will set the base font for your website.


vh / vw, viewport height and viewport width (relative):
sizing relative to viewport/window; 1vh = 1% viewport height
% (relative):
sizing relative to parent element's property

Learn all about CSS values and units at (MDN)



Colors & CSS

There are many different ways to specify color in CSS. The three most common are with keywords or hexadecimal and rgb values.

We've already seen how CSS understands certain color keywords like purple or blue. For a list of all color keywords, visit the link above.
You may have seen color represented with a # in front of a value, like #c55da1. This is called a hexadecimal RGB value.
Each pair of values represents one of the color channels — red, green and blue — and allows us to specify any of the 256 available values for each.
These values are less easy to understand, but they are a lot more versatile than keywords — you can use hex values to represent any color you want to use in your color scheme.
Similar to hexadecimal, but reformatted to be easier to read is the rgb function. The rgb function - rgb() - takes three parameters that represent the red, green, and blue channel values of the colors.
Each of the 3 channels is represented by a decimal number between 0 and 255 - rgb(197, 93, 161)
There is a fourth parameter that represents the alpha channel of the color, which controls opacity (0 = fully transparent, 1 = solid/fully opaque). Values in between give you different levels of transparency.

Learn more about Applying color to HTML elements using CSS (MDN)



CSS and Background Images

To set a background image, use the url() function and pass in the path to the image, such as url(path-to-img.jpg) or url(https://img-link.net)

background-size: cover will cover the entire HTML container, potentially distorting or clipping the image when fitting it to whole the container
background-size: contain will cover as much of the HTML container as possible without clipping or distorting the background image

background-size: cover vs. contain


Learn more about CSS Backgrounds and borders (MDN)



CSS Variables

To make your site look cohesive its common practice to stick to a simple color palate of three or four colors. This often leads to multiple instances of those three/four colors in your css, This could lead to errors from mistyping or editing, and makes it difficult to switch to a different color scheme.

CSS variables or custom properties provide a solution to this problem. To set CSS variables/custom properties, select the root element using html or :root, and set up variables that can be reused throughout your project. Prefixing any custom property name you choose to use with "--" ...

:root {
  --primary-color: #845ec2;
  --secondary-color: #b39cd0;
  --text-primary-color: #fbeaff;
  --text-secondary-color: #00c9a7;
}
To access your custom properties, use the var() function and pass in the property name:

.blog-post {
  background-color: var(--primary-color);
  color: var(--text-primary-color);
}
Note In CSS we use var; this is not Javascript.


Learn more about using CSS custom properties / variables (MDN)



Stylesheet normalize.css

Default styles are different across browsers, meaning, the way each browser interprets and represents CSS varies. Apart from that browsers are usually filled to the brim with quirky (or bug-causing) behavior.

We want to have control over every aspect of our style across every browser.

So, we need to normalize or reset styles to make sure that every browser treats our elements the same.

To do this, we'll add normalize.css from CDNJS in the head of our HTML files, like so:

<!-- **IGNORE** THE WEIRD STYLING THAT VS CODE ADDS TO THIS CODE LINE. It can all be on one line -->

<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css"
/>


Google Fonts

Google Fonts is extremely helpful to virtually assure that your selected fonts will load on any computer/device.

Go to Google Fonts and select your fonts by clicking the "+" button. Each font you select is added to a tab at the bottom right of the screen (stick to two or three fonts maximum). Clicking the tab shows your font families and how to embed them.

Google Fonts constructs a custom HTML link with the font families you've selected, like this:

<link
  href="https://fonts.googleapis.com/css?family=Merriweather|Montserrat&display=swap"
  rel="stylesheet"
/>
Google Fonts also constructs the CSS rules to specify your font families in your stylesheet:

font-family: "Montserrat", sans-serif;
font-family: "Merriweather", serif;
If you intend to use different font weights or italicization, make sure to click the Customize tab and select the options you want. Google Fonts will add those options to the link it constructs - notice the numbers after Merriweather: below.

<link
  href="https://fonts.googleapis.com/css?family=Merriweather:400,900,900i|Montserrat&display=swap"
  rel="stylesheet"
/>


Collapsible Nav Bar --Hamburger-- element

Font Awesome
You will most likely want to introduce a responsive "hamburger" icon to stand in for your navigation links on smaller screens.

We will use Font Awesome Icons for our "hamburger"/bars icon.

The first step toward using Font Awesome icons is to link to the Font Awesome CSS in our HTML. Without this, we won't have access to the necessary Font Awesome classes:

<link
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css"
  rel="stylesheet"
/>

Adding the Nav Bar Hamburger Icon
Next, we can add a "hamburger" icon to our HTML by adding the following tag as a child of the <nav> element:

<i class="fas fa-bars"></i>
Note the line of code above has a unique tag <i></i>. This will select the correct icon from the Font Awesome Icon set. "fas" in this case is a unique Font Awesome class associated with the Font Awesome stylesheet linked above.

<nav>
  <i class="fas fa-bars"></i>
  <ul>
    <li>Home</li>
    <li>Contact</li>
    <li>GitHub</li>
    <li>MDN</li>
  </ul>
</nav>
Now we have the bars icon alongside our navigation links. However, we want either one or the other to appear based on screen size - not both at once.

Using media queries, we can specify at which screen size, the bars icon should be hidden, and visa-versa.

@media (min-width: 550px) {
  nav > .fa-bars {
    display: none;
  }
}
NOTE: to target the hamburger icon, we need to use our class .fa-bars to target it in the Nav Bar.

That solves our issue on bigger screens, but we still need to fix our mobile view.

On our mobile view, we will want to toggle the display of navigation links when the user clicks the bars icon.

In the HTML, lets add a class to the <ul> tag like hidden--mobile, like so...

<ul class="hidden--mobile nav-links"></ul>
In our CSS, create a media query that targets the smaller screen size and add a rule that targets that class:

/* in HTML: <ul class="hidden--mobile"> */
@media (max-width: 550px) {
  .hidden--mobile {
    display: none;
  }
}
Finally, to add our "toggle" functionality, we use JavaScript. We add an event listener to our "hamburger icon" that listens for a click. Inside the event listener's callback function, target the class list for the <ul> element inside the <nav> tag, and toggle the hidden--mobile class with the toggle() method.

document.querySelector(".fa-bars").addEventListener("click", () => {
  document.querySelector("nav > ul").classList.toggle("hidden--mobile");
});
Font Awesome Icons Cheatsheet



Jumbotron/Hero, & Border Radius

Hero
At the top of websites, it's common to see a large image with some text and possibly a button. This heading style is sometimes known as a "Jumbrotron" or "Hero" section.

To add a "Jumbotron", in your CSS, target your header and add a background-image with a background-size of cover and add a height that covers most of the screen using vh units (you may want to specify different heights based on screen size).

header {
  background-image: url(https://source.unsplash.com/random/800x600);
  background-size: cover;
  height: 100vh;
}
Border Radius
Since button elements are technically only supposed to be used to submit forms, for our "Hero" "button" we can use an <a> tag that we style to look like a button.

In our CSS, we target our <a> tag and add background-color, padding, and border-radius properties so that our <heading> <a> tag appears like a button.

header > a {
  text-decoration: none;
  background-color: white;
  font-size: 1.5em;
  padding: 1.5rem;
  border-radius: 10px;
}
Without border-radius, our button would have sharp, right angle corners. Adding a few pixels of border-radius rounds the corners of an HTML element's border edge. A border-radius of 50% creates a round button!

We could add a basic click action to our button to 'give' it something to do till we add a link, or a more advanced click action in our Javascript...

<a id="heroButton" href="" onClick="alert('Hello! You clicked the Button!')"
  >"Call to Action Button"</a
>
Once we have our <a> "button", all that is left is to center our text and "button" using Flexbox. Piece of cake!

