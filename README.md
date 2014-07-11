Fergd's Mixins, Extends, & Helpers
====

My collection of Sass mixins, helpers, and snippets I tend to use in my projects. This is also a place I put snippets that I don't always use and don't always remember, but when I need them, I really need them. Some are original to me and some are influenced by other developers. Credit is listed where that is the case. 

Generally, What is What
----
  - Use mixins if the rule set requires variables to be passed in
  - Minimize code with extends if no variables are required

---
Layout Labels
---
I find this useful for testing layout. This applies helper labels to elements on your page. Default setting pulls the class name, but you can target any HTML attribute. 
example use only targeting the attr type and leaving the rest default: @include debug-labels($attr-type: attr(data-content));
```sh
@mixin debug-labels($attr-type: attr(class), $debug-font-size: 1em, $debug-color: black, $debug-bg-color: yellow){
	&:after{
		content: $attr-type;
		font-size: $debug-font-size;
		font-family: serif;
		color: $debug-color;
		padding: 0.25em;
		background-color: $debug-bg-color;
	}
}
```
Stop Shakira
---
Firefox image hover wiggle bug. Appropriate in the reset.
```sh
.stop-shakira{
	-moz-backface-visibility: hidden;
}
```
Easy Ellipsis
---
```sh
.ellipsis{
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
	-ms-text-overflow: ellipsis;
	-o-text-overflow: ellipsis;
}
```
HIDE ALL THE THINGS!!
---
Carefully executed conceling. Keep in mind accessibility requirements. Credit to h5bp.com where noted.
```sh
/* Hide only visually, but have it available for screenreaders: h5bp.com/v */
.is-visually-hidden { 
	border: 0; 
	clip: rect(0 0 0 0); 
	height: 1px; 
	margin: -1px; 
	overflow: hidden; 
	padding: 0; 
	position: absolute; 
	width: 1px; 
}

/* Extends the .visuallyhidden class to allow the element to be focusable when navigated to via the keyboard: h5bp.com/p */
.is-visually-hidden.focusable:active, 
.is-visually-hidden.focusable:focus { 
	clip: auto; 
	height: auto; 
	margin: 0; 
	overflow: visible; 
	position: static; 
	width: auto; 
}

/* Hide text only */
.hidden-text{
	text-indent: 100%;
	overflow: hidden;
	white-space: nowrap;
}

/* Hide completely, including from screen-readers */
.is-completely-hidden { display: none; }

```
Vertically Align Text
---
```sh
@mixin text-vert-align($line-height){
	display: inline-block;
	vertical-align: middle;
	line-height: $line-height;
}
```
Center Block Elements
---
```sh
@mixin centered-blocks($positioned-type: absolute, $left-value: 50%, $top-value: 50%, $horz-value: -50%, $vert-value: -50){
	position: $positioned-type;
	left: $left-value;
	top: $top-value;
	transform:translate($horz-value, $vert-value);
	-webkit-transform: translate($horz-value, $vert-value);
	-ms-transform: translate($horz-value, $vert-value);
}

.vertically-centered{
	@include centered-blocks($left-value: 0, $horz-value: 0);
}

.horizontally-centered{
	@include centered-blocks($top-value: 0, $vert-value: 0);
}
```
Hide Browser Imposed Spin Button
---
Hide the browser's addition of spinner controls on number fields. Ideally, this would be in the reset
```sh
input[type=number] { 
	-moz-appearance:textfield; 
}

input[type=number]::-webkit-outer-spin-button, 
input[type=number]::-webkit-inner-spin-button { 
	-webkit-appearance: none; 
	margin: 0; 
}
```