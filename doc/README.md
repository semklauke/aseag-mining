# journey
> http://ivu.aseag.de/interfaces/ura/journey?


## Query parameters

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



## JSON Response


&emsp;**`type`: _string_** <br />
&emsp;&nbsp;should be "JourneyResults" <br /><br />
&emsp;**`searchQuery`:** {<br />
&emsp;&emsp;&emsp;**`queryString`: _string_** <br />
&emsp;&emsp;&emsp; full HTTP query string (with defaults)<br />
&emsp;}<br /><br />
&emsp;**`resultCount`: _int_** <br />
&emsp;&nbsp;length of array `resultList` (see below)<br /><br />
&emsp;**`maxJourneyDurationInS`: _int_** <br /><br />
&emsp;**`resultList`:** []<br />
&emsp;&nbsp;list of **journey objects**. See [journey object](#journey-object)<br /><br />

### { Journey Object }
&emsp;**`type`: _string_** <br />
&emsp;&nbsp;should be "Journey"<br /><br />
&emsp;**`mode`: _string_** <br />
&emsp;&nbsp;I've only seen "Compact"<br /><br />
&emsp;**`uuid`: _string_** <br />
&emsp;&nbsp;list of all uuid's for this journey (only one if you dont have change buses)<br />
&emsp;&nbsp;For structure of uuid's look at [uuids](#uuids)<br /><br />
&emsp;**`status`: _string_** <br >
&emsp;&nbsp;known values: ["OK", ]<br /><br />
&emsp;**`messageList`: []** <br >
&emsp;&nbsp;I've only seen this array empty<br /><br />
&emsp;**`queryString`: _string_** <br >
&emsp;&nbsp;same `queryString` as above<br /><br />
&emsp;**`startTimeInUnixEpochMillis`: _int_** <br /><br />
&emsp;**`endTimeInUnixEpochMillis`: _int_** <br /><br />
&emsp;**`currentServerTimeInUnixEpochMillis `: _int_** <br /><br />
&emsp;**`durationsInS`: {** <br />
&emsp;&emsp;&emsp;**`bus`: _int_** <br />
&emsp;&emsp;&emsp;**`walk`: _int_** <br />
&emsp;&emsp;&emsp;**`total`: _int_** <br />
&emsp;}<br /><br />
&emsp;&emsp;**`distancesInM`: {** <br />
&emsp;&emsp;&emsp;**`bus`: _int_** <br />
&emsp;&emsp;&emsp;**`walk`: _int_** <br />
&emsp;&emsp;&emsp;**`total`: _int_** <br />
&emsp;}<br /><br />
&emsp;**`startLocation`: _location object_** **{** ... **}** <br />
&emsp;&nbsp;A **location object**. See [location object](#location-object)<br /><br />
&emsp;**`endLocation`: _location object_** **{** ... **}** <br />
&emsp;&nbsp;A **location object**. See [location object](#location-object)<br /><br />
&emsp;**`elementCount`: _int_** <br />
&emsp;&nbsp;number of elements in `elementList` which contains all bus lines<br /><br />
&emsp;**`elementList`:** []<br />
&emsp;&nbsp; Contains all parts (bus drives, walks, changes of buses) of the jourey.<br />
&emsp;&nbsp; Each element is a **trip object** of the 3 types: **PublicTransportTrip**, **IndividualTrip**, **TripChange**<br />
&emsp;&nbsp; See [trip object](#trip-object)<br /><br />

### { Trip Object }
&emsp;Describes a part of a journey.<br />
- ["PublicTransportTrip"](#publictransporttrip) describes a bus drive on one line.
- ["IndividualTrip"](#individualtrip) describes walking. For example from one bus stop to another.
- ["TripChange"](#tripchange) describes the changing the bus line at a bus station **?**

#### &emsp;{PublicTransportTrip}
&emsp;&emsp;**`type`:** **"PublicTransportTrip"** <br /><br />
&emsp;&emsp;**`modalType`:** **"bus"** <br /><br />
&emsp;&emsp;**`uuid`: _string_** <br />
&emsp;&emsp;&nbsp;uuid of joureny + trip. See [uuids](#uuids) <br /><br />
&emsp;&emsp;**`start`: _prediction object_ {** .. **}** <br />
&emsp;&emsp;&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
&emsp;&emsp;**`end`: _prediction object_ {** .. **}** <br />
&emsp;&emsp;&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
&emsp;&emsp;**`durationInS`: _int_** <br /><br />
&emsp;&emsp;**`lengthInM`: _int_** <br />
&emsp;&emsp;&nbsp;Seems to be always 0 for **PublicTransportTrip** <br /><br />
&emsp;&emsp;**`messageList`: []** <br />
&emsp;&emsp;&nbsp;I've only seen this array empty<br /><br />
&emsp;&emsp;**`tripId`: _int_** <br />
&emsp;&emsp;&nbsp;uniqe number from uuid. See [uuids](#uuids)<br /><br />
&emsp;&emsp;**`destinationName`: _string_** <br /><br />
&emsp;&emsp;**`destinationText`: _string_** <br />
&emsp;&emsp;&nbsp;Often the same as `destinationName`<br /><br />
&emsp;&emsp;**`isSaveConnection`: _bool_** <br /><br />
&emsp;&emsp;**`lineId`: _int_** <br /><br />
&emsp;&emsp;**`lineName`: _string_** <br />
&emsp;&emsp;&nbsp;often same as `lineId` <br /><br />
&emsp;&emsp;**`vehicleId`: _int_** <br /><br />
&emsp;&emsp;**`isLowFloorVehicle`: _bool_** <br /><br />
&emsp;&emsp;**`isAccessible`: _bool_** <br /><br />
&emsp;&emsp;**`haltCount`: _int_** <br /><br />

#### &emsp;{IndividualTrip}
&emsp;&emsp;**`type`:** **"IndividualTrip"** <br /><br />
&emsp;&emsp;**`modalType`:** **"walk"** <br /><br />
&emsp;&emsp;**`uuid`: _string_** <br />
&emsp;&emsp;&nbsp;uuid of joureny + trip. See [uuids](#uuids) <br /><br />
&emsp;&emsp;**`start`: _prediction object_ {** .. **}** <br />
&emsp;&emsp;&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
&emsp;&emsp;**`end`: _prediction object_ {** .. **}** <br />
&emsp;&emsp;&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
&emsp;&emsp;**`durationInS`: _int_** <br /><br />
&emsp;&emsp;**`lengthInM`: _int_** <br /><br />
&emsp;&emsp;**`messageList`: []** <br />
&emsp;&emsp;&nbsp;I've only seen this array empty<br /><br />
&emsp;&emsp;**`isAccessible`: _bool_** <br /><br />


#### &emsp;{TripChange}
&emsp;&emsp;**`type`:** **"TripChange"** <br /><br />
&emsp;&emsp;**`durationInS`: _int_** <br />
&emsp;&emsp;&nbsp;Time to wait between buses. I guess :D <br /><br />
&emsp;&emsp;**`source`: _string_** <br />
&emsp;&emsp;&nbsp;uuid of incoming/prev. **trip object**. See [uuids](#uuids) <br /><br />
&emsp;&emsp;**`target`: _string_** <br />
&emsp;&emsp;&nbsp;uuid of outgoing/next **trip object**. See [uuids](#uuids) <br /><br />

### { Prediction Object }
&emsp;**`type`: _string_** <br />
&emsp;&nbsp;I've only seen "Prediction" <br /><br />
&emsp;**`location`: _location object_** **{** ... **}** <br />
&emsp;&nbsp;A **location object**. See [location object](#location-object)<br /><br />
&emsp;**`visitNumber`: _int_** <br />
&emsp;&nbsp;Don't know what this is <br /><br />
&emsp;**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
&emsp;**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
