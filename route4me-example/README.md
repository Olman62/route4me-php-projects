# Sample Route4Me PHP Project

The sample project demonstrates the download and usage of the Route4Me php SDK from **packagist.org**.

To create a PHP project using Route4me SDK, do following:

- Createa a folder (e.g. **route4me-example**).  
- Go to the created folder.  
- Create the composer (**composer.json**) file in the folder with content:
```
{
  "name": "company/route4me-php-example",
  "description": "Sample project with Route4Me PHP SDK",
  "minimum-stability": "stable",
  "version": "1.0.0",

  "authors": [
	{
		"name": "John Doe",
		"email": "john-doe@mail.com"
	}
  ],

  "require": {
	"php": ">=7",
	"ext-json": "*",
	"ext-sockets": "*",
	"symfony/process": "*",
	"route4me/route4me-php": "~1.2.0"
  },

  "require-dev": {
	"phpunit/phpunit": "7.5.20"
  },

  "autoload": {
	"psr-4": {
	  "ExampleProject\\": "src/ExampleProject"
	}
  }
}
```

- Change the appropriate parameters to your own (author, email, project name).  
- Run a CLI tool (cmd, powershell, shell) withi the folder and run the command:  
```
composer install
```

- Create the folders **src/ExampleProject/examples** in the core folder and create the PHP file optimization-4stops.php in the folder **examples**. FInally, write the code in it:
```
<?php

namespace ExampleProject;

$root = realpath(dirname(__FILE__).'/../../../');
require $root.'/vendor/autoload.php';

use Route4Me\Enum\OptimizationType;
use Route4Me\Enum\AlgorithmType;
use Route4Me\Enum\DistanceUnit;
use Route4Me\Enum\DeviceType;
use Route4Me\Enum\TravelMode;
use Route4Me\Address;
use Route4Me\Route4Me;
use Route4Me\RouteParameters;
use Route4Me\OptimizationProblemParams;
use Route4Me\OptimizationProblem;

// Set the api key in the Route4me class
Route4Me::setApiKey('11111111111111111111111111111111');

$addresses = array();
$addresses[] = Address::fromArray(array(
    "lng"         => -85.757308,
    "lat"         => 38.251698,
    "is_depot"    => true,
    "time"        => 300,
    "sequence_no" => 0,
    "address"     => "455 S 4th St, Louisville, KY 40202"
));

$addresses[] = Address::fromArray(array(
    "lng"         => -85.793846,
    "lat"         => 38.141598,
    "is_depot"    => false,
    "time"        => 300,
    "sequence_no" => 1,
    "address"     => "1604 PARKRIDGE PKWY, Louisville, KY, 40214"
));

$addresses[] = Address::fromArray(array(
    "lng"         => -85.786514,
    "lat"         => 38.202496,
    "is_depot"    => false,
    "time"        => 300,
    "sequence_no" => 2,
    "address"     => "1407 MCCOY, Louisville, KY, 40215"
));

$addresses[] = Address::fromArray(array(
    "lng"         => -85.774864,
    "lat"         => 38.178844,
    "is_depot"    => false,
    "time"        => 300,
    "sequence_no" => 3,
    "address"     => "4805 BELLEVUE AVE, Louisville, KY, 40215"
));

$parameters = RouteParameters::fromArray(array(
    "algorithm_type"          => AlgorithmType::TSP,
    "distance_unit"           => DistanceUnit::MILES,
    "device_type"             => DeviceType::WEB,
    "optimize"                => OptimizationType::DISTANCE,
    "travel_mode"             => TravelMode::DRIVING,
    "route_max_duration"      => 86400,
    "store_route"             => true,
    "vehicle_capacity"        => 1,
    "vehicle_max_distance_mi" => 10000
));

$optimizationParams = new OptimizationProblemParams;
$optimizationParams->setAddresses($addresses);
$optimizationParams->setParameters($parameters);

$problem = OptimizationProblem::optimize($optimizationParams);

echo 'Optimization problem ID: '.$problem->optimization_problem_id;
```

> **Note**: change the API key provided in the code with your own.

Congratulations, you now have a functional PHP project using the Route4Me PHP SDK from **packagist.org**.