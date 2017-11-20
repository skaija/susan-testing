---
title: Bicycling
---

**If you are not familiar with [GrpahQL](../0-graphql) and [GraphiQL](../1-graphiql) yet it is highly recommended to review those pages at first.**

## Bicycling related query types

Routing API provides three types of queries you can run related to bicycling:

-	City bike rental stations and bikes that are available in Helsinki
-	City bike parks that are available in Helsinki
-	Bicycling routes using city bike or your personal bike

## City bikes

**Note:** City bikes are available in Helsinki only.

**Note:** City bike API data is realtime and it is always up to date.

> https://www.hsl.fi/en/citybikes

![citybikes](./citybikes.png)

## Query examples 

### All available city bike stations

Click [this link]() to run the query below in GraphiQL. It should fetch all available city bike stations.

```
{
  bikeRentalStations {
    name
    stationId
  }
}
```

### City bike station and its current bike availability details

Click [this link]() to run the query below in GraphiQL. It should fetch the city bike station with id B07, and its current bike availability details.

```
{
  bikeRentalStation(id:"B07") {
    stationId
    name
    bikesAvailable
    spacesAvailable
    lat
    lon
    allowDropoff
  }
}
```

### All available city bike parks

Click [this link]() to run the query below in GraphiQL. It should fetch all available city bike parks.

```
{
  bikeParks{
    id
    bikeParkId
    name
    spacesAvailable
  }
}
```

### Available city bike park

Click [this link]() to run the query below in GraphiQL. It should fetch the city bike park with id 906 and its current space availability details.

```
{
  bikePark(id:"906") {
    id
    bikeParkId
    name
    spacesAvailable
    lat
    lon
  }
}

```

### Route from Kamppi to Kasarmitori using city bike rental

Click [this link]() to run the query below in GraphiQL. It should fetch route from Kamppi to Kasarmitori using city bike rental and show also rental stations.

**Note:** Use of mode BICYCLE_RENT, which is not returned as mode.

```
{
  plan(
    fromPlace: "Kamppi, Helsinki",
    from: {lat: 60.168992, lon: 24.932366},
    toPlace: "Kasarmitori, Helsinki",
    to: {lat: 60.165246, lon: 24.949128},
    numItineraries: 3,
    modes: "BICYCLE_RENT,BUS,TRAM,SUBWAY,RAIL,FERRY,WALK",
    walkReluctance: 2.1,
    walkBoardCost: 600,
    minTransferTime: 180,
    walkSpeed: 1.2
  ) {
    itineraries{
      walkDistance,
      duration,
      legs {
        mode
        startTime
        endTime
        from {
          lat
          lon
          name
          bikeRentalStation {
            stationId
            name
          }
          stop {
            name
          }
        },
        to {
          lat
          lon
          name
        },
        agency {
          id
        },
        distance
        legGeometry {
          length
          points
        }
      }
    }
  }
}
```

### Query Bicycle route from Kamppi to Pisa riding your personal bike

Click [this link]() to run the query below in GraphiQL. It should fetch bicycle route from Kamppi to Pisa.

**Note:** maxWalkDistance is used for cycling too

```
{
  plan(
    fromPlace: "Kamppi, Helsinki",
    from: {lat: 60.168992, lon: 24.932366},
    toPlace: "Pisa, Espoo",
    to: {lat: 60.175294, lon: 24.684855},
    modes: "BICYCLE",
    walkReluctance: 2.1,
    walkBoardCost: 600,
    minTransferTime: 180,
    walkSpeed: 1.2,
    maxWalkDistance: 10000
  ) {
    itineraries{
      walkDistance,
      duration,
      legs {
        mode
        startTime
        endTime
        from {
          lat
          lon
          name
          stop {
            code
            name

          }
        },
        to {
          lat
          lon
          name
        },
        agency {
          id
        },
        distance
        legGeometry {
          length
          points
        }
      }
    }
  }
}
```
