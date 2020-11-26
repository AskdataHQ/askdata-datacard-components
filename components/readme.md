## Feed 

Every feed has a configuration document stored into feed collection. 

The following extract contains the inclusion/exclusion logic used to determine if what messages must have to be considered in the feed retrieval. In the example, will be considered all messages that have stream with value: _feed/BA44E597, but not "agent".


```
"streams" : {
        "include" : [
            "_feed/BA44E597"
        ], 
        "exclude" : [
            "agent"
        ]
 },
"code" : "test1",
"published": true
```

In particular, that feed is public (cause of "published": true property) so its messages will be shown in the main feed.

Note: delete and update are available only to the owner of Feed