# litlife/fb2-to-html

This package can be used to convert fb2 to html

## Installation

Use the package manager [composer](https://getcomposer.org/) to install.

```bash
composer require litlife/fb2-to-html
```

## Usage

### Generate new sitemap and add new url

```bash
use DOMDocument;
use Litlife\Fb2ToHtml\Fb2ToHtml;

$inputXml = <<<EOT
<FictionBook xmlns="http://www.gribuser.ru/xml/fictionbook/2.0" xmlns:l = "http://www.w3.org/1999/xlink">
<body>
<section>
<poem>
<stanza>
<v>text</v>
<v>text</v>
</stanza>
<text-author>Author</text-author>
</poem>
</section>
</body>
</FictionBook>
EOT;

$customClassNamePrefix = 'my-';

$dom = new DOMDocument();
$dom->loadXML($inputXml);

$class = new Fb2ToHtml($customClassNamePrefix);
$html = $class->toHtml($dom->getElementsByTagName('section')->item(0)->childNodes);

print($html);
```
Output html:

```
<div class="my-poem">
<div class="my-stanza">
<p>text</p>
<p>text</p>
</div>
<div class="my-text-author">Author</div>
</div>
```

## Testing
```bash
composer test
```
## License
[MIT](https://choosealicense.com/licenses/mit/)
