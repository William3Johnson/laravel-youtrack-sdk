# Laravel YouTrack SDK

![cog-laravel-youtrack-sdk](https://cloud.githubusercontent.com/assets/1849174/26226734/98de7ac6-3c36-11e7-9017-4c0f2151ec81.png)

<p align="center">
<a href="https://travis-ci.org/cybercog/laravel-youtrack-sdk"><img src="https://img.shields.io/travis/cybercog/laravel-youtrack-sdk/master.svg?style=flat-square" alt="Build Status"></a>
<a href="https://styleci.io/repos/91741303"><img src="https://styleci.io/repos/91741303/shield" alt="StyleCI"></a>
<a href="https://codeclimate.com/github/cybercog/laravel-youtrack-sdk"><img src="https://img.shields.io/codeclimate/github/cybercog/laravel-youtrack-sdk.svg?style=flat-square" alt="Code Climate"></a>
<a href="https://github.com/cybercog/laravel-youtrack-sdk/releases"><img src="https://img.shields.io/github/release/cybercog/laravel-youtrack-sdk.svg?style=flat-square" alt="Releases"></a>
<a href="https://github.com/cybercog/laravel-youtrack-sdk/blob/master/LICENSE"><img src="https://img.shields.io/github/license/cybercog/laravel-youtrack-sdk.svg?style=flat-square" alt="License"></a>
</p>

## Introduction

Laravel wrapper for the [YouTrack REST PHP client library](https://github.com/cybercog/youtrack-rest-php). 

## Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
    - [Initialize API client](#initialize-api-client)
    - [API requests](#api-requests)
    - [API responses](#api-responses)
- [Change log](#change-log)
- [Contributing](#contributing)
- [Testing](#testing)
- [Security](#security)
- [Credits](#credits)
- [Alternatives](#alternatives)
- [License](#license)
- [About CyberCog](#about-cybercog)

## Features

- Using contracts to keep high customization capabilities.
- Multiple authentication strategies: Token, Cookie.
- Utilizes PHP Standard Recommendations:
  - [PSR-2 (Coding Style Guide)](http://www.php-fig.org/psr/psr-2/).
  - [PSR-4 (Autoloading Standard)](http://www.php-fig.org/psr/psr-4/).
  - [PSR-7 (HTTP Message Interface)](http://www.php-fig.org/psr/psr-7/).
- Covered with unit tests.

## Requirements

- YouTrack >= 2017.1 with REST-API enabled (always enabled, by default)
- PHP >= 7.1
- Guzzle HTTP Client >= 6.2

## Installation

The preferred method is via [composer](https://getcomposer.org). Follow the
[installation instructions](https://getcomposer.org/doc/00-intro.md) if you do not already have
composer installed.

Once composer is installed, execute the following command in your project root to install this library:

```sh
$ composer require cybercog/laravel-youtrack-sdk
```

Include the service provider within `app/config/app.php`:

```php
'providers' => [
    Cog\Laravel\YouTrack\Providers\YouTrackServiceProvider::class,
],
```

## Usage

### Initialize API client

```php
$youtrack = app(\Cog\YouTrack\Rest\YouTrackClient::class);
```

Starting with YouTrack 2017.1 release [authorization based on permanent tokens](https://www.jetbrains.com/help/youtrack/standalone/2017.2/Manage-Permanent-Token.html) is recommended as the main approach for the authorization in your REST API calls.

By default API client will use Permanent Token authentication. But if you want you could redefine it in `.env` file:

```
YOUTRACK_AUTH=cookie
```

### API requests


#### HTTP GET request

```php
$response = $youtrack->get('/issue/TEST-1');
```

#### HTTP POST request

```php
$response = $youtrack->post('/issue', [
    'project' => 'TEST',
    'summary' => 'New test issue',
    'description' => 'Test description',
]);
```

#### HTTP PUT request

```php
$response = $youtrack->put('/issue/TEST-1', [
    'summary' => 'Updated summary',
    'description' => Updated description,
]);
```

#### HTTP DELETE request

```php
$response = $youtrack->delete('/issue/TEST-1');
```

### API responses

Each successful request to the API returns instance of `\Cog\YouTrack\Rest\Response\Contracts\Response` contract. By default it's `\Cog\YouTrack\Rest\Response\YouTrackResponse` class.

#### Get PSR HTTP response

PSR HTTP response could be accessed by calling `getResponse` method on API Response.

```php
$youtrackResponse = $youtrack->get('/issue/TEST-1');
$psrResponse = $youtrackResponse->getResponse();
```

#### Get response Cookie

```php
$apiResponse = $youtrack->get('/issue/TEST-1');
$cookieString = $apiResponse->getCookie();
```

#### Get response Location

```php
$apiResponse = $youtrack->get('/issue/TEST-1');
$location = $apiResponse->getLocation();
```

#### Transform response to array

```php
$apiResponse = $youtrack->get('/issue/TEST-1');
$location = $apiResponse->toArray();
```

#### Get HTTP response status code

```php
$apiResponse = $youtrack->get('/issue/TEST-1');
$location = $apiResponse->getStatusCode();
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Testing

Run the tests with:

```sh
$ composer test
```

## Security

If you discover any security related issues, please email oss@cybercog.su instead of using the issue tracker.

## Credits

- [Anton Komarev](https://github.com/a-komarev)
- [All Contributors](../../contributors)

## Alternatives

Alternatives not found.

*Feel free to add more alternatives as Pull Request.*

## License

- `YouTrack REST PHP` package is open-sourced software licensed under the [MIT License](LICENSE).

## About CyberCog

[CyberCog](http://www.cybercog.ru) is a Social Unity of enthusiasts. Research best solutions in product & software development is our passion.

![cybercog-logo](https://cloud.githubusercontent.com/assets/1849174/18418932/e9edb390-7860-11e6-8a43-aa3fad524664.png)
