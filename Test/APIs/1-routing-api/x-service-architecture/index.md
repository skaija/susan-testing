---
title: Service architecture
description:
  info: Routing API enables developers to query routes and timetable related information using either REST or GraphQL interfaces.
  architecture: https://raw.githubusercontent.com/HSLdevcom/digitransit-site/master/pages/en/developers/routing-api/architecture.xml
assets:
  source: https://github.com/HSLdevcom/OpenTripPlanner
  dockerHub: https://hub.docker.com/r/hsldevcom/opentripplanner/
  Dockerfile: https://github.com/HSLdevcom/OpenTripPlanner/blob/master/Dockerfile
technologies:  
  "GTFS-RT": "https://developers.google.com/transit/gtfs-realtime/"
  "GTFS": "https://developers.google.com/transit/gtfs/"
  "Java": null
docker:
  dockerfile: https://github.com/HSLdevcom/OpenTripPlanner/blob/master/Dockerfile
  imageName: hsldevcom/opentripplanner
  buildScript: https://github.com/HSLdevcom/OpenTripPlanner/blob/master/build-docker-image.sh
  runContainer: docker run -e OTP_DATA_CONTAINER_URL=http://otp-data-container:8080 -p 8080:8080 hsldevcom/opentripplanner
  accessContainer: http://localhost:8080/routers/
---
Routing API is implemented using OpenTripPlanner.
> http://www.opentripplanner.org/

## Static and realtime information

OpenTripPlanner APIs provide access to static and realtime routing and transit information.
Routing and timetable data is based on static GTFS and it is enriched by realtime information for those departures that have realtime information available. This means that results returned by OpenTripPlanner always contain realtime information should it be
available.

## API Documentation

### REST

REST interface is provided as it is available in OpenTripPlanner. First thing to do is to familiarize yourself with OpenTripPlanner documentation:
> http://docs.opentripplanner.org/en/latest/

OpenTripPlanner requires developers to make API requests through routers. Digitransit providers routers for Helsinki region, the Waltti regions and entire Finland:

| Region                        | Router URL                              |
|-------------------------------|-----------------------------------------|
| Helsinki region | http://api.digitransit.fi/routing/v1/routers/hsl/     |
| Waltti regions  | http://api.digitransit.fi/routing/v1/routers/waltti/  |
| Entire Finland  | http://api.digitransit.fi/routing/v1/routers/finland/ |

### GraphQL

GraphQL API is built by us. Similarly to REST, GraphQL has different router endpoints for Helsinki region, the Waltti regions and entire Finland. 

**For more details about the GraphQL you can go to our [GraphQL](../0-graphql) page**

#### Introspection query

You can get access to GraphQL schema by running
 [this example in GraphQL console](http://dev.hsl.fi/graphql/console/?query=query%20IntrospectionQuery%20%7B%0A%20%20%20%20__schema%20%7B%0A%20%20%20%20%20%20queryType%20%7B%20name%20%7D%0A%20%20%20%20%20%20mutationType%20%7B%20name%20%7D%0A%20%20%20%20%20%20types%20%7B%0A%20%20%20%20%20%20%20%20...FullType%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20directives%20%7B%0A%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20description%0A%20%20%20%20%20%20%20%20args%20%7B%0A%20%20%20%20%20%20%20%20%20%20...InputValue%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20onOperation%0A%20%20%20%20%20%20%20%20onFragment%0A%20%20%20%20%20%20%20%20onField%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20fragment%20FullType%20on%20__Type%20%7B%0A%20%20%20%20kind%0A%20%20%20%20name%0A%20%20%20%20description%0A%20%20%20%20fields(includeDeprecated%3A%20true)%20%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20args%20%7B%0A%20%20%20%20%20%20%20%20...InputValue%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20type%20%7B%0A%20%20%20%20%20%20%20%20...TypeRef%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20isDeprecated%0A%20%20%20%20%20%20deprecationReason%0A%20%20%20%20%7D%0A%20%20%20%20inputFields%20%7B%0A%20%20%20%20%20%20...InputValue%0A%20%20%20%20%7D%0A%20%20%20%20interfaces%20%7B%0A%20%20%20%20%20%20...TypeRef%0A%20%20%20%20%7D%0A%20%20%20%20enumValues(includeDeprecated%3A%20true)%20%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20isDeprecated%0A%20%20%20%20%20%20deprecationReason%0A%20%20%20%20%7D%0A%20%20%20%20possibleTypes%20%7B%0A%20%20%20%20%20%20...TypeRef%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20fragment%20InputValue%20on%20__InputValue%20%7B%0A%20%20%20%20name%0A%20%20%20%20description%0A%20%20%20%20type%20%7B%20...TypeRef%20%7D%0A%20%20%20%20defaultValue%0A%20%20%7D%0A%20%20fragment%20TypeRef%20on%20__Type%20%7B%0A%20%20%20%20kind%0A%20%20%20%20name%0A%20%20%20%20ofType%20%7B%0A%20%20%20%20%20%20kind%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20ofType%20%7B%0A%20%20%20%20%20%20%20%20kind%0A%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20ofType%20%7B%0A%20%20%20%20%20%20%20%20%20%20kind%0A%20%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D)

## Related open source projects

| Url                           | Open source project                     |
|-------------------------------|-----------------------------------------|
| https://github.com/opentripplanner/OpenTripPlanner            | OpenTripPlanner upstream development on GitHub
| https://groups.google.com/forum/#!forum/opentripplanner-dev   | OpenTripPlanner developers forum where you can view or create new posts as a developer
| https://groups.google.com/forum/#!forum/opentripplanner-users | OpenTripPlanner users forum where you can view or create new posts as an end user
| https://onebusaway.org/                                       | OneBusAway: The Open Source platform for Real Time Transit Info
| https://github.com/OneBusAway?utf8=✓&query=gtfs               | GTFS related projects: Open-source transit app for real-time information
| https://developers.google.com/transit/                        | Google developers transit community: Making public transit data universally accessible
| https://github.com/conveyal/r5                                | Conveyal R5 development on GitHub: Rapid Realistic Routing on Real-world and Reimagined networks
| https://blog.conveyal.com/                                    | Conveyal and their blog

1. Keep up with OpenTripPlanner upstream development on GitHub<br/>
   https://github.com/opentripplanner/OpenTripPlanner

2. Follow OpenTripPlanner developers mailing list:<br/>
   https://groups.google.com/forum/#!forum/opentripplanner-dev

3. Follow OpenTripPlanner users mailing list:<br/>
   https://groups.google.com/forum/#!forum/opentripplanner-users

4. Keep up with Conveyal R5 development on GitHub<br/>
   https://github.com/conveyal/r5

5. Keep up with Conveyal and their blog:<br/
   http://conveyal.com/blog/

6. Keep up with OneBusAway and especially GTFS related projects<br/>
   http://onebusaway.org/<br/>
   https://github.com/OneBusAway?utf8=%E2%9C%93&query=gtfs

7. Follow Google transit community and its mailing lists:<br/>
   https://developers.google.com/transit/community?hl=en