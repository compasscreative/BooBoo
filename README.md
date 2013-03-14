BooBoo
======

## Introduction

BooBoo is a single PHP class that helps manages uncaught exceptions and errors, including fatal errors. BooBoo does not display the errors, but rather provides a callback so your specific application can display them in a meaningful way. You may also include an, optional, PSR-3 compatible logger.

## Basic usage

```php
<?php

BooBoo::setup(function($e)
{
	// Set our response code
	http_response_code(500);

	// Display error
	die($exception->getMessage());

});
```

## Advanced usage

```php
<?php

// Setup logger
$logger = new Logger('errors');
$logger->pushHandler(new StreamHandler('logs/errors.log'));

// Setup error handler
BooBoo::setup(function($e)
{
	// Set our response code
	http_response_code(500);

	// Display error view
	$view = new View('error.php');
	$view->exception = $e;
	$view->render();

}, $logger);
```