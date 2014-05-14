## Overview
Slate's Terms endpoint allows you to create terms.

## Fields

Field            	| Type		| Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
Title 				| varchar	| yes
Handle 			    | varchar	| yes
Status 			    | enum		| no		| Hidden, Live, Deleted
StarDate		    | date		| no		|
EndDate		        | date		| no
ParentID		    | int		| no

## Relationships

Relationship     | Type      | Related Class              | Notes
---------------  | ----      | -----                      |
Parent           | one-one	 | 

## Create term
`POST /terms/create`

##  Get one term
`GET /terms/[term_handle]`

## Delete term
`POST /terms/[term_handle]/delete`