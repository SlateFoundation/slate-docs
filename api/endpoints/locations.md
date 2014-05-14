## Overview
Slate's Locations endpoint allows you to manipulate the locations object.

## Fields

Field                | Type		| Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
Title 				| varchar	| yes
Handle 			    | varchar	| no
Status 			    | enum		| no		| Hidden, Live, Deleted
Description		    | text		| no		|
ParentID		    | int		| no

## Relationships

Relationship     | Type      | Related Class              | Notes
---------------  | ----      | -----                      |
Parent           | one-one	 | Emergence\\Locations\\Location |

## Create locations
`POST /locations/create`

##  Get one location
`GET /locations/[location_handle]`

## Delete location
`POST /locations/[local_handle]/delete`