## Overview
Slate's Course Sections endpoint allows you to create Course Sections.

## Fields

Field           | Type      | Description
--------------- |           | -------------
CourseID        | int       | The ID of the course to which the section belongs,
Title           | varchar   | The title of the course section.
Handle          | varchar   | The handle that will be used in the course section URL
Code            | varchat   | Course code - eg. "bio101a" 
Status          | enum      | Hidden, Live, Deleted
Notes           | text      | Course section description or other notes
StudentsCapacity| int       | Maximum students allowed per course section.
TermID          | int       | The ID of the term to which this course section belongs.
ScheduleID      | int       |
LocationID      | int       |

## Relationships

Relationship     | Type      | Related Class                                | Notes
---------------  | ----      | -----                                        |
Course           | one-one   | Slate\\Courses\\Course                       |
Term             | one-one   | Slate\\Term                                  |
Schedule         | one-one   | Slate\\Courses\\Schedule                     |
Location         | one-one   | Emergence\\Locations\\Location               |
Participants     | many-many | Slate\\Courses\\SectionParticipant           |
Instructors      | many-many | Slate\\Courses\\SectionParticipant           |
Students         | many-many | Slate\\Courses\\SectionParticipant           |
CouMappingsrse   | many-many | Slate\Integrations\SynchronizationMapping    |


## Create course section
`POST /sections/create`

##  Get one course section
`GET /sections/[section_handle]`

## Delete course section
`POST /sections/[section_handle]/delete`