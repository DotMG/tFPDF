# tFPDF
**This repository is only made for cloning official tFPDF releases which are available at: 
http://fpdf.org/en/script/script92.php THERE WILL BE NO DEVELOPMENT IN THIS REPOSITORY!**

_The only change in this version is that the require_once() calls to font/unifont/ttfonts.php
are commented and resolved through the composer autoloader. The demo ex.php was changed
accordingly, too._

**This is a fork of setasign/tFPDF, where a new method SetCellMargin() was added**

$cMargin is a private property, but I needed to change it to be able to match the result of GetStringWidth() with MultiCell() or Cell(). This is because GetStringWidth() does not consider a cell margin, while Cell() or MultiCell() uses a non-zero value of cell margin ($cMargin). As I didn't necessarily want any cell Margin, I added this method to reset $cMargin to zero. Without resetting $cMargin to zero, if I calculated the size of a string with GetStringWidth() and used Cell() or MultiCell() with that width and with the same text, I sometimes end up having automatic carriage return on my PDF, due to cell margins.

**As I have proposed the changes to the maintainer of tFPDF, if such changes are added to the official version, I will very likely delete my own fork**

tFPDF accepts UTF-8 encoded text. It embeds font subsets allowing small PDF files.

It requires a folder 'unifont' as a subfolder of the 'font' folder.

You should make the 'unifont' folder writeable (CHMOD 755 or 644). Although this
is not essential, it allows caching of the font metrics the first time a font is used,
making subsequent uses much faster.

All tFPDF requires is a .ttf TrueType font file. The file should be placed in the
'unifont' directory. Optionally, you can also define the path to your system fonts e.g. 'C:\Windows\Font'
(see the example ex.php file) and reference TrueType fonts in this directory.

Pass a fourth parameter as true when calling AddFont(), and use utf-8 encoded text 
when using Write() etc.

## Installation with [Composer](https://packagist.org/packages/setasign/tfpdf)

If you're using Composer to manage dependencies, you can use

    $ composer require setasign/tfpdf:1.33

or you can include the following in your composer.json file:

```json
{
    "require": {
        "setasign/tfpdf": "1.33"
    }
}
```

## Usage

Notice that tFPDF is not name-spaced. You can extend the class this way:

```php 
namespace your\namespace;
    
class Document extends \tFPDF
```

or create an instance this way:

```php 
$pdf = new \tFPDF();
```
