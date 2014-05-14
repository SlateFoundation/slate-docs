## Overview
Slate's Courses endpoint allows you to create Course Sections.

##Fields

Field    			| Type		| Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
Title 				| varchar	| yes
Handle 			    | varchar	| yes
Code 			    | varchar	| yes
Status 			    | enum		| yes		| Hidden, Live, Deleted
Description		    | text		| no		|
Prerequisites		| text		| no
DepartmentID		| int		| no
