# HTML5-PHP

This is a **highly experimental** HTML5 Parser.

The need for an HTML5 parser in PHP is clear. This project initially
began with the seemingly abandoned `html5lib` project [original source](https://code.google.com/p/html5lib/source/checkout).
But after some initial refactoring work, we began a new parser.

- An HTML5 serializer [in progress; early alpha]
- Support for PHP namespace [done]
- Composer support [in progress]
- Event-based (SAX-like) parser [in progress]
- DOM tree builder [in progress]
- Interoperability with QueryPath [not started]

## Basic Usage

HTML5-PHP has a high-level API and a low-level API. 

Here is how you use the high-level `HTML5` library API:

```php
<?php
// Assuming you installed from Composer:
require "vendor/autoload.php";


// An example HTML document:
$html = <<< 'HERE'
  <html>
  <head>
    <title>TEST</title>
  </head>
  <body id='foo'>
    <h1>Hello World</h1>
    <p>This is a test of the HTML5 parser.</p>
  </body>
  </html>
HERE;

// Parse the document. $dom is a DOMDocument.
$dom = HTML5::parse($html);

// Render it as HTML5:
print HTML5::saveHTML($dom);

// Or save it to a file:
HTML5::save('out.html');

?>
```

The `$dom` created by the parser is a full `DOMDocument` object. And the
`save()` and `saveHTML()` methods will take any DOMDocument.


### The Low-Level API

This library provides the following low-level APIs that you can use to
create more customized HTML5 tools:

- An `InputStream` abstraction that can work with different kinds of
input source (not just files and strings).
- A SAX-like event-based parser that you can hook into for special kinds
of parsing.
- A flexible error-reporting mechanism that can be tuned to document
syntax checking.
- A DOM implementation that uses PHP's built-in DOM library.

The unit tests exercise each piece of the API, and every public function
is well-documented.

## Notes on Serialized Formats

The serializer (`save()`, `saveHTML()`) follows the 
[section 8.9 of the HTML 5.0 spec] (http://www.w3.org/TR/2012/CR-html5-20121217/syntax.html#serializing-html-fragments).
So tags are serialized according to these rules:

- A tag with children: &lt;foo&gt;CHILDREN&lt;/foo&gt;
- A tag that cannot have content: &lt;foo&gt; (no closing tag)
- A tag that could have content, but doesn't: &lt;foo&gt;&lt;/foo&gt;

## Thanks to...

We owe a huge debt of gratitude to the original authors of html5lib.

While not much of the orignal parser remains, we learned a lot from
reading the html5lib library. And some pieces remain here. In
particular, much of the UTF-8 and Unicode handling is derived from the
html5lib project.

## License

This software is released under the MIT license. The original html5lib
library was also released under the MIT license.
