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



### JSON Response


**`type`: _string_** <br />
&nbsp;should be "JourneyResults" <br /><br />
**`searchQuery`:** {<br />
&emsp;&emsp;**`queryString`: _string_** <br />
&emsp;&emsp; full HTTP query string (with defaults)<br />
}<br /><br />
**`resultCount`: _int_** <br />
&nbsp;length of array `resultList` (see below)<br /><br />
**`maxJourneyDurationInS`: _int_** <br /><br />
**`resultList`:** []<br />
&nbsp;list of **journey objects**. See [journey object](#journey-object)<br /><br />

#### journey object
**`type`: _string_** <br />
&nbsp;should be "Journey"<br /><br />
**`mode`: _string_** <br />
&nbsp;I've only seen "Compact"<br /><br />
**`uuid`: _string_** <br />
&nbsp;list of all uuid's for this journey (only one if you dont have change buses)<br />
&nbsp;For structure of uuid's look at [uuids](#uuids)<br /><br />
**`status`: _string_** <br >
&nbsp;known values: ["OK", ]<br /><br />
**`messageList`: []** <br >
&nbsp;I've only seen this array empty<br /><br />
**`queryString`: _string_** <br >
&nbsp;same `queryString` as above<br /><br />
**`startTimeInUnixEpochMillis`: _int_** <br /><br />
**`endTimeInUnixEpochMillis`: _int_** <br /><br />
**`currentServerTimeInUnixEpochMillis `: _int_** <br /><br />
**`durationsInS`: {** <br />
&emsp;&emsp;**`bus`: _int_** <br />
&emsp;&emsp;**`walk`: _int_** <br />
&emsp;&emsp;**`total`: _int_** <br />
}<br /><br />
&emsp;**`distancesInM`: {** <br />
&emsp;&emsp;**`bus`: _int_** <br />
&emsp;&emsp;**`walk`: _int_** <br />
&emsp;&emsp;**`total`: _int_** <br />
}<br /><br />
**`startLocation`: _location object_** **{** ... **}** <br />
&nbsp;A **location object**. See [location object](#location-object)<br /><br />
**`endLocation`: _location object_** **{** ... **}** <br />
&nbsp;A **location object**. See [location object](#location-object)<br /><br />
**`elementCount`: _int_** <br />
&nbsp;number of elements in `elementList` which contains all bus lines<br /><br />
**`elementList`:** []<br />
&nbsp; Contains all parts (bus drives, walks, changes of buses) of the jourey.<br />
&nbsp; Each element is a **trip object** of the 3 types: **PublicTransportTrip**, **IndividualTrip**, **TripChange**<br />
&nbsp; See [trip object](#trip-object)<br /><br />

#### trip object
Describes a part of a journey.<br />
- ["PublicTransportTrip"](#publictransporttrip) describes a bus drive on one line.
- ["IndividualTrip"](#individualtrip) describes walking. For example from one bus stop to another.
- ["TripChange"](#tripchange) describes the changing the bus line at a bus station **?**

##### PublicTransportTrip
**`type`:** **"PublicTransportTrip"** <br /><br />
**`modalType`:** **"bus"** <br /><br />
**`uuid`: _string_** <br />
&nbsp;uuid of joureny + trip. See [uuids](#uuids) <br /><br />
**`start`: _prediction object_ {** .. **}** <br />
&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
**`end`: _prediction object_ {** .. **}** <br />
&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
**`durationInS`: _int_** <br /><br />
**`lengthInM`: _int_** <br />
&nbsp;Seems to be always 0 for **PublicTransportTrip** <br /><br />
**`messageList`: []** <br />
&nbsp;I've only seen this array empty<br /><br />
**`tripId`: _int_** <br />
&nbsp;uniqe number from uuid. See [uuids](#uuids)<br /><br />
**`destinationName`: _string_** <br /><br />
**`destinationText`: _string_** <br />
&nbsp;Often the same as `destinationName`<br /><br />
**`isSaveConnection`: _bool_** <br /><br />
**`lineId`: _int_** <br /><br />
**`lineName`: _string_** <br />
&nbsp;often same as `lineId` <br /><br />
**`vehicleId`: _int_** <br /><br />
**`isLowFloorVehicle`: _bool_** <br /><br />
**`isAccessible`: _bool_** <br /><br />
**`haltCount`: _int_** <br /><br />

##### IndividualTrip

**`type`:** **"IndividualTrip"** <br /><br />
**`modalType`:** **"walk"** <br /><br />
**`uuid`: _string_** <br />
&nbsp;uuid of joureny + trip. See [uuids](#uuids) <br /><br />
**`start`: _prediction object_ {** .. **}** <br />
&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
**`end`: _prediction object_ {** .. **}** <br />
&nbsp;A **prediction object**. See [prediction object](#prediction-object)<br /><br />
**`durationInS`: _int_** <br /><br />
**`lengthInM`: _int_** <br /><br />
**`messageList`: []** <br />
&nbsp;I've only seen this array empty<br /><br />
**`isAccessible`: _bool_** <br /><br />


##### TripChange

**`type`:** **"TripChange"** <br /><br />
**`durationInS`: _int_** <br />
&nbsp;Time to wait between buses. I guess :D <br /><br />
**`source`: _string_** <br />
&nbsp;uuid of incoming/prev. **trip object**. See [uuids](#uuids) <br /><br />
**`target`: _string_** <br />
&nbsp;uuid of outgoing/next **trip object**. See [uuids](#uuids) <br /><br />

#### Prediction Object

**`type`: _string_** <br />
&nbsp;I've only seen "Prediction" <br /><br />
**`location`: _location object_** **{** ... **}** <br />
&nbsp;A **location object**. See [location object](#location-object)<br /><br />
**`visitNumber`: _int_** <br />
&nbsp;Don't know what this is <br /><br />
**`estimatedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
**`estimatedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
**`aimedArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
**`aimedDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
**`scheduledArrivalInUnixEpochMillis`: _int_** unix timestamp in ms <br /><br />
**`scheduledDepartureInUnixEpochMillis`: _int_** unix timestamp in ms <br />
