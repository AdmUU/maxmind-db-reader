# MaxMind DB Reader Hyperf API #

## Description ##

This is the MaxMind DB Reader for PHP Hyperf or other resident process framework. It preloads the entire mmdb file into memory, with the memory usage equal to the size of the mmdb file. It has no disk IO operations and maintains query efficiency at the microsecond level.

### Install Dependencies ###

Run in your project root:

```
php composer.phar require webmaster/maxmind-db-reader:~1.0
```

## Usage ##

## Example ##

```php
<?php
namespace App\Service;

use MaxMind\Db\Reader;

class IpLocationService
{
    private $reader;

    public function maxMind(): Reader
    {
        $dbFile = storage_path() . '/ip/GeoIP2-City.mmdb';
        $dbContents = file_get_contents($dbFile, false);
        return new Reader($dbFile, $dbContents);
    }

    public function search(string $ip): string
    {
        if (! $this->reader) {
            $this->reader = $this->maxMind();
        }

        $location = $this->reader->get($ip);

        return $location;
    }

}
```

## Support ##

Please report all issues with this code using the [GitHub issue tracker](https://github.com/AdmUU/maxmind-db-reader/issues).

## Copyright and License ##

This software is Copyright (c) 2014-2025 by MaxMind, Inc.

Modified and developed by the Admin.IM community.