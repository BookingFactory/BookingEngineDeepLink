# The Booking Factory IBE Deep Link manual

## Booking Steps And Anchors

Anchore | Description
---------|---------
#/ | Select Dates
#/choose-room | Select Room
#/choose-offer | Select Rate
#/choose-extras | Select Extras (optional)
#/summary | Summary Screen
#/payment | Payment Screen*

\* Payment screen is not allow direct access right now. This feature will be added later.

## Deep links

**Deep Link** - link with predefined data for minimize count of client steps at booking process.

Each Deep Link should be build by next pattern:

```
[public_booking_page_address]/[arguments][step_anchore]
```

_**Example**_:
```
https://spilmanhotel.co.uk/book/?dateFrom=2018-10-09&nights=4#/choose-room
```
This link open second step where client can choose Room with specified checkin date and count of nights.

### Deep Link Rules

For some steps arguments can be optional or required. At next table you can see what rules we use.

Anchore | Step Name | Affected Fields | Required Fields*
---------|---------|---------|---------
#/ | Select Dates | dateFrom, nights, promocode, referer |
#/choose-room | Select Room | dateFrom, nights, promocode, referer | dateFrom, nights
#/choose-offer | Select Rate | dateFrom, nights, promocode, room, referer | dateFrom, nights, room
#/choose-extras | Select Extras (optional) | dateFrom, nights, promocode, room, count, rate, referer | dateFrom, nights, room, count, rate
#/summary | Summary Screen | dateFrom, nights, promocode, room, count, rate, referer | dateFrom, nights, room, count, rate
#/payment | Payment Screen | dateFrom, nights, promocode, room, count, rate, referer | dateFrom, nights, room, count, rate

\* To open requested step by anchore URL you should pass all required fields.

### Format requirements:
Argument | Validation
---------|---------
dateFrom | Valid future date in ISO 8601 (YYYY-MM-DD)
nights | Positive integer greater than 0
promocode | Any string (not have any validations)
room | Valid Room Type Short Name from TheBookingFactory Hotel Settings
count | Positive integer greater than 0
rate | Valid Rate Category ID from TheBookingFactory Hotel Settings, Positive integer grater than 0
referer | Any string to represent partner
currency | Use one of presented currencies, like USD, EUR, THB etc.
lng | Use one of presented languages, line es, en, ru, etc
