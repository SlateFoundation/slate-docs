## Overview
Slate's Pages endpoint allows you to manipulate the page object.

## Fields

Field                | Type        | Required?	| Notes
------------------  | --------	| --------	| ------
ID				    | int		| yes		|
ContextClass		| varchar	| no
ContextID 			| int	    | no
Title 		    	| varchar	| yes		| 
Handle		        | varchar	| yes		|
AuthorID         	| int		| no		| 
Status         	    | enum		| no		| Hidden, Live, Deleted
Published    	    | timestamp	| no		|
Visibility          | enum		| no		| Public, Private
LayoutClass         | enum		| no		| OneColumn
LayoutConfig        | text		| no		|



## Relationships

Relationship     | Type             | Related Class                     | Notes
---------------  | ----             | -----                             |
Context          | context-parent   |                                   |
GlobalHandle     | handle           |                                   |
Author           | one-one          | Person                            | 
Items            | many-many        | Emergence\CMS\Item\AbstractItem   | foreign - ContentID
Tags             | many-many        | Tag                               | linkClass - TagItem, linkLocal - ContextID
Comments         | context children | Comment                           | 



## Create page
`POST /pages/create`

##  Get one page
`GET /pages/[page_handle]`

## Delete page
`POST /pages/[page_handle]/delete`