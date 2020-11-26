### Body components

The body is an array of components. Every component has a component\_type property that qualifies the component self and a detail list. This list is specific for different component\_type but the number and quality of custom details are fixed (except for not mandatory ones)

**text**

It prints a simple text into the card.

`1 2 3 4 5 6` `{ "component_type":"text", "details":{ "text":"Ci sono 1031 richieste di servizio IT con aging superiore a 30 giorni nel 2018." } }`

**image**

It prints an image addressed by resource field, alt\_text is used in those case when the resource field is not available.

example:

`1 2 3 4 5 6 7` `{ "component_type":"image", "details":{ "resource":"https://s3.eu-central-1.amazonaws.com/innaas.smartfeed/icons/isa/top11offensiveyoung.png", "alt_text":"Top 11 Young - Offensive Index" } }`

#### cta

It enables a button that prints the label fields. The action is a calling to the URL contained by the link field.

example:

`1 2 3 4 5 6 7` `{ "component_type":"cta", "details":{ "link":"smartfeed://card/ACEA-fatturato_cumulato_aprile", "label":"Drill down per aziende" } }`

#### comparison

It prints two pieces of information (item) at comparison. For each item it's possible to specify the following fields:

**Property name**

**Description**

**Mandatory**

**Possible values**

**Property name**

**Description**

**Mandatory**

**Possible values**

label

The label that will be printed in top of the item

false

value

The value of the item

true

format

The format of data, useful to presentation issue. If the value is _string_ the value must be printed as is, no transformation

true

string/numeric/currency/time

unit

The measuring unit

only for _currency_ and _time_ format

EUR (tri-letter ISO4217) for _currency_ unit / [Date Format](http://www.unicode.org/reports/tr35/tr35-31/tr35-dates.html#Date_Format_Patterns "http://www.unicode.org/reports/tr35/tr35-31/tr35-dates.html#Date_Format_Patterns")

markup

A simple indicator if the value is positive or not. If GOOD the value must be colored green, red in the other case

false

GOOD/BAD

description

The subtitle

false

example:

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21` `{ "component_type":"comparison", "details":{ "item_a":{ "label":"Fatturato ad aprile 2018", "value":"242,95 Mln €", "format":"string", "unit":"EUR", "markup":"GOOD", "description":"10% di incremento" }, "item_b":{ "label":"Previsione fatturato 2018", "value":"718,88 Mln €", "format":"string", "unit":"EUR", "markup":"BAD", "description":"2% sotto l'obiettivo" } } }`

#### container

It contains items

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15` `{ "component_type":"container", "details":{ "image":"https://s3.eu-central-1.amazonaws.com/innaas.smartfeed/icons-thumb-down@2x.png", "items":[ { "component_type":"item", "details":{ "title":"Incasso", "text":"Incasso previsto: 50.000,00 € -17.499,09 € al raggiungimento dell’obiettivo" } } ] } }`

**item**

The component prints a container item but it's possible to use it outside of a container

**Property name**

**Description**

**Mandatory**

**Property name**

**Description**

**Mandatory**

icon

Icon print on this left of the line

false

title

The label print after icon

true

description

Description before action

true

action

The measuring unit

Link and URL for an action

example:

`1 2 3 4 5 6 7 8 9 10 11 12` `{ "component_type":"item", "details":{ "icon": "https://s3.eu-central-1.amazonaws.com/innaas.smartfeed/icons/acea/its_blank.png", "title": "NUMERO INCIDENT", "description": "581", "action": { "label" : "show", "url" : "smartfeed://topic/its/workorder_incident" } } }`

**table**

It prints a table for which it's possible to specify the header columns and the row values. The maximum number of column is of max 3, but it possible to use 2 ones.

**Property name**

**Description**

**Widths with 2 or 3 columns**

**Text justification**

**Property name**

**Description**

**Widths with 2 or 3 columns**

**Text justification**

columns

Array of string

{4/7, 3/7}, {3/7, 2/7, 2/7}

{left, centered, right}

rows

String matrix

{4/7, 3/7}, {3/7, 2/7, 2/7}

{left, right}

The text will be truncated with ... at the end of the second line.  
example:

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22` `{ "component_type":"table", "details":{ "columns":[ "Oggetto", "Scadenza", "Stato" ], "rows":[ [ "N° fattura 1233143", "22.04.2018", "Non pagata +9000" ], [ "Anticipo Iva", "30.05.2018", "Non pagata -1000" ] ] } }`

**Horizontal Chart**

It prints a progress bar that represents the range between \[start, end\]. The value contains the percentage of progression and the bar must be colored until this value.

**Property name**

**Description**

**Type**

**Possible values**

**Property name**

**Description**

**Type**

**Possible values**

start

the start of the range

Numeric

0

end

the end of the range

Numeric

100

value

the value of the percentage

Numeric

45

example:

`1 2 3 4 5 6 7 8` `{ "component_type":"horizontal_chart", "details":{ "start":0, "end":45, "value":100 } }`

**map**

It prints a map according to the given coordinates.

**Property name**

**Description**

**Mandatory**

**Property name**

**Description**

**Mandatory**

center

lat and long of the map center

true

center\_on\_me

if true the map must be center of my current position, false otherwise

true

radius

the number of meters for radius

true

show\_my\_position

if true a pin on my position must be shown

true

points

list of lat and long for the different points to show

true

geo

geoJson coordinates

false

example:

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48` `{ "component_type":"map", "details":{ "center":{ "lat":"41.876471", "long":"12.465616" }, "center_on_me":false, "radius":1000, "show_my_position":false, "points":[ { "lat":"41.881789", "long":"12.467728" }, { "lat":"41.876346", "long":"12.465314" }, { "lat":"41.875301", "long":"12.465470" } ], "geojson":{ "features":[ { "geometry":{ "coordinates":[ 12.33845213, 45.43490485 ], "type":"Point" }, "properties":{ "__fillAlpha":0.5, "__fillColor":"#266ff2", "__radius":6.0, "__strokeColor":"#266FF2", "__strokeWidth":2.0, "some property":"value" }, "type":"Feature" } ] } } }`

_**geoJson**_ coordinates follow the geoJson standard format (please see [https://en.wikipedia.org/wiki/GeoJSON](https://en.wikipedia.org/wiki/GeoJSON "https://en.wikipedia.org/wiki/GeoJSON"))

It’s possible to use Point, LineStrig, Polygon,MultiPoint, MultiLineString, MultiPolygon andGeometryCollection features.

In the properties it’s possible to specify the value of custom property in order to show that in the tooltip when users will tap over the Feature.

Apart from custom properties, there are the styles one as visible into the example, their name are reserved

**Style property name**

**Description**

**Feature Type**

**Mandatory**

**Style property name**

**Description**

**Feature Type**

**Mandatory**

\_\_fillAlpha

the alpha factor for color

Point

true

\_\_fillColor

the main color

Point

true

\_\_radius

the size of element

Point

true

\_\_strokeWidth

how big is the border

Point

true

\_\_strokeColor

the color of the border

Point

true

  
**Message Visibility**

In the main view two particular feeds are available:

*   Home
    
*   Inbox
    

In the home, all the messages from the public feed are visualized together with those messages belong to the feed specified into _include_ strategy specified into FeedConfiguration.  
In the inbox all the messages that have been directed to the logged user.  
They are visible because of the owner is “agent”. So every feed with ownership of agent will be visible in the bar beside Home and Inbox.

A custom feed could be created by a user during the sharing rule process and by agent, when it connects a dataset. By default a “dataset” feed is public but a “user-defined” feed not, it is visible to the owner when he clicks on his channels.

Meteo and Sport are private channel

MYSQL is a public channel

It is possible to publish a user-defined feed changing the following property inside of feed collection:

`1` `"published":true`

By setting it to true the related highlight will be shown on the main page of the feed.

_What is visible in the main page of feed?_

The main feed returns all messages belonging to all feed created by the current user (check owner property in the related feed document), all those messages belonging the feeds marked as published and all messages whose stream is dynamically resolved through the inclusion/exclusion in the configuration of feed stored in the feed collection.

1.  get all messages of feeds I created (the owner in feed document contains my user id)
    
2.  get all messages of published feed (the feed of other users as well)
    
3.  get all messages with the stream is in the range of streams dynamically resolved in the feed home
    
4.  if nothing is retrieved all messages with “main” stream will be retrieved
    
5.  zero card is returned if no messages are found using the logic 1..4
    

Home and Inbox are two special kinds of feed always present by default. They are printed in the top of the main view because their owner is “agent”. So if you want to add a new feed in that bar the owner of this feed should be “agent”.

### **Suggestions**

…

### **Sharing rule**

…

### **Search**

The search is made possible through multiple instances of the ElasticSearch index.

For every index, there is a Searcher object responsible for searching, suggestions and in some case the indexing document.

**Index name**

**Description**

**ElasticSearch index name**

**Produce suggestions**

**Component**

**Index name**

**Description**

**ElasticSearch index name**

**Produce suggestions**

**Component**

Topic

It stores measure only

“feed\_index”

true

Entities

It contains the _title_, _timestamp_ and _action_ info

"state.smartbot.flatentity"

true

ElasticEntityMeasureSearcher

UserQuery

It contains all the queries made by users and it is interrogated to produce the “previous query” in the search item result

"events.smartbot.user\_query"

false

ChainSearcher:{  
ElasticUserQuerySearcher, ElasticDiscoveryQuerySearcher}

_For developers_

SearchConfiguration class is responsible for the building the Chain of the searcher used when a search is performed.  
ChainSearcher is a kind of searcher that contains different Searcher and executed.

_Search and Browse special item_

There are two special search result items with subtitle “Search” normally returned as the first result only when the user input is not empty. Clicking on it, it possible ask the given input directly to the agent.

The second is “Browse” of Question catalog that shows the list of Discovey entry in the same view. Note it appears in the first result position if the user hasn’t typed any text. In all the other case (when the results are returned) is returned on the last position.

_Search and Browse with no results_

_Browse in the last position_

_Suggestions_

The horizontal suggestions are suggested from search and they can contain measure and entities as shown in the figure:

_**Measures** suggested: total spend on pos, price_

_**Entity** suggested: restaurant, residentia-residential_

_Total spend on pos, price, waiters_ are some of the measures suggested automatically.

In particular, the horizontal suggestions come from the ElasticEntityMeasureSearcher executing the following logic:

1.  if the user input except spaces is empty it returns measures (case 1)
    
2.  if the user input has some tokens it returns a list of entities. If the last token is not empty it will use the _matchPhrasePrefixQuery_ operator (case 2)
    
3.  if the list of entities is empty it tries to return a list of ENTITY using _matchPhrasePrefixQuery_ operator.
    

Configuration
=============

### **Agent**

Every time an agent is being created a new configuration on feed is created as well. The configuration is present in feedConfiguration Mongo collection. The feedConfiguration document contains the property that customizes the behavior of that feed.

Property configuration

**Name**

**Description**

**Type**

**Name**

**Description**

**Type**

visible

If true, the agent can be accessed to everyone, anonymous included. Otherwise, the connection is possible only with a valid token. This property is automatically set by the system when the permission for anonymous users is being changed on the relative agent (see Kafka ShareAgentStream event streaming).

Boolean

InitCommand

If set, when a user asks the initial (empty) history of messages exchange with the agent, that text contained by this property is sent to the agent and so triggers a chat.

String

forYou

It true, the channel “For you” is enabled, which means that messages will be sent to it. What about its visibility depends on forYouHidden.

Boolean

forYouHidden

It false, the “For you” is enabled is visible In the list of channels seen by users.

Boolean

### **Feed**

Every feed has a configuration stored into feed collection. The following extract contains the inclusion/exclusion logic used to determine if what messages must have to be considered in the feed retrieval. In the example, will be considered all messages that have stream with value: \_feed/BA44E597, but not "agent".

`1 2 3 4 5 6 7 8 9 10 11 12` `... "streams" : { "include" : [ "_feed/BA44E597" ], "exclude" : [ "agent" ] }, "code" : "test1", "published": true ...`

In particular, that feed is public (cause of "published": true property) so its messages will be shown in the main feed.

Note: delete and update are available only to the owner of Feed