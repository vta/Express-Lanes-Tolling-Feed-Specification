# Express-Lanes-Tolling-Feed-Specification

This document explains the types of files and data that comprise the Express Lanes Tolling Feed Specification (ELTFS) ("ELFS"? "TFS"?) and defines the fields used in all of those files.


## Live Toll Update format

The data sent and received to/from the API is sent as a JSON array of objects with each of the following fields being required in each object:

* **name** (string) is any string describing the location of the area. In the examples, CLW and FSW represent toll locations for "SR 237 West to Sunnyvale" and "I-880 North to Oakland", respectively. This field cannot be null.
* **time** (number|null) a number representing time as the number of milliseconds since 1 January 1970 00:00:00 UTC. This value can be null, but it is highly recommended to be populated, as this value allows clients to determine when the next update should occur.
* **price** (string|null) is the price
* **message** (string|null) is any arbitrary message to display

## Agency Definition
    Agency : String
    location :  [{lat,lng}]
    direction: [n|ne|e|se|s|sw|w|nw]
    active_hours_start: Date
    active_hours_end : Date
    type: bridge|express lane
