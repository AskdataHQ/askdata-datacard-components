### **Feed message components**

A Smartfeed message is composed of the following components:

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16` `{ "stream":"", "topics":[ ], "text":"hi", "attachment":{ }, "quick_replies":[ ], "thread":"", "receiver":"", "sender":"0ee....", "time":153224343222`

The fields that contain the data to be shown are text, quick\_replies, attachment and sender (if message into chat view).

_Stream_

It is a label used to classify the messages. It’s possible to use every label you want excluded the reserved ones, as followed described:

*   _main_: is the default, if no stream wasn’t specified during creation of the messages, they’ll take this value;
    
*   _agent_: the default value for all messages that come from and are sent to the agent, in other words, the chat channel;
    
*   _\_feed/{{feedId}}_: is a dynamically resolved feed channel. All messages with this value belonging to the feed with given id {{feedId}};
    
*   _\_user/{{userId}}_: is a dynamic value resolved with the current user id. This classification is used to indicate the “inbox” channel.
    

  
_Thread_  
Is the id of message root of a discussion. If a user clicks on a card to show the details it’ll have the possibility to send messages to the agent regarding that specific card. All the messages exchanged with the agent after will belong to the same thread so their thread property will be valued with the root message id ([see the api](https://innaas.atlassian.net/wiki/spaces/A/pages/522256400/Comments "https://innaas.atlassian.net/wiki/spaces/A/pages/522256400/Comments"))

_Topic_

A topic is a label associated with the card; his format is “/type/code” and it comes from insight generation process. The type and code should be present in an ENTITY to permit to recognize the name of the topic self.  
For a card, it’s possible to give multiple topics. The user can pin a topic by clicking on the “Follow” button when the application shows it on the right side of the header. In this case, the name of the topic will be shown on the Channels menu. Of course, it’s possible to remove the pin by clicking on the topic in the channel and then by selecting the Unfollow button in the header bar.

_Attachment_

The following json is an example of attachment format:  
  

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46` `"attachment": { "id": "ACEA-best_kpi", "domain": "ACEA", "type": null, "topics": [ "/generale/best" ], "code": "ACEA-best_kpi", "hat": { "icon": "https://s3.eu-central-1.amazonaws.com/innaas.smartfeed/icons/acea/aceaico.png", "name": "Home", "sponsored": false, "action": "smartfeed://topic/generale/best" }, "header": { "icon": "https://s3.eu-central-1.amazonaws.com/innaas.smartfeed/icons/acea/home_blank.png", "title": "Best KPI", "notification": 0, "timestamp": 1527756898640, "action": "smartfeed://topic/generale/best", "action_label": "Mostra tutte" }, "body": [ { "component_type": "text", "details": { "text": "Il fatturato idrico cumulato ad aprile 2018 è in crescita del 10% rispetto all'anno precedente." } }, { "component_type": "cta", "details": { "link": "smartfeed://card/ACEA-fatturato_cumulato_aprile", "label": "Drill down per aziende" } } ], "footer": { "interaction": 0, "url": "smartfeed://card/best_kpi", "bookmark": { "count": 3, "bookmarked": true } } }`

The elements of an attachment are:

**Property name**

**Description**

**Mandatory**

**Property name**

**Description**

**Mandatory**

hat

It contains generic info relative to the card like name and sponsored info

false

header

It contains the _title_, _timestamp_ and _action_ info

false

body

It contains an array of components that populate the card

true

footer

It contains the number of interaction with the card, liking information and a sharing URL

false

_id_

the unique id of the message

true

_domain_

the domain which message belong to

true

_type_

type of the message

false

_code_

code of the message (part of ID)

true

_topics_

the topic list of the message

false