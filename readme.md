# Modus - NHTSA

PHP API ([Lumen](http://lumen.laravel.com/docs) based) allowing clients to view rating of vehicles via
 [NHTSA NCAP 5 Star Safety Ratings API](https://one.nhtsa.gov/webapi/Default.aspx?SafetyRatings/API/5)

## Requirements
* PHP >= 5.6.4
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension

**Note:** If you get error `(60) SSL certificate : unable to get local issuer certificate`, do the follow steps

* Download the latest [cacert.pem](https://curl.haxx.se/ca/cacert.pem) and place into your local
* Add the following line to php.ini
```
 curl.cainfo=/path/to/downloaded/cacert.pem
 openssl.cafile=/path/to/downloaded/cacert.pem
 ```
* Restart server to apply changes

## Installation
The system utilizes [Composer](https://getcomposer.org/download/) to manage its dependencies. So, before using the system, make sure you have `Composer` installed on your machine.

* Clone repository via git 
```
https://github.com/anhht83/modus-nhtsa.git
```
* Move to `<root>` directory
```
cd <root>
```
* Download vendors and Install 
```
composer install
```
* Start Server 
```
php -S localhost:8080 -t ./public
```

Make sure the server port `8080` is available (You can change to other port)

## API Document
http://docs.modusnhtsaapi.apiary.io

## Example
You could use [Postman app](https://www.getpostman.com/apps) to run examples

**Requirement 1**

Can we visit the following Requirement 1 URLs and get meaningful JSON output from them:

* `GET http://localhost:8080/vehicles/2015/Audi/A3`
* `GET http://localhost:8080/vehicles/2015/Toyota/Yaris`
* `GET http://localhost:8080/vehicles/2015/Ford/Crown Victoria`
* `GET http://localhost:8080/vehicles/undefined/Ford/Fusion`

**Requirement 2**

Can we visit the Requirement 2 URL when sending each of the following JSON request bodies and get meaninful JSON output from each:

```
POST http://localhost:8080/vehicles
```

```
{
    "modelYear": 2015,
    "manufacturer": "Audi",
    "model": "A3"
}
```

```
{
    "modelYear": 2015,
    "manufacturer": "Toyota",
    "model": "Yaris"
}
```

Note - the JSON body below is erroneous, and should not crash your application but should return an empty `Results` object and set `Count` to `0` in your response.

```
{
    "manufacturer": "Honda",
    "model": "Accord"
}
```

**Requirement 3**

Can we visit the following Requirement 2 URLs and get meaningful JSON output from them:

* `GET http://localhost:8080/vehicles/<MODEL YEAR>/<MANUFACTURER>/<MODEL>?withRating=true`
* `GET http://localhost:8080/vehicles/<MODEL YEAR>/<MANUFACTURER>/<MODEL>?withRating=false` (should return the same output as Requirement 1)
* `GET http://localhost:8080/vehicles/<MODEL YEAR>/<MANUFACTURER>/<MODEL>?withRating=bananas` (should return the same output as Requirement 1)
* `GET http://localhost:8080/vehicles/<MODEL YEAR>/<MANUFACTURER>/<MODEL>` (should return the same output as Requirement 1)

## License

[MIT license](http://opensource.org/licenses/MIT)
