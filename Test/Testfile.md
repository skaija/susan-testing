## TESTING GraphiQL linking ##

# Query all bus routes where number is like “58” #


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
