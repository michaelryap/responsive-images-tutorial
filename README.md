#Responsive Images Tutorial

##Introduction

Over time, device manufacturers like Apple offer displays with higher and higher resolutions.

In October of 2015, Apple announced all 27-inch iMacs will be sold with a [5K display](www.theverge.com/2015/10/13/9512503/apple-imac-update-27-inch-5k-price-release-date-specs).

![alt tag](docs/4K.png)

<sub>5K resolution refers to a pixel dimension of 5,120×2,880, equivalent to about 14.7 million pixels.</sub>

![alt tag](docs/hodinkee.jpg)

<sub>The maximim width of the sites like the one pictured above is 1,440 pixels. On a 4K display more than one thousand pixels occupy the space to the its right and left hand side. On a 5K display, almost two thousand pixels buffers each side.</sub>

Since [2010](http://alistapart.com/article/responsive-web-design), savvy developers like [The Great Discontent](http://thegreatdiscontent.com) have been building sites with fluid widths—whereby its grid, images, and text dynamically scale according to the width of the observing browser.

![alt tag](docs/discontent-hero.jpg)

<sub>Notice how the layout of The Great Discontent on a 4K display occupies the entire width of the observing browser.</sub>

![alt tag](docs/discontent-body.jpg)

<sub>The Great Discontent defines its container by the observing browser-width rather than a fixed-dimension.</sub>

##Fluid Width Images

Let’s practice responsive web design by creating a fluid-width layout of cabin pornography.

**Step 1**

Download the [ZIP file](https://github.com/michaelryap/responsive-images-tutorial/archive/master.zip) containing the images we’ll be using.

Inspect the files within the folder labeled "img".

**Step 2**

Fire up Sublime Text and create a new HTML file.

```
<!doctype html>

<html>

<head>
	<meta charset="utf-8" >
	<style></style>
</head>

<body></body>

</html>
```

**Step 3**

Add the images.

```
<img src="img/cabin-porn-1.jpg" />
<img src="img/cabin-porn-2.jpg" />
<img src="img/cabin-porn-3.jpg" />
<img src="img/cabin-porn-4.jpg" />
<img src="img/cabin-porn-5.jpg" />
<img src="img/cabin-porn-6.jpg" />
<img src="img/cabin-porn-7.jpg" />
<img src="img/cabin-porn-8.jpg" />
<img src="img/cabin-porn-9.jpg" />
<img src="img/cabin-porn-10.jpg" />
<img src="img/cabin-porn-11.jpg" />
<img src="img/cabin-porn-12.jpg" />
```

Let’s envision a scenario whereby we wish to dynamically scale the cabin images in columns of increasing number as the observing browser-width increases.

If you open the page we’ve created in your browser, the columns increase in number as the observing browser-width increases, but the images don't dynamically scale.

Let’s fix that.

**Step 4**

Add a paragraph to display messages to ourselves. (This will make sense in about 6 more lines of code.)

`<p>My width is </p>`

**Step 5**

Let’s establish our logic in psuedocode.

* When the browser-width is 0 to 480 pixels, dynamically scale the images within a single column
* When the browser-width is 480 to 960 pixels, dynamically scale the images within two columns
* When the browser-width is 960 to 1440 pixels, dynamically scale the images within three columns
* When the browser-width is 1440 pixels and above, dynamically scale the images within four columns

**Step 6**

Between the opening and closing `<style>` tags, add this block of code:

````
@media (min-width: 0px) and (max-width: 480px){
	p:after { content: "between 0 and 480px"; }
}
````

**Step 7**

Write the rules required to set the columns according to each set of browser-width conditions:

```
@media (min-width: 0px) and (max-width: 480px){
	/* Display a message describing the current browser width */
	p:after { content: "between 0 and 480px"; }
	/* Create a single-column layout */
	img { width: 100%; }
}
```

**The Finished Exercise**

```
<!doctype html>

<html>

	<head>

	<meta charset="utf-8" >

	<style>

		@media (min-width: 0px) and (max-width: 480px){
			/* Display a message describing the current browser width */
			p:after { content: "between 0 and 480px"; }
			/* Create a single-column layout */
			img { width: 100%; }
		}

		@media (min-width: 480px) and (max-width: 960px) {
			/* Display a message describing the current browser width */
			p:after { content: "between 480 and 960px"; }
			/* Create a 2-column layout */
			img { width: 49%; }
		}

		@media (min-width: 960px) and (max-width: 1440px) {
			/* Display a message describing the current browser width */
			p:after { content: "between 960 and 1440px"; }
			/* Create a 3-column layout */
			img { width: 33%; }
		}

		@media (min-width: 1440px) {
			/* Display a message describing the current browser width */
			p:after { content: "greater than 1440px"; }
			/* Create a four-column layout */
			img {
				width: 24%;
			}
		}

	</style>

	</head>

	<body>

		<p>My width is </p>

		<img src="img/cabin-porn-1.jpg" />
		<img src="img/cabin-porn-2.jpg" />
		<img src="img/cabin-porn-3.jpg" />
		<img src="img/cabin-porn-4.jpg" />
		<img src="img/cabin-porn-5.jpg" />
		<img src="img/cabin-porn-6.jpg" />
		<img src="img/cabin-porn-7.jpg" />
		<img src="img/cabin-porn-8.jpg" />
		<img src="img/cabin-porn-9.jpg" />
		<img src="img/cabin-porn-10.jpg" />
		<img src="img/cabin-porn-11.jpg" />
		<img src="img/cabin-porn-12.jpg" />

	</body>

</html>

```

##Art-directed Responsive Images

Media queries are a pain to write—they require lots of typing and indentation.

Luckily, the smart people of the [Responsive Issues Community Group (RICG)](https://www.w3.org/community/respimg/) have been working to modify the HTML5 specification to make our lives easier.

In short, they’ve introduced the `<picture>` element to allow us to easily specify which image is displayed according to a browser’s width.

**Step 1**

Create a new HTML file.

```
<!doctype html>

<html>

<head>

	<meta charset="utf-8" >

	<style></style>

</head>

<body>

</body>

</html>
```

**Step 2**

Add a simple style that displays all images to 100% the width of its container.

```
<style>
	img {
		width: 100%;
	}
</style>
```

**Step 3**

Add a new image and surround it with opening and closing `<picture>` tags

```
<picture>
	<img src="img/pluto.jpg"/>
</picture>
```

**Step 4**

Add rules to display alternative images depending on the observing browser’s width.

```
<source media="(min-width: 1440px)" srcset="img/pluto-cinemascope.jpg">
<source media="(min-width: 960px)" srcset="img/pluto-hd.jpg">
````

**The Finished Exercise**

```
<!doctype html>

<html>

<head>

	<meta charset="utf-8" >

	<style>
		img {
			width: 100%;
		}
	</style>

</head>

<body>

	<picture>
		<source media="(min-width: 1440px)" srcset="img/pluto-cinemascope.jpg">
		<source media="(min-width: 960px)" srcset="img/pluto-hd.jpg">
		<img src="img/pluto.jpg"/>
	</picture>

</body>

</html>

```
