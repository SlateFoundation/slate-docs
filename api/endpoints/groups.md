## Overview
Slate's Groups endpoint allows you to manipulate the groups object.

## Fields

Field                | Type    	| Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
Name 				| varchar	| yes
ParentID 			| int	    | no
Founded 			| date		| no		| 
Data		        | text		| no		|
Status     		    | enum		| no		| Hidden, Live, Deleted

## Relationships

Relationship     | Type         | Related Class              | Notes
---------------  | ----         | -----                      |
Members          | one-many     |GroupMember  |
Parent           | one-one      |  |
People           | many-many    | Person  | LinkClass = GroupMember

## Create groups
`POST /groups/create`

##  Get one group
`GET /groups/[group_handle]`

## Delete group
`POST /groups/[group_handle]/delete`