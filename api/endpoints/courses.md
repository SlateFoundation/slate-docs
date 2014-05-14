## Overview
Slate's Courses endpoint allows you to create Courses.

## Fields

Field        		| Type		| Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
Title 				| varchar	| yes
Handle 			    | varchar	| yes
Code 			    | varchar	| yes
Status 			    | enum		| yes		| Hidden, Live, Deleted
Description		    | text		| no		|
Prerequisites		| text		| no
DepartmentID		| int		| no

## Relationships

Relationship     | Type      | Related Class              | Notes
---------------  | ----      | -----                      |
Department       | one-one	 | Slate\\Courses\\Department |
Sections	     | one-many  | Slate\\Courses\\Section	  |

## Create course
`POST /courses/create`

##  Get one course
`GET /courses/[course_handle]`

## Delete course
`POST /courses/[course_handle]/delete`