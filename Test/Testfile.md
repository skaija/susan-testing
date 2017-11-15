## TESTING GraphiQL linking ##

# Query all bus routes where number is like “58” #

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
[Query in GraphiQL](https://api.digitransit.fi/graphiql/hsl?query=%7B%0A%20%20routes(name%3A%20%2258%22%2C%20modes%3A%20%22BUS%22)%20%7B%0A%20%20%20%20id%0A%20%20%20%20agency%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%7D%0A%20%20%20%20shortName%0A%20%20%20%20longName%0A%20%20%20%20desc%0A%20%20%7D%0A%7D)
