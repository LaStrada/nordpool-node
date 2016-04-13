# Nordpool Elspot API npm client

[![Build Status](https://travis-ci.org/samuelmr/nordpool.svg?branch=master)](https://travis-ci.org/samuelmr/nordpool)

Unofficial [Nordpool](http://www.nordpoolspot.com/) Elspot API npm client

## Features

- [Prices](http://www.nordpoolspot.com/Market-data1/Elspot/Area-Prices/)
- [Volumes](http://www.nordpoolspot.com/Market-data1/Elspot/Volumes/) (not implemented yet)
- [Capacities](http://www.nordpoolspot.com/Market-data1/Elspot/Capacities1/) (not implemented yet)
- [Flow](http://www.nordpoolspot.com/Market-data1/Elspot/Flow1/) (not implemented yet)


## Usage

### Install

```
npm install nordpool
```

### Example 1: Latest hourly prices from all areas
```js

var nordpool = require('nordpool')
var prices = new nordpool.Prices()

var opts = {
  currency: 'EUR', // can also be 'DKK', 'NOK', 'SEK'
}

prices.hourly(opts, function (error, results) {
  if (error) console.err(error)
  for (var i=0; i<results.length; i++) {
    var date = results[i].date // moment object (see http://momentjs.com/)
    var price = results[i].value // float, EUR/MWh
    var hourlyPriceMessage = results[i].area +
      " at " + date.format("DD.MM. H:mm") + ": " + price/10 + " eurocent/kWh"
    console.log(hourlyPriceMessage)
  }
})

```

### Example 2: Weekly prices in Bergen

```js

var nordpool = require('nordpool')
var prices = new nordpool.Prices()

var opts = {}
opts.currency = 'NOK'
opts.area = 'Bergen', // DK2, EE1, FI, 'Kr.sand', LT, LV, 'Oslo', SE1, SE4, ...
opts.from = '2015-01-01'

prices.weekly(opts, function (error, results) {
  if (error) console.err(error)
  for (var i=0; i<results.length; i++) {
    var date = results[i].date // moment object (see http://momentjs.com/)
    var price = results[i].value // float, EUR/MWh
    var weeklyPriceMessage = "The price on week " + date.format("W/Y") +
      " was " + price + " NOK/MWh"
    console.log(weeklyPriceMessage)
  }
})

```

See possible `area`s (regions) from [nordpoolspot.com](http://www.nordpoolspot.com/Market-data1/Elspot/Area-Prices/)