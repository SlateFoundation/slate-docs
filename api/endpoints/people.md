## Overview
Slate's People endpoint allows you to manipulate the Person object.

## Fields
Field           | Value Type            | Required? |   Description
--------------- | -------------         |   ------  | ---------------
ID              | int                   | Yes       | Person's ID.
FirstName       | varchar               | Yes       | Person's first name.
LastName        | varchar               | Yes       | Person's last name.
MiddleName      | varchar               | No        | Person's middle name.
Gender          | enum (Male, Female)   | No        | Person's gender.
BirthDate       | date                  | No        | Person's date of birth.
Location        | varchar               | No        | Person's address/zip
About           | text                  | No        | Person's description
PrimaryPhotoID  | int                   | No        |
PrimaryEmailID  | int                   | No        |
PrimaryPhoneID  | int                   | No        |
PrimaryPostalID | int                   | No        |

## Relationships

Field               | Type              | Related Class             | Notes
---------------     | -------------     | --------                  | --------
GroupMemberships    | one-many 		    | GroupMember 	            | indexField = GroupID foreign = PersonID
Notes			 	| context-children	| Person			        | order = array(‘ID’ => ‘DESC’)
Groups				| many-many		    | GroupMember	            | linkLocal - PersonID linkForeign - GroupID
PrimaryPhoto		| one-one			| PhotoMedia 		        | local - PrimaryPhotoID
Photos				| context-children	| PhotoMedia		        |
Comments			| context-children	| Comment		            | order = array(‘ID’ => ‘DESC’)
PrimaryEmail		| one-one			| \\Emergence\\People\\ContactPoint\\Email
PrimaryPhone		| one-one			| \\Emergence\\People\\ContactPoint\\Phone
PrimaryPostal		| one-one			| \\Emergence\\People\\ContactPoint\\Postal
ContactPoints		| one-many		    | ContactPoint
Relationship		| one-many		    | \\Emergence\\People\\Relationship

## Create
`POST /sections/create`

##  Get one person
`GET /people/[ID]`

## Delete 
`POST /people/[ID]/delete`