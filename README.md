# LongRunning

![Tests](https://github.com/LongRunning/LongRunning/workflows/Tests/badge.svg?branch=main)

This is the LongRunning mono repository for the following packages:

* [core](https://github.com/LongRunning/core)
* [doctrine-orm](https://github.com/LongRunning/doctrine-orm)
* [sentry](https://github.com/LongRunning/sentry)

## Installation

:warning: Instead of installing this mono repository we recommend you to install the sub packages instead. See above.

```
composer require long-running/long-running
```

## Symfony

If you are using Symfony, make sure to enable the bundle:
```php
<?php
// config/bundles.php

return [
    // ...
    LongRunning\Core\Bundle\LongRunningBundle::class => ['all' => true],
];
```

## How to use?

```php
<?php

final class MyCleaner implements \LongRunning\Core\Cleaner
{
    public function cleanUp() : void
    {
        echo "Cleaning up memory!";
    }
}

$cleaner = new \LongRunning\Core\DelegatingCleaner([
    new MyCleaner(),
]);

while (true) {
    // Do heavy work, like processing jobs from a queue
    echo "Doing heavy work";
    sleep(1);
    echo "Done with heavy work";

    // Cleanup things
    $cleaner->cleanUp();
}
```

## Existing cleaners

LongRunning provides 2 packages that add additional cleaners:

* [doctrine-orm](https://github.com/LongRunning/doctrine-orm)
* [sentry](https://github.com/LongRunning/sentry)


## Upgrading

If you are coming from LongRunning 0.5.0 please refer to [UPGRADING.md](UPGRADING.md).
