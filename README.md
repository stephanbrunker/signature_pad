Signature Pad - Lightweight
===========================

Signature Pad is a JavaScript library for drawing smooth signatures. It's HTML5 canvas based and uses variable width Bézier curve interpolation based on [Smoother Signatures](http://corner.squareup.com/2012/07/smoother-signatures.html) post by [Square](https://squareup.com).
It works in all modern desktop and mobile browsers and doesn't depend on any external libraries.

This is a new fork based on [szimek/signature_pad](https://github.com/szimek/signature_pad) following these goals: 
* minimal footprint - only the `app.js` and `signature_pad.js` files and one CSS formatted element `signature-pad canvas` is needed
* also an absolutely minium example with just the basic elements
* rewritten drawing logic to make it similar to the [Android version](https://github.com/stephanbrunker/android-signaturepad), much more tidier source code and fixed some issues like drawing dots and the draw start sequence. 

![Example](https://user-images.githubusercontent.com/18150071/30086866-aaceae46-929d-11e7-936a-fb830d36bd9f.JPG)

## Demo
[Demo](http://stephanbrunker.github.io/signature_pad) works in desktop and mobile browsers. You can check out its [source code](https://github.com/stephanbrunker/js/signature_pad.js). 

For some tips on how to handle window resize and high DPI screens you can also find more about in [HTML5 Rocks tutorial](http://www.html5rocks.com/en/tutorials/canvas/hidpi) or the [base](https://github.com/szimek/signature_pad) of this fork. There you can also get a much more styled version using CSS and more info to use the library on runtime with JavaScript.

## Usage

### CSS,HTML & PHP
Copy the signature_pad.js and app.js files into the /js/ directory on your site

The signature is drawn on a canvas, this is the only element you need to format in width and height which gives you the size of the signature.
 
In the PHP/html form, you include that canvas inside a div with id *"signature-pad"* and an hidden input named *img-data* where the script dumps the image. And of course, you need to link to the script.

```php
<!-- Form for getting signature -->
<form ... >
	<div id='signature-pad' class='signature-pad'>
	  <canvas>This browser doesn't support the canvas for the signaturepad.</canvas>
	  <div class='signature-pad-footer' >
		  <button class="left" id="save" type="button" >Save</button>
		  <button class="right" id="clear" type="button" >Clear</button>
	  </div>
	</div>
<input type="hidden" name="img-data" id="img-data"> 
</form>
<noscript><p>This site needs JavaScript to work properly</p></noscript>
<script src="js/signature_pad.js"></script> 
<script src="js/app.js"></script> 

<!-- show the signature you got as POST -->
<?php 
$img_data = $_POST['img-data']; // contains the image as dataURL
?>
<p><img src='<?php echo $img_data;?>' height='150px' width='400px' alt='signature'></p> 
```

### Options
<dl>
<dt>minWidth</dt>
<dd>(float) Minimum width of a line. Defaults to <code>0.5</code>.</dd>
<dt>maxWidth</dt>
<dd>(float) Maximum width of a line. Defaults to <code>2.5</code>.</dd>
<dt>backgroundColor</dt>
<dd>(string) Color used to clear the background. Can be any color format accepted by <code>context.fillStyle</code>. Defaults to <code>"rgba(0,0,0,0)"</code> (transparent black). Use a non-transparent color e.g. <code>"rgb(255,255,255)"</code> (opaque white) if you'd like to save signatures as JPEG images.</dd>
<dt>penColor</dt>
<dd>(string) Color used to draw the lines. Can be any color format accepted by <code>context.fillStyle</code>. Defaults to <code>"black"</code>.</dd>
<dt>velocityFilterWeight</dt>
<dd>(float) Weight used to modify new velocity based on the previous velocity. Defaults to <code>0.7</code>.</dd>
</dl>

## License
Released under the [MIT License](http://www.opensource.org/licenses/MIT).
