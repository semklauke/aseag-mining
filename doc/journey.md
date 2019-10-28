## journey
> http://ivu.aseag.de/interfaces/ura/journey?


### Query parameters

| key            | type                     | required | default | info |
|:---------------|:-------------------------|:---------|:--------|:-----|
| startStopId    | number (int)             | ✓        | -       | can be obtained by. e.g **instance** |
| endStopId      | number (int)             | ✓        | -       | an be obtained by. e.g **instance**  |
| departureTime  | number (timestamp)       | ✓        | -       | unix timestamp in *millisecounds !!!* So timestamp * 1000 |
| arrivalTime    | number (timestamp)       | ✖ / ✓    | -       | Can be used istead of depatrureTime |
| minTimeChanges | number (int)             | ✖        | 2       | not sure of this has really an effect. Couldn't find a difference between default value and 0 |
| maxNumChanges  | number (int)             | ✖        | 8       | "    | 
| maxWaitingTime | number (int)             | ✖        | 90      | propably minutes. Not sure if just waiting time to the first bus or sum of all waiting times (when changing bus) |
| maxNumResults  | number (int)             | ✖        | 10      | -    |     



### Return object


**`type`: _string_** <br />
 should be "JourneyResults" <br /><br />
**`searchQuery`:** {<br />
&emsp;&emsp;**`queryString`: _string_** <br />
&emsp;&emsp; full HTTP query string (with defaults)<br />
}<br /><br />
**`resultCount`: _int_** <br />
 length of array `resultList` (see below)<br /><br />
**`maxJourneyDurationInS`: _int_** <br /><br />
**`resultList`:** [<br />
&emsp;{<br />
&emsp;&emsp;**`type`: _string_** <br />
&emsp;&emsp; should be "Journey"<br /><br />
&emsp;&emsp;**`mode`: _string_** <br />
&emsp;&emsp; I've only seen "Compact"<br /><br />
&emsp;&emsp;**`uuid`: _string_** <br />
&emsp;&emsp; list of all uuid's for this journey (only one if you dont have change buses)<br />
&emsp;&emsp; For structure of uuid's look at [uuid.md](./uuid.md)<br /><br />
&emsp;&emsp;**`status`: _string_** <br >
&emsp;&emsp; known values: ["OK", ]<br /><br />
&emsp;&emsp;**`messageList`: []** <br >
&emsp;&emsp; I've only seen this array empty<br /><br />
&emsp;&emsp;**`queryString`: _string_** <br >
&emsp;&emsp; same `queryString` as above<br /><br />
&emsp;&emsp;**`startTimeInUnixEpochMillis`: _int_** <br /><br />
&emsp;&emsp;**`endTimeInUnixEpochMillis`: _int_** <br /><br />
&emsp;&emsp;**`currentServerTimeInUnixEpochMillis `: _int_** <br /><br />
&emsp;&emsp;**`durationsInS`: {** <br />
&emsp;&emsp;&emsp;&emsp;**`bus`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`walk`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`total`: _int_** <br />
&emsp;&emsp;} <br /><br />
&emsp;&emsp;**`distancesInM`: {** <br />
&emsp;&emsp;&emsp;&emsp;**`bus`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`walk`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`total`: _int_** <br />
&emsp;&emsp;} <br /><br />
&emsp;&emsp;**`startLocation`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;**`endLocation`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;**`elementCount`: _int_** <br />
&emsp;&emsp; number of elements in `elementList` which contains all bus lines<br /><br />
&emsp;&emsp;**`elementList`:** 3 types: **PublicTransportTrip**, **TripChange**, **IndividualTrip** **[** <br />
&emsp;&emsp;&emsp;{ <br />
&emsp;&emsp;&emsp;&emsp;**`type`:** **"PublicTransportTrip"** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`modalType`:** **"bus"** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`uuid`: _string_** <br /> 
&emsp;&emsp;&emsp;&emsp; see [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`uuid`: _string_** <br />
&emsp;&emsp;&emsp;&emsp; uuid of joureny. See [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`start`: _prediction object_ {** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`type`: _string_** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; I've only seen "Prediction" <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`location`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`visitNumber`: _int_** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; Don't know what this is <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
&emsp;&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;&emsp;**`end`: _prediction object_ {** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`type`: _string_** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`location`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`visitNumber`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
&emsp;&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;&emsp;**`durationInS`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`lengthInM`: _int_** <br />
&emsp;&emsp;&emsp;&emsp; Seems to be always 0 for **PublicTransportTrip** (so non walking trip) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`messageList`: []** <br />
&emsp;&emsp;&emsp;&emsp; I've only seen this array empty<br /><br />
&emsp;&emsp;&emsp;&emsp;**`tripId`: _int_** <br />
&emsp;&emsp;&emsp;&emsp; uniqe number from uuid. See [uuid.md](./uuid.md)<br /><br />
&emsp;&emsp;&emsp;&emsp;**`destinationName`: _string_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`destinationText`: _string_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`isSaveConnection`: _bool_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`lineId`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`lineName`: _string_** <br />
&emsp;&emsp;&emsp;&emsp; often same as `lineId` <br /><br />
&emsp;&emsp;&emsp;&emsp;**`vehicleId`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`isLowFloorVehicle`: _bool_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`isAccessible`: _bool_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`haltCount`: _int_** <br /><br />
&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;{ <br />
&emsp;&emsp;&emsp;&emsp;**`type`:** **"IndividualTrip"** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`modalType`:** **"walk"** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`uuid`: _string_** <br /> 
&emsp;&emsp;&emsp;&emsp; see [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`uuid`: _string_** <br />
&emsp;&emsp;&emsp;&emsp; uuid of joureny. See [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`start`: _prediction object_ {** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`type`: _string_** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; I've only seen "Prediction" <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`location`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`visitNumber`: _int_** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; Don't know what this is <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
&emsp;&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;&emsp;**`end`: _prediction object_ {** <br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`type`: _string_** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`location`: _location object_** [location.md](./location.md) **{** ... **}** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`visitNumber`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
&emsp;&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;&emsp;**`durationInS`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`lengthInM`: _int_** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`messageList`: []** <br />
&emsp;&emsp;&emsp;&emsp; I've only seen this array empty<br /><br />
&emsp;&emsp;&emsp;&emsp;**`isAccessible`: _bool_** <br /><br />
&emsp;&emsp;&emsp;} <br /><br />
&emsp;&emsp;&emsp;{ <br />
&emsp;&emsp;&emsp;&emsp;**`type`:** **"TripChange"** <br /><br />
&emsp;&emsp;&emsp;&emsp;**`durationInS`: _int_** <br />
&emsp;&emsp;&emsp;&emsp; Time to wait between buses <br /><br />
&emsp;&emsp;&emsp;&emsp;**`source`: _string_** <br />
&emsp;&emsp;&emsp;&emsp; uuid of incoming/prev. trip object. See [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;&emsp;**`target`: _string_** <br />
&emsp;&emsp;&emsp;&emsp; uuid of outgoing/next trip object. See [uuid.md](./uuid.md) <br /><br />
&emsp;&emsp;&emsp;} <br /><br />
&emsp;}<br /><br />
]<br /><br />
