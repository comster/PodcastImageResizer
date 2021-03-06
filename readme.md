# Podcastimages.com

This server contains images for podcasts, at any size.

## Documentation

You get the image by doing a CRC32 of the image url (minus the protocol scheme) and calling:

`https://podcastimages.com/<crc32>_<resolution>.jpg`

So, for the image url:

`https://www.theincomparable.com/imgs/logos/logo-batmanuniversity-3x.jpg?cache-buster=2019-06-11`

`CRC32('www.theincomparable.com/imgs/logos/logo-batmanuniversity-3x.jpg?cache-buster=2019-06-11')` gives: `1639321931`

If you wanted the 300px square version of that image you would call:

https://podcastimages.com/1639321931_300.jpg

## CRC32 in PHP

```php
echo return_pimgurl('https://podnews.net/static/podnews-2000x2000.png',300);

function return_pimgurl($url,$size) {
    $scheme=parse_url($url, PHP_URL_SCHEME).'://';
    $pos = strpos($url, $scheme);
    if ($pos !== false) {
        $newurl = substr_replace($url, '', $pos, strlen($scheme));
    }
    return 'https://podcastimages.com/'.crc32($newurl).'_'.$size.'.jpg';
}
```
