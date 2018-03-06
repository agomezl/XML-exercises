# Flights

Given the following schema:

```
Airports(_code,city)

FlightCodes(_code, airlineName)

Flights(departureAirport, destinationAirport, departureTime, arrivalTime, _code)
  departureAirport ­> Airports.code
  destinationAirport ­> Airports.code
  code ­> FlightCodes.code
```

Write an XML document that contains a DTD corresponding to this
database schema together with the data in the following table (where
you can invent the departure and arrival times yourself).

| Flight code | Airline    | Dep. city  | Dep. airport |  Arr. city | Arr. airport |
|:-----------:|:----------:|:----------:|:------------:|:----------:|:------------:|
| SK111       | SAS        | Gothenburg | GOT          |  Frankfurt | FRA          |
| AF222       | Air France | Paris      | ORY          |  Malta     | MLA          |
| AB222       | Air Berlin | Frankfurt  | FRA          |  Munich    | MUC          |
| KM111       | Air Malta  | Munich     | MUC          |  Malta     | MLA          |
