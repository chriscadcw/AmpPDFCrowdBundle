AmpPDFCrowdBundle
=================

This bundle act as a thin wrapper over the PDFCrowd API to ease integration with Symfony.

[![Build Status](https://secure.travis-ci.org/hubertperron/AmpPDFCrowdBundle.png)](http://travis-ci.org/hubertperron/AmpPDFCrowdBundle)

## Installation

### Using composer

    {
        "repositories": [
            {
                "type": "package",
                "package": {
                    "name": "pdfcrowd/pdfcrowd-php",
                    "version": "2.5",
                    "dist": {
                        "url": "http://pdfcrowd.com/static/clients/php/pdfcrowd-2.5-php.zip",
                        "type": "zip"
                    },
                    "autoload": {
                        "files": ["pdfcrowd.php"]
                    }
                }
            }
        ],
        "require": {
            "amp/pdfcrowd-bundle": "dev-master"
        }
    }

### Add the bundle to your application kernel

``` php
// File: app/AppKernel.php
public function registerBundles()
{
    return array(
        // ...
        new Amp\PDFCrowdBundle\AmpPDFCrowdBundle(),
        // ...
    );
}
```

## Configuration

``` yaml
amp_pdf_crowd:
    username: your-username
    apikey: the-api-key
```

## Usage

### Controller

``` php
$pdfCrowd = $this->get('amp_pdf_crowd.api');
$url = $this->generateUrl('route_name', array(), true);

$pdfData = $pdfCrowd->convertURI($url);
$fileName = $this->container->getParameter('kernel.root_dir') . '/../web/pdfs/example.pdf';

file_put_contents($fileName, $pdfData); // Make sure this directory is writable
```

### Command

``` bash
 $ app/console pdfcrowd:convert https://github.com/hubertperron/AmpPDFCrowdBundle web/pdfs/example.pdf
```