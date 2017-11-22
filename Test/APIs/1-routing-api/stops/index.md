---
title: Stops
---

**If you are not yet familiar with [GraphQL](../0-graphql) and [GraphiQL](../1-graphiql) it is highly recommended to review those pages at first.**

## Terms

First, let’s define some terms:

**Agency** is some public transport provider, e.g. HSL.

Also, familiarize yourself with [routes terms](../routes/).

## Notes about stop ids

Stop ids are in "acencyid:stopid" format. HSL agencyid is **HSL**. Stop id is available as **gtfsId**.

## Query examples

**Note:** For more details about the query type **stops** you can use the **Documentation Explorer** provided in GraphiQL.

**Note:** If the examples provided with an id do not return what is expected then the id in question may not be in use any more and you should try again with an existing id.

### Query all stops, returning their id, name and location
```
{
  stops{
    gtfsId
    name
    lat
    lon
  }
}
```

### Query stop by id:
```
{
  stop(id: "HSL:1173210") {
    name
    wheelchairBoarding
  }
}
```

### Query stop by id and information about routes that go through it
```
{
  stop(id: "HSL:1173112") {
    name
    lat
    lon
    patterns {
      id
      name
      route {
        gtfsId
        shortName
        longName
      }
      directionId
    }
  }
}
```


### Query all stops where name is like "hertton"
```
{
  stops(name: "hertton") {
    id
    name
    wheelchairBoarding
  }
}
```

### Query a stop by number
```
{
  stops(name: "4040") {
    id
    name
    wheelchairBoarding
  }
}
```
