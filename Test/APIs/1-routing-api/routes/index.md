---
title: Routes
---

**If you are not familiar with [GraphQL](../0-graphql) and [GraphiQL](../1-graphiql) yet it is highly recommended to review those pages at first.**

## Glossary

| Term                                  | Explanation                     |
|---------------------------------------|---------------------------------|
| Routes                                | A public transport service shown to customers under a single name, usually from point A to B and back. For example: trams 1 and 1A, buses 18 and 102T, or train A. Commonly used synonym: line
| Pattern                               | A sequence of stops as used by a specific direction and variant of a route. For example a tram entering/departing service from/to the depot usually joins at the middle of the route, or a route might have a short term diversion (poikkeusreitti) without changing the route name (longer diversions usually are marked as different routes).
| Trip                                  | A specific occurance of a route, usually identified by the route and exact departure time from the first stop. For example bus 102 leaving from Otaniemi on 2017-11-21 10:00, or more generally leaving from Otaniemi at 10:00 on specified days (e.g. Monday to Friday from 2015-11-20 to 2016-11-24 excluding holidays).

## Query examples

**Note:** For more details about the query type **routes** and its parameters you can use **Documentation Explorer** provided in GraphiQL.

**Note:** If the examples provided with some id or other value do not return what is expected then the value in question may not be in use any more and you should try again with an existing value.

### Query all bus routes where number is like "58*"

1. Click [this link](https://api.digitransit.fi/graphiql/hsl?query=%7B%0A%20%20routes(name%3A%20%2258%22%2C%20modes%3A%20%22BUS%22)%20%7B%0A%20%20%20%20id%0A%20%20%20%20agency%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%7D%0A%20%20%20%20shortName%0A%20%20%20%20longName%0A%20%20%20%20desc%0A%20%20%7D%0A%7D) to run the query below in GraphiQL.

```
{
  routes(name: "58", modes: "BUS") {
    id
    agency {
      id
    }
    shortName
    longName
    desc
  }
}
```

2. Press play in GraphiQL to execute the query.

### Query all tram routes where number is like "1*"

1. Click [this link](https://api.digitransit.fi/graphiql/hsl?query=%7B%0A%20%20routes(name%3A%20%221%22%2C%20modes%3A%20%22TRAM%22)%20%7B%0A%20%20%20%20id%0A%20%20%20%20agency%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%7D%0A%20%20%20%20shortName%0A%20%20%20%20longName%0A%20%20%20%20desc%0A%20%20%7D%0A%7D) to run the query below in GraphiQL.

```
{
  routes(name: "1", modes: "TRAM") {
    id
    agency {
      id
    }
    shortName
    longName
    desc
  }
}
```

2. Press play in GraphiQL to execute the query.

### Query stop names for bus number 50 for one direction

1. Click [this link](https://api.digitransit.fi/graphiql/hsl?query=%7B%0A%20%20pattern(id%3A%22HSL%3A1050%3A1%3A01%22)%20%7B%0A%20%20%20%20name%0A%20%20%20%20stops%7B%0A%20%20%20%20%20%20name%20%20%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D) to run the query below in GraphiQL.

```
{
  pattern(id:"HSL:1050:1:01") {
    name
    stops{
      name  
    }
  }
}
```

2. Press play in GraphiQL to execute the query.