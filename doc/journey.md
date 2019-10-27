### journey
✖
#### query parameters
| key            | type                     | required | default | info |
|:---------------|:-------------------------|:---------|:--------|:-----|
| startStopId    | number (int)             | ✓        | -       | can be obtained by. e.g **instance** |
| endStopId      | number (int)             | ✓        | -       | an be obtained by. e.g **instance**  |
| departureTime  | number (timestamp)       | ✓        | -       | unix timestamp in _millisecounds !!!_ So timestamp * 1000 |
| arrivalTime    | number (timestamp)       | ✖ / ✓    | -       | Can be used istead of depatrureTime |
| minTimeChanges | number (int)             | ✖        | 2       | not sure of this has really an effect. Couldn't find a difference between default value and 0 |
| maxNumChanges  | number (int)             | ✖        | 8       | "    | 
| maxWaitingTime | number (int)             | ✖        | 90      | propably minutes. Not sure if just waiting time to the first bus or sum of all waiting times (when changing bus) |
| maxNumResults  | number (int)             | ✖        | 10      | -    |     

