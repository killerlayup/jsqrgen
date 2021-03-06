JS QRGen
===

This is a QRCode generator written in pure javascript, without any dependencies. (jQuery is not needed, either.)

Based on [Kazuhiko Arase's QRCode](http://www.d-project.com/).

The only requirement is that the browser works with a `canvas`, which is supported by most modern browsers.

Usage
---
Here is a simple example:

``` html
<script type=text/javascript src=qrgen.min.js></script>
<div id=qrcode></div>
<script>
var qrc=new QRCanvas({
	data:location.href
});
qrc.appendTo(document.getElementById('qrcode'));
</script>
```

Check `test` folder for more advanced examples.

[中文说明](http://geraldl.net/js/qrgen) [测试页面](http://geraldl.net/js/qrgen-test)

Document
---

* *function* QRCanvas(*options*)  
  This is a constructor to build a QRCanvas object with a QRCode and a canvas built inside.
  * *options* is an object with or without the attributes below (all attributes are optional):
    * *data*  
      The **raw** data to be encoded in the QRCode, text should be encoded before calling.
    * *cellSize* \*  
      The pixel width or height of a cell.
    * *size* \*  
      The pixel width or height of the entire image, ignored if *cellSize* is assigned.
    * *typeNumber*  
      The type number of the QRCode, may be one of `1..10`. If less than `1`, the smallest valid type number will be found.
    * *correctLevel*  
      The correct level of QRCode, should be one of `['L','M','Q','H']`, default as `M`.  
      When *image* is assigned, *correctLevel* will be set to `H`.
    * *colorDark* \*\*  
      The background color of a cell when it is dark, default as `black`.
    * *colorLight* \*\*  
      The background color of a cell when it is not dark, default as `white`.
    * *image*  
      An object with attributes listed below (all optional):
      * *dom*  
        An `img` element with the image to be drawn in the middle of the canvas.
      * *clearEdges*  
        A boolean to decide whether to clear the cells broken by the image, default as `true`.
      * *margin*  
        The pixel gap between the image and the QRCode cells around it, default as `2`.
    * *effect*  
      An object with a *key* attribute to choose an effect, and *value* attribute as a parameter.  
      *key* can be `null` or one of the items below:
      * `round`  
        *value* is a ratio between 0 and 0.5, making cells round with a border-radius of *value* * `cellSize`.
      * `liquid`  
        *value* is a ratio between 0 and 0.5.

  \* Since *width* and *height* of a QRCode are always equal, we just need one of them, renaming to *size*.

  \*\* Both *colorDark* and *colorLight* can be a callable function, which will return a color,
     with `size_of_qrcode, row_id, column_id` as the arguments, so different colors may be used
     in different positions to make a characteristic QRCode.

  * **Methods**
    * *function* appendTo(*dom*)  
      Append the `canvas` to *dom*, works the same as `dom.appendChild(this.canvas)`.

Known Issues
---
Opera 12 (Presto) has problems with `canvas.arcTo`, so effects will probably fail.
