## Overview
Slate's BlogPost endpoint allows you to manipulate the BlogPost object.

## Fields

Field                | Type        | Required?    | Notes
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



## Create blog post
`POST /blog/create`

##  Get one blog post
`GET /blog/[blog_handle]`

## Delete blog post
`POST /blog/[blog_handle]/delete`