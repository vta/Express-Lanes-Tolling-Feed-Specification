# Managed and Tolled Lanes Feed Specification (MTLFS)
This document explains the types of files and data that comprise the Managed and Tolled Lanes Feed Specification (MTLFS) and defines the fields used in all of those files.

## Table of Contents
* [Files](#files)


## Files
This specification defines the following files along with their associated content:

File Name                   | Required      | Defines
--------------------------- | ------------  | ----------
MTLFS.json                  | Optional      | Auto-discovery file that links to all of the other files published by the system. This file is optional, but highly recommended.
general_toll_info.json      | Yes           | Describes toll payment methods, min and max tolls, and restrictions
toll_destination.json       | Yes           | Describes entrances and exits to the facility
toll_facility.json          | Optional      | Describes the lane types of the facility
toll_periods.json           | Optional      | Describes the name and operational dates and times of the facilities
toll_signs.json             | Optional      | Describes the regions the system is broken up into
toll_authority_info.json    | Yes           | Describes the system including System operator, URLs, contact info, time zone

### toll_authority_info.json
Describes the system including System operator, URLs, contact info, time zone.  A JSON array of hours defined as follows:

Field Name          | Required    | Defines
--------------------| ------------| ----------
agency_id        | Yes         | 
agency_name        | Yes         | 
agency_url              | Yes         | 
agency_timezone        | Yes         | 
agency_lang          | Yes         | 
agency_phone        | Yes         | 
toll_program        | Optional         | 
toll_program_shortname        | Optional         | 
toll_program_url        | Optional         | 
toll_operator        | Optional         | 
toll_authority        | Optional         | 

Example:
```json
{
  "agency_id": "VTA",
  "agency_name": "Santa Clara Valley Transportation Authority",
  "agency_url": "http://www.vta.org",
  "agency_timezone": "America/Los_Angeles",
  "agency_lang": "EN",
  "agency_phone": "408-321-2300",
  "toll_program": "Silicon Valley Express Lanes",
  "toll_program_shortname": "SVEL",
  "toll_program_url": "http://www.vta.org/getting-around/using-express-lanes",
  "toll_operator": "VTA",
  "toll_authority": "BATA"
}
```

### toll_destination.json
Describes entrances and exits to the facility

Field Name          | Required    | Defines
--------------------| ------------| ----------
facility_id        | Yes         | 
destination_id        | Yes         | 
agency_url              | Yes         | 
CTOC_Entry_Plaza_ID        | Yes         | 
CTOC_Exit_Plaza_ID          | Yes         | 
toll_destination        | Yes         | 
destination_description        | Optional         | 
destination_type        | Optional         | 

Example:
```json

[{
 "facility_id": "CLW",
 "destination_id": "FSW", 
 "CTOC_Entry_Plaza_ID": "5110",
 "CTOC_Exit_Plaza_ID": "5111",
 "toll_destination": "North First St",
 "destination_description": "North First St, San Jose, CA",
 "destination_type": "Freeway"
},
{
 "facility_id": "FSE",
 "destination_id": "CLE", 
 "CTOC_Entry_Plaza_ID": "5118",
 "CTOC_Exit_Plaza_ID": "5119",
 "toll_destination": "I-880 North bound",
 "destination_description": "I-880 NB, Milpitas, CA",
 "destination_type": "Freeway"
}]
```

### general_toll_info.json
Describes the system including System operator, URLs, contact info, time zone.  A JSON array of hours defined as follows:

Field Name          | Required    | Defines
--------------------| ------------| ----------
tolled_vehicles        | Yes         | 
tolling_methods        | Yes         | 
payment_options              | Yes         | 
toll_periods        | Yes         | 
minimum_toll          | Yes         | 
maximum_toll        | Yes         | 
toll_currency        | Optional         | 
toll_restrictions        | Optional         | 

Example:
```json
{
 "tolled_vehicles": "SOV",
 "tolling_methods": "transponder",
 "payment_options": "FasTrak",
 "toll_periods": "dynamic",
 "minimum_toll": "0.50",
 "maximum_toll": "7.00",
 "toll_currency": "USD",
 "toll_exemptions": [ "HOV2", "Motorbike", "transit", "greensticker", "whitesticker" ],
 "toll_restrictions": "none",
}
```

### toll_signs.json
Describes the system including System operator, URLs, contact info, time zone.  A JSON array of hours defined as follows:

Field Name          | Required    | Defines
--------------------| ------------| ----------
facility_id        | Yes         | 
sign_id        | Yes         | 
geometry              | Yes         | 
sign_type        | Yes         | 
toll_destination          | Yes         | 

Example:
```json
[{
 "facility_id": "CLW",
 "sign_id": "750",	 
 "geometry": {
	  "type": "Point",
	  "coordinates": [-121.92073, 37.44290]
	},
 "sign_type": ["Dynamic Toll Rate", "Dynamic Messages"],
 "toll_destination" : "North First St"
},
{
 "facility_id": "FSE",
 "sign_id": "250",	 
 "geometry": {
	  "type": "Point",
	  "coordinates": [-121.94227, 37.41967]
	},
 "sign_type": ["Dynamic Toll Rate","Dynamic Messages"],
 "toll_destination" : "I-880 NB"
}]
```


### toll_periods.json
Describes the name and operational dates and times of the facilities

Field Name          | Required    | Defines
--------------------| ------------| ----------
facility_id        | Yes         | 
name        | Yes         | 
hours_of_operation              | Yes         | 
direction        | Yes         | 
days_of_week          | Yes         | 
start_date        | Yes         | 
end_date          | Yes         | 


Example:
```json
[{
 "facility_id": "CLW",
 "name": "Calaveras Westbound",
 "hours_of_operation": [[0500, 1000], [1500, 1900]],
 "direction": "westbound",
 "days_of_week": "MTWRF",
 "start_date": "20120325",
 "end_date": "20500101"
},
{
 "facility_id": "FSE",
 "name": "First Street Eastbound",
 "hours_of_operation": [[0500, 0900], [1500, 1900]],
 "direction": "northbound",
 "days_of_week": "MTWRF",
 "start_date": "20120325",
 "end_date": "20500101"
}]
```
