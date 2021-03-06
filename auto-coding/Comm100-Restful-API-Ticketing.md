  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 4.0 | v4 | Ticketing Restful API | 2020-7-16 | Frank |  
 

# Parameter introduction 
- Incoming parameters:
    - Get API passes parameters through the query string 
    - Put/Post API passes parameters through json data. 
    - DateTime Parameters: 
        - All time parameters need to be entered in the standard format of <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO-8601</a>
- All time values are UTC time. The caller can convert to different time zones where needed. 

# Resource List 
|Name|EndPoint|Note| 
|---|---|---| 
|[Ticket](#tickets)| /ticketing/tickets| Tickets |  
|[RecycleBinTicket](#RecycleBinTicket)| /ticketing/recycleBinTickets| RecycleBin tickets |
|[Message](#message)| /ticketing/messages| Messages |  
|[View](#views)| /ticketing/views| Agent console views| 
|[Routing](#Routing)| /ticketing/routingConfig | Routing | 
|[AutoDistributionConfig](#AutoDistributionConfig)| /ticketing/autoDistributionConfig| Auto distributions | 
|[Trigger](#Triggers)| /ticketing/triggers| Triggers| 
|[SLAPolicy](#SLAPolicies)| /ticketing/SLAPolicies| SLA policies | 
|[WorkingHourConfig](#WorkingHour)| /ticketing/workingHourConfig| Work time | 
|[Holiday](#Holiday)| /ticketing/holidays| Holiday | 
|[Fields&Mapping](#fields&mapping)| /ticketing/fields| System fields and custom fields | 
|[BlockedEmailSender](#blockedemailsenders)| /ticketing/blockedEmailSenders| Blocked email, domain | 
|[Junk](#junks)| /ticketing/junks| Emails from blocked senders | 
|[ChannelAccount](#channel-accounts)| /ticketing/channelAccounts| Channel accounts |  

# Tickets 
## objects 
### ticket 
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | id of ticket | 
| `subject` | string | ticket subject | 
| `assigneeType` | string | `agent`, `bot` | 
| `assigneeId` | string | agent id, bot id | 
| `departmentAssigneeId` | string | department assignee id | 
| `priority` | string | `urgent`, `high`, `normal`, `low` | 
| `status` | string | `new`, `pendingInternal`, `pendingExternal`, `onHold`, `resolved` | 
| `contactOrVisitorType` | string | `contact`, `visitor` | 
| `contactOrVisitorId` | string | contact id, visitor id | 
| `hasDraft` | boolean | if has draft | 
| `mergedToTargetId` | int | merged ticket id | 
| `isReadByAgent` | boolean | if the ticket is read by agent | 
| `isReadByContact` | boolean | if the portal ticket is read by contact | 
| `createdById` | string | contact id, agent id, visitor id| 
| `createdByType` | string | `agent`, `contact`, `visitor` | 
| `createdTime` | datetime | create time of ticket | 
| `lastUpdatedTime` | datetime | last updated time of ticket | 
| `lastStatusChangedTime` | datetime | last status change time of ticket | 
| `lastRepliedTime` | datetime | last replied time | 
| `lastRepliedById` | string | last replied by id | 
| `lastRepliedByType` | string | `agent`, `contact`, `visitor`, `channelAccount`, `bot`|
| `resolvedById` | string | contact id, agent id| 
| `resolvedByType` | string | `agent`, `contact`, `system` | 
| `resolvedTime` | datetime | resolved time of ticket | 
| `firstMessageId` | string | the id of the first message | 
| `channelId` | string | the channel id of the first message | 
| `channelAccountId` | string | the channel account id of the first message | 
| `lastMessageId` | string | the id of the last message | 
| `lastMessageChannelId` | string | the channel id of the last message | 
| `lastMessageChannelAccountId` | string | the channel account id of the last message | 
| `totalReplies`| int | total replies number | 
| `firstRespondBreachTime` | datetime | Timestamp that denotes when the first response is due | 
| `nextRespondBreachTime` | datetime | Timestamp that denotes when the next response is due | 
| `resolveBreachTime` | datetime | Timestamp that denotes when the ticket is due to be resolved | 
| `isEditable`| boolean | if the current agent can update\reply the ticket | 
| `originalConversationId` | string | original id on social platform | 
| `isInRecycleBin` | boolean | is in recycle bin | 
| `customFields` | [custom field value](#custom-field-value)[] | custom field value array | 
| `mentionedAgents`|[mentioned agent](#mentioned-agent)[]| mentioned agents list | 
| `tagIds` | string[] | tag id array | 

### custom field value
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of custom field |
| `name` | string | the name of custom field |
| `value` | string | the value of custom field |

### custom field id and value
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of custom field |
| `value` | string | the value of custom field |

### mentioned agent 
| Name | Type | Description | 
| - | - | - | 
| `agentId` | string | the agent id of mentioned | 
| `isReadByAgent`| boolean | if the mentioned ticket is read | 
| `messageId`| string | message id| 

### message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `ticketId` | integer | id of ticket | 
| `body` | string | message text | 
| `type` | string | `text`, `html`,`audio`,`video`,`image`,`file`,`location`|
| `metadata` | string | json fomat, content of message |
| `parentId` | string | parent id |
| `originalId` | string | id in original channel |
| `time` | datetime | received time for incoming message, sent time for outgoing message | 
| `sentById`| string | id of agent, contact, visitor |
| `sentByType`| string | `agent`, `contact`, `system`, `bot`, `channelAccount`, `visitor` |  
| `attachments`| [attachment](#attachment)[] | attachment array |  
| `messageDelivery` | [messageDelivery](#messageDelivery) | message delivery info, only available for ougoing message |  

### messageDelivery
| Name | Type | Description | 
| - | - | - | 
| `messageId` | string | id of message | 
| `status` | string | send status：`waitForSending`,`sending`,`failed` | 
| `failReason` | string | fail reason | 

### note 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `ticketId` | integer | id of ticket | 
| `text` | string | note text | 
| `createdTime` | datetime | created time | 
| `sentById`| string | id of agent |
| `attachments`| [attachment](#attachment)[] | attachment array |  

### ticket draft 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message draft | 
| `ticketId` | integer | id of ticket |     
| `body` | string | draft body | 
| `metadata` | string | json of draft | 
| `lastUpdatedById`| string | id of agent| 
| `LastUpdatedTime` | datetime | the last updated time |
| `attachments`| [attachment](#attachment)[] | attachment array | 

 ### attachment 
| Name | Type | Description | 
| - | - | - |
| `id` | string | attachment unique id |  
| `fileKey` | string | file key |  
| `name` | string | attachment file name| 
| `size` | int | size file name| 
| `url` | string | attachment download link |    

 ### event log
| Name | Type | Description | 
| - | - | - | 
| `id` | string | event log id | 
| `ticketId` | integer | id of ticket | 
| `text` | string | event log text | 
| `time` | datetime | event time | 

## endpoints 
|EndPoint|Note| 
|---|---|
| `get  /ticketing/tickets`  |  [List tickets](#List-tickets)  |
| `get  /ticketing/tickets/{id}` |  [Get a ticket](#Get-a-ticket)  |
| `post  /ticketing/tickets` | [Submit a new ticket](#Submit-a-new-ticket) |
| `put  /ticketing/tickets/{id}` | [Update a ticket ](#Update-a-ticket ) |
| `put  /ticketing/tickets/`  | [Batch update tickets](#Batch-update-tickets) |
| `post  /ticketing/tickets/{id}:read`  | [Mark a ticket as read](#Mark-a-ticket-as-read) |
| `post  /ticketing/tickets/{id}:unread`  | [Mark a ticket as unread ](#Mark-a-ticket-as-unread) |
| `post  /ticketing/tickets/{id}:merge` | [ Merge a ticket ](#Merge-a-ticket) |
| `get  /ticketing/tickets/unreadCount` | [List unread tickets number for views](#List-unread-tickets-number-for-views) |
| `delete  /ticketing/tickets/{id}` | [Delete a ticket ](#Delete-a-ticket ) |
| `delete  /ticketing/tickets`  | [Batch delete tickets ](#Batch-delete-tickets ) |
| `get  /ticketing/tickets/{id}/messages` | [List messages of a ticket](#List-messages-of-a-ticket) |
| `post  /ticketing/tickets/{id}/messages` | [Post a message](#Post-a-message) |
| `put  /ticketing/messages/{id}`  | [update a message](#update-a-message) |
| `get  /ticketing/messages/{id}`  | [Get a message](#Get-a-message) |
| `get  /ticketing/messages:identify`  | [Iditify a specific message by original Id and channel Id](#Iditify-a-specific-message-by-original-Id-and-channel-Id) |
| `post  /ticketing/messages/{id}:resend`  | [Resend a message](#Resend-a-message) |
| `get  /ticketing/tickets/{id}/draft`  | [Get a ticket draft ](#Get-a-ticket-draft) | 
| `post  /ticketing/tickets/{id}/draft`  | [Create a ticket draft ](#Create-a-ticket-draft) |
| `put  /ticketing/tickets/{id}/draft`  | [Update a ticket draft ](#Update-a-ticket-draft) |
| `delete  /ticketing/tickets/{id}/draft`  | [ Delete a ticket draft ](#Delete-a-ticket-draft) |
| `get  /ticketing/tickets/{id}/notes` | [List notes of a ticket](#List-notes-of-a-ticket) |
| `post  /ticketing/tickets/{id}/notes` | [ post a note](#Post-a-note) |
| `get  /ticketing/tickets/{id}/eventLogs` | [ List ticket event logs ](#List-ticket-event-logs) |

### List tickets 
`get  /ticketing/tickets` 
+ Each request returns a maximum of 50 tickets. 
+ Parameters 
    - viewId: string, view id
    - tagId: string, tag id
    - keywords: string
    - time: DateTime, last updated time, default search the last 90 days, format: `time=startTime, endTime` 
    - timeZoneOffset, float, time zone of your time parameters
    - pageIndex: integer, default 1
    - pageSize: integer, default 20, max value 50
    - sortBy: string, `nextSLABreach`, `lastReplyTime`, `lastUpdatedTime`, `priority`, `status` , default value: `lastUpdatedTime`
    - sortOrder: string, `ascending`, `descending`, default value: `descending`
    - contactOrVisitorId: string

+ Response 
    - tickets: [ticket](#tickets) list, 
    - total: integer, total number of tickets 
    - previousPage: string, next page uri, the first page return null. 
    - nextPage: string, the last page return null. 
+ Includes

    | Includes | Description |
    | - | - |
    | agentAssignee | `get  /ticketing/tickets?include=agentAssignee` |
    | departmentAssignee | `get  /ticketing/tickets?include=departmentAssignee` |
    | contactOrVisitor | `get  /ticketing/tickets?include=contactOrVisitor` |
    | createdBy | `get  /ticketing/tickets?include=createdBy` |
    | lastRepliedBy | `get  /ticketing/tickets?include=lastRepliedBy` | 
    | lastMessage | `get  /ticketing/tickets?include=lastMessage` |

### Get a ticket 
`get  /ticketing/tickets/{id}` 
+ Parameters 
    - id: integer, ticket  
+ Response 
    - [ticket](#ticket) 
+ Includes

    | Includes | Description |
    | - | - |
    | agentAssignee | `get  /ticketing/tickets/{id}?include=agentAssignee` |
    | departmentAssignee | `get  /ticketing/tickets/{id}?include=departmentAssignee` |
    | contactOrVisitor | `get  /ticketing/tickets/{id}?include=contactOrVisitor` |
    | createdBy | `get  /ticketing/tickets/{id}?include=createdBy` |
    | lastRepliedBy | `get  /ticketing/tickets/{id}?include=lastRepliedBy` |
    | messages | `get  /ticketing/tickets/{id}?include=messages` |
    | eventLogs | `get  /ticketing/tickets/{id}?include=eventLogs` |
    | lastMessage | `get  /ticketing/tickets/{id}?include=lastMessage` |
 
### Submit a new ticket
`post  /ticketing/tickets` 
- Parameters 
    - subject: string, ticket subject, required 
    - assigneeType: string, `agent`, `bot`
    - assigneeId: string, agent id, bot id
    - departmentAssigneeId: string, department id 
    - priority: string, `urgent`, `high`, `normal`, `low`, default value: `normal` 
    - status: string, `new`, `pendingInternal`, `pendingExternal`, `onHold`, `resolved`, default value: `new` 
    - channelId: string, the channel id of the first message,
    - channelAccount: string, the channel account id of the first message,
    - contactOrVisitorId: string,
    - contactOrVisitorType: string, `contact` or `visitor`
    - customFields: [custom field id and value](#custom-field-id-and-value)[], custom field value array
    - tagIds: string[], tag id array
    - messages: [message](#message)[], the first message of the ticket, option
        
+ Response 
    - [ticket](#tickets)


### Update a ticket 
`put  /ticketing/tickets/{id}` 
- Parameters 
    - id: integer, ticket id
    - subject: string, ticket subject
    - contactOrVisitorType: string, `contact`, `visitor`
    - contactOrVisitorId: integer, contact id, visitor id
    - assigneeType: string, `agent`, `bot`
    - assigneeId: string, bot, agent id
    - departmentAssigneeId: string, department id
    - priority: string, priority: `urgent`, `high`, `normal`, `low`
    - status: string, `new`, `pendingInternal`, `pendingExternal,`, `onHold`, `resolved`
    - isReadByAgent: boolean
    - customFields: [custom field id and value](#custom-field-id-and-value)[], custom field value array
    - tagIds: string[], tag id array
- Response 
    - [ticket](#ticket) 

### Batch update tickets
`put  /ticketing/tickets/` 
+ Parameters 
    - ids: integer[], ticket id array
    - status, string
    - priority, string
    - assignedType: string, `agent`, `bot`
    - assigneeId: string
    - departmentAssigneeId, string
    - isReadByAgent, boolean
    - isInRecycleBin, boolean
+ Response 
    - [ticket](#ticket) list 

### List ticket event logs
`get  /ticketing/tickets/{id}/eventLogs`
- Parameters 
    - id: integer, ticket id 
- Response 
    - [event log](#event-log)

### List messages of a ticket 
`get  /ticketing/tickets/{id}/messages` 
+ Parameters 
    - id: integer, ticket id 
+ Response 
    - [message](#message) list 
+ Includes

    | Includes | Description |
    | - | - |
    | sentBy | `get  /ticketing/tickets/{id}/messages?include=sentBy` | 

### Get a message 
`get  /ticketing/messages/{id}` 
+ Parameters 
    - id: string, message id
+ Response 
    - [message](#message)
+ Includes

    | Includes | Description |
    | - | - |
    | sentBy | `get  /ticketing/messages/{id}?include=sentBy` |

### Iditify a specific message by original Id and channel Id
`post  /ticketing/messages:identify` 
+ Parameters 
    - originalId: string
    - channelId: string
+ Response 
    - [message](#message)

### Post a message 
`post  /ticketing/tickets/{id}/messages` 
- Parameters  
    - type: string, required
    - body: string, required
    - metadata: string, json
    - parentId: string
    - sentByType: string, agent or contact
    - sentById: string, agent Id or contact Id
    - time: datetime
- Response 
    - [message](#message) 

### Update a message 
`get  /ticketing/messages/{id}` 
+ Parameters 
    - id: string, message id
    - metadata: string,
    - messageDelivery: [messageDelivery](#messageDelivery)
+ Response 
    - [message](#message)

### Resend a message 
`post  /ticketing/messages/{id}:resend` 
- Parameters  
    - id: string, message id, 
- Response 
    - [message](#message) 

### Reply bot response with an intent
`post  /ticketing/tickets/{id}/messages:botIntent`
- Parameters  
    - id: number, ticket id,
    - botId: string, bot id, required
    - intentId: string, bot intent id, required
    - metadata: string
- Response 
    - http status code

### Mark a ticket as read 
`post  /ticketing/tickets/{id}:read` 
+ Parameters 
    - id: integer, ticket id 
+ Response 
    - http status code

### Mark a ticket as unread 
`post  /ticketing/tickets/{id}:unread` 
+ Parameters 
    - id: integer, ticket id 
+ Response 
    - http status code

### Delete a ticket 
`delete  /ticketing/tickets/{id}` 
- Parameters 
    - id: integer, ticket id
- Response 
    - http status code 

### Get a ticket draft 
`get  /ticketing/tickets/{id}/draft/` 
- Parameters 
    - id: integer, ticket id 
- Response 
    - [ticket draft](#ticket-draft) 

### Create a ticket draft 
`post  /ticketing/tickets/{id}/draft` 
- Parameters 
    - [ticket draft](#ticket-draft) 
- Response 
    - [ticket draft](#ticket-draft) 

### Update a ticket draft 
`put  /ticketing/tickets/{id}/draft` 
- Parameters 
    - [ticket draft](#ticket-draft) 
- Response 
    - [ticket draft](#ticket-draft) 

### Delete a ticket draft 
`delete  /ticketing/tickets/{id}/draft` 
- Parameters 
    - id: integer, ticket id 
- Response 
    - http status code 

### List notes of a ticket 
`get  /ticketing/tickets/{id}/notes` 
+ Parameters 
    - id: integer, ticket id 
+ Response 
    - [note](#note) list 
+ Includes

    | Includes | Description |
    | - | - |
    | sentBy | `get  /ticketing/tickets/{id}/notes?include=sentBy` |

### Post a note 
`post  /ticketing/tickets/{id}/notes` 
- Parameters  
    - text: string, required
    - attachments, attachment[]
- Response 
    - [note](#note) 

### Merge a ticket 
`post  /ticketing/tickets/{id}:merge`
- Parameters 
    - id: integer, target ticket id, 
    - sourceId: integer, source ticket id 
- Response 
    - [ticket](#ticket) 

### List unread tickets number for views 
`get  /ticketing/tickets/unreadCount?viewIds={viewid1}&viewIds={viewid2}&viewIds={viewid3}`
- Parameters 
    - viewIds: view id array
    - timeZoneOffset: double
- Response 
    - allCount: integer, all unread ticket number. 
    - array including: 
        - viewId: string, view id 
        - unreadCount: integer, count unread tickets of a view 
        - unreadTicketIds: integer[],
        - unreadMentionedCount: integer, the number of tickets which is unread and mentioned to me 
        - unreadMentionedTicketIds: integer[]

# RecycleBinTicket

## endpoints 

|EndPoint|Note| 
|---|---|
| `get  /ticketing/recycleBinTickets/`  | [List recycleBin tickets ](#List-recycleBin-tickets ) |
| `get  /ticketing/recycleBinTickets/{id}`  | [Get a recycleBin ticket](#Get-a-recycleBin-ticket) |
| `get  /ticketing/recycleBinTickets/{id}/messages`  | [List messages of a recycleBin ticket](#List-messages-of-a-recycleBin-ticket) |
| `get  /ticketing/recycleBinTickets/{id}/notes`  | [List notes of a recycleBin ticket](#List-notes-of-a-recycleBin-ticket) |
| `get  /ticketing/recycleBinTickets/{id}/eventlogs`  | [List eventlogs of a recycleBin ticket](#List-eventlogs-of-a-recycleBin-ticket) |
| `delete  /ticketing/recycleBinTickets/{id}`  | [Delete a recycleBin ticket](#Delete-a-recycleBin-ticket) |
| `post  /ticketing/recycleBinTickets/{id}:restore `  | [Restore a recycleBin ticket](#Restore-a-recycleBin-ticket) |

### List recycleBin tickets 
`get  /ticketing/recycleBinTickets/` 
- Parameters 
    - keywords: string
    - pageIndex: integer
    - pageSize: integer, default 20, max value 50
    - time: default search the last 90 days, format: `time=startTime, endTime`
- Response 
    - recycleBinTickets: [ticket](#ticket) list 
    - total: integer, total number of tickets 
    - previousPage: string, next page uri, the first page return null. 
    - nextPage: string, the last page return null. 
- Includes

    | Includes | Description |
    | - | - |
    | agentAssignee | `get  /ticketing/recycleBinTickets?include=agentAssignee` |
    | departmentAssignee | `get  /ticketing/recycleBinTickets?include=departmentAssignee` |
    | contactOrVisitor | `get  /ticketing/recycleBinTickets?include=contactOrVisitor` |
    | createdBy | `get  /ticketing/recycleBinTickets?include=createdBy` |
    | lastRepliedBy | `get  /ticketing/recycleBinTickets?include=lastRepliedBy` | 
    | lastMessage | `get  /ticketing/recycleBinTickets?include=lastMessage` | 

### Get a recycleBin ticket 
`get  /ticketing/recycleBinTickets/{id}` 
- Parameters 
    - id: integer, ticket id 
- Response 
    - [ticket](#ticket) 
- Includes

    | Includes | Description |
    | - | - |
    | agentAssignee | `get  /ticketing/recycleBinTickets/{id}?include=agentAssignee` |
    | departmentAssignee | `get  /ticketing/recycleBinTickets/{id}?include=departmentAssignee` |
    | contactOrVisitor | `get  /ticketing/recycleBinTickets/{id}?include=contactOrVisitor` |
    | createdBy | `get  /ticketing/recycleBinTickets/{id}?include=createdBy` |
    | lastRepliedBy | `get  /ticketing/recycleBinTickets/{id}?include=lastRepliedBy` |
    | messages | `get  /ticketing/recycleBinTickets/{id}?include=messages` |
    | eventLogs | `get  /ticketing/recycleBinTickets/{id}?include=eventLogs` |

### List messages of a recycleBin ticket
`get  /ticketing/recycleBinTickets/{id}/messages` 
- Parameters 
    - id: integer, ticket id
- Response 
    - [message](#message) 
- Includes

    | Includes | Description |
    | - | - |
    | sentBy | `get  /ticketing/recycleBinTickets/{id}/messages?include=sentBy` |

### List notes of a recycleBin ticket
`get  /ticketing/recycleBinTickets/{id}/notes` 
- Parameters 
    - id: integer, ticket id
- Response 
    - [note](#note)  

 ### List eventlogs of a recycleBin ticket
`get  /ticketing/recycleBinTickets/{id}/eventlogs` 
- Parameters 
    - id: integer, ticket id
- Response 
    - [eventlog](#eventlog)  

### Delete a recycleBin ticket 
`delete  /ticketing/recycleBinTickets/{id}` 
- Parameters 
    - id: integer, ticket id 
- Response 
    - http status code 

### Restore a recycleBin ticket 
`post  /ticketing/recycleBinTickets/{id}:restore ` 
- Parameters 
    - id: integer, ticket id 
- Response 
    - [ticket](#ticket)  

# Views 
## objects 
### view 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | view id | 
| `name` | string | view name | 
| `isPrivate` | boolean | if private view| 
| `conditionMetType` | string | condition met type | 
| `logicalExpression` | string | logical expression | 
| `conditions` | [conditions](#condition) | condition array | 
| `createdById` | string | agent id |  

### condition
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the condition | 
| `fieldName` | string | field name | 
| `operator` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
| `value` | string | condition value | 
| `order` | integer | order number | 

## endpoints 
### List views 
`get  /ticketing/views`
- Parameters 
    - no parameters 
- Response 
    - [view](#view) list

### Create a new view 
`post  /ticketing/views`
- Parameters 
    - name: string, view name, required 
    - isPrivate: boolean, if private view, default value: `false` 
    - conditionMetType: string
    - logicalExpression: string
    - conditions: [conditions](#condition), view conditions
- Response 
    - [view](#view) list 

### Get a view and its conditions 
`get  /ticketing/views/{id}` 
- Parameters 
    - id: string, view id 
- Response 
    - [view](#view) 

### Update a view 
`put  /ticketing/views/{id}` 
- Parameters 
    - id: string, view id 
    - name: string, view name, required 
    - isPrivate: boolean, if private view 
    - conditionMetType: string
    - logicalExpression: string
    - conditions: [conditions](#condition)
- Response 
    - [view](#view) 

### Delete a view 
`delete  /ticketing/views/{id}` 
- Parameters 
    - id: string, view id 
- Response 
    - http status code 


# Routing
## objects
### routingConfig
| Name | Type | Description |
| - | - | - |
| `isEnabled` | boolean | whether the routing is enabled or not.
| `type` |string | the type of routing, including `simple`and `routingRules`. |
| `routeTypeForSimpleRouting` | string | the rule of route ,including `department` and `agent` |
| `routeToAgentIdForSimpleRouting` | string | route to agent id |
| `routeToDepartmentIdForSimpleRouting` | string | route to department id |
| `priorityForSimpleRouting` | string | `urgent`, `high`, `normal`, `low` |
| `percentageToBotWhenOnline` | integer | Percentage of new ticket to bot when agents are online when simple routing |
| `percentageToBotWhenOffline` | integer | Percentage of new ticket to bot when agents are offline when simple routing |
| `routingRules` | [routingRule](#routingRule)[] | an array of [routingRule](#routingRule) json object. |
| `routeToTypeWhenNoRuleMatched` | string | the rule of failed route  including `department` and `agent` |
| `routeToAgentIdWhenNoRuleMatched` | string | match failed route to agent id |
| `RouteToDepartmentIdWhenNoRuleMatched` | string | match failed route to department id |
| `priorityWhenNoRuleMatched` | string | `urgent`, `high`, `normal`, `low` |
| `percentageToBotWhenOnlineWhenNoRuleMatched` | integer | Percentage of new ticket to bot when agents are online when match failed |
| `percentageToBotWhenOfflineWhenNoRuleMatched` | integer | Percentage of new ticket to bot when agents are offline when match failed |

### routingRule
| Name | Type | Description |
| - | - | - |
| `id` | string | id of the routing rule |
| `isEnabled` | boolean | whether the routing rule is enabled or not. |
| `name` | string | name of the routing rule |
| `conditionMetType` | string | `any`,`all`,`logicalExpression` |
| `logicalExpression` | string | logical expression |
| `conditions` | [conditions](#condition)  | an trigger condition json object. |
| `routeToType` | string | type of the route, including `agent` and `department`, value `department` is available when config of department is open. 
| `routeToAgentId` | string | route to agent id  |
| `routeToDepartmentId` | string | route to department id |
| `priority` | string | ticket priority enum number|
| `percentageToBotWhenOnline` | integer | Percentage of new ticket to bot when agents are online |
| `percentageToBotWhenOffline` | integer | Percentage of new ticket to bot when agents are offline |
| `order` | integer | order of the routing rule |

## endpoints
### get routingConfig
`get  /ticketing/routingConfig`
+ Parameters
    - no parameters
+ Response
    - [routingConfig](#routingConfig)

### Update routing
`put  /ticketing/routingConfig`
+ Parameters
    - isEnabled: boolean
    - type: string, `simple`, `routingRules`
    - routeTypeForSimpleRouting: string, department and agent
    - routeToAgentIdForSimpleRouting: string, simple route to agent id
    - routeToDepartmentIdForSimpleRouting, string, simple route to department id
    - percentageToBotWhenOnline: integer
    - percentageToBotWhenOffline: integer
    - priorityForSimpleRouting: string,
    - routeToTypeWhenNoRuleMatched: string, department and agent
    - routeToAgentIdWhenNoRuleMatched: string
    - RouteToDepartmentIdWhenNoRuleMatched: string
    - priorityWhenNoRuleMatched: string
    - percentageToBotWhenOnlineWhenNoRuleMatched: integer
    - percentageToBotWhenOfflineWhenNoRuleMatched: integer 
+ Response
    - [routingConfig](#routingConfig)

### Enable routing
`post  /ticketing/routingConfig:enable`
+ Parameters
    - no parameters
+ Response
    - [routingConfig](#routingConfig)

### Disable routing
`post  /ticketing/routingConfig:disable`
+ Parameters
    - no parameters
+ Response
    - [routingConfig](#routingConfig)

### Get a routing rule
`get  /ticketing/routingRules/{id}`
+ Parameters
    - id: string
+ Response
    - [routingRule](#routingRule)

### Create a routing rule
`post  /ticketing/routingRules`
+ Parameters
    - routingRule: [routingRule](#routingRule)
+ Response
    - [routingRule](#routingRule)

### Update a routing rule
`put  /ticketing/routingRules/{id}`
+ Parameters
    - routingRule: [routingRule](#routingRule)
+ Response
    - [routingRule](#routingRule)

### Enable a routing rule
`post  /ticketing/routingRules/{id}:enable`
+ Parameters
    - id: routing rule id
+ Response
    - [routingRule](#routingRule)

### Disable a routing rule
`post  /ticketing/routingRules/{id}:disable`
+ Parameters
    - id: routing rule id
+ Response
    - [routingRule](#routingRule)

### Delete a routing rule
`delete  /ticketing/routingRules/{id}`
+ Parameters
    - id: string
+ Response
    - http status code

# AutoDistributions
## objects
### autoDistributionConfig
| Name | Type | Description | 
| - | - | - | 
| `isEnabled` | boolean | if enabled Auto Distribution |
| `autoDistributionMethod`| string | `loadBalancing`, `roundRobin` |
| `isLastAssignedAgentPreferred`| boolean | prefer to allocate to the last assignee |
| `ifLimitMaxTicketsForAllAgents` | boolean | if set maximum number of tickets an agent can be allocated to |
| `maxTicketsForAllAgents` | integer | maximum number of tickets all agents can be allocated to |
| `ifExcludePendingExternalFromAgentMaxTicketCount` | boolean | if exclude `Pending External` status while count an agent's tickets number |
| `ifExcludeOnHoldFromAgentMaxTicketCount` | boolean | if exclude `On Hold` status while count an agent's tickets number |
| `agentAutoDistributions` | [agentAutoDistribution](#agentAutoDistribution)[] | agent preference for distribution |
| `departmentAutoDistributions`| [departmentAutoDistribution](#departmentAutoDistribution)[] | array of department distribution rules |

### departmentAutoDistribution
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | string | department id |
| `autoDistributionMethod`| string | `loadBalancing`, `roundRobin` |
| `isLastAssignedAgentPreferred` | boolean | prefer to allocate to the last assignee |

### agentAutoDistribution
| Name | Type | Description | 
| - | - | - | 
| `agentId` | string | agent id |
| `maxTickets` | integer | the maximum number of the tickets a agent can accept at the same time |
| `ifParticipateInAutoDistribution` | boolean | if the agent participate in auto distribution |

## endpoints
### Get auto distribution config
`get  /ticketing/autoDistributionConfig`
+ Parameters
    - no parameters
+ Response
    - [autoDistributionConfig](#autoDistributionConfig)

### Update auto distribution config
`put  /ticketing/autoDistributionConfig`
+ Parameters
     - [autoDistributionConfig](#autoDistributionConfig)
+ Response
    - [autoDistributionConfig](#autoDistributionConfig)

### Enable auto distribution
`post  /ticketing/autoDistributionConfig:enable`
+ Parameters
     - no parameters
+ Response
    - [autoDistributionConfig](#autoDistributionConfig)

### Disable auto distribution
`post  /ticketing/autoDistributionConfig:disable`
+ Parameters
     - no parameters
+ Response
    - [autoDistributionConfig](#autoDistributionConfig)

# Triggers
## object
### trigger
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the trigger |
| `name` | string | name of the trigger |
| `description` | string | description of the trigger |
| `isEnabled` | boolean | if enabled the trigger |
| `order` | integer | trigger execute and display order |
| `event` | string |  `whenTicketIsCreated`, `whenATicketReplyIsReceived`, `whenAnAgentReplied`, `whenTheAssigneeOfATicketHasChanged`, `whenTheStatusOfATicketHasChanged`, ` whenATicketStatusStaysTheSameForASpecifiedPeriodOfTime` |
| `status` | string | ticket status |
| `statusDuration` | string | ticket status duration |
| `isValueSettingEnabled` | boolean | if set value |
| `triggerActionUpdateField` | [triggerActionUpdateField](#triggerActionUpdateField)[] | auto update field value |
| `ifSendEmail` | boolean | if send email |
| `ifSendEmailToContacts` | boolean | if send email to contacts|
| `ifSendEmailToAgents` | boolean | if send email to agents |
| `conditionMetType` | string | `any`,`all`,`logicalExpression` |
| `logicalExpression` | string | logical expression |
| `triggerConditions` | [triggerConditions](#condition) | trigger conditions | 
| `triggerActionAgentRecipient` | string[] | agent id array of recipient |
| `triggerActionEmailContent` | [triggerActionEmailContent](#triggerActionEmailContent)[] | |


### triggerActionEmailContent
| Name | Type | Description | 
| - | - | - | 
| `subject` | string | subject of the email content |
| `htmlBody` | string | html body |
| `textBody` | string | plain text |

### triggerActionUpdateField
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the autoUpdate |
| `fieldId` | string | field id | 
| `value` | string | condition value | 

## endpoints
### List all triggers
`get  /ticketing/triggers`
+ Parameters 
    - no parameters
+ Response
    - [trigger](#trigger) list

### Get a trigger
`get  /ticketing/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - [trigger](#trigger)

### Submit a trigger
`post  /ticketing/triggers`
+ Parameters
    -[trigger](#trigger)
+ Response
    - [trigger](#trigger)

 ### Update a trigger
`put  /ticketing/triggers/{id}`
+ Parameters
    -[trigger](#trigger)
+ Response
    - [trigger](#trigger)

### Enable a trigger
`post  /ticketing/triggers/{id}:enable`
+ Parameters
    - id: trigger id
+ Response
    - [trigger](#trigger)   

### Disable a trigger
`post  /ticketing/triggers/{id}:disable`
+ Parameters
    - id: trigger id
+ Response
    - [trigger](#trigger)  

 ### Delete a trigger
`delete  /ticketing/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - http status code

# SLAPolicies
## objects
### SLAPolicy
| Name | Type | Description | 
| - | - | - | 
| `id` | string | SLA policy id |
| `isEnabled` | boolean | if enabled this SLA policy |
| `firstRespond` | integer | |
| `nextRespond` | integer | |
| `resolution` | integer | |
| `operationalHours`| boolean | if `businessHours`, `calenderHours` |
| `conditionMetType` | string | `any`,`all`,`logicalExpression` |
| `logicalExpression` | string | logical expression |
| `slaPolicyCondition` | [conditions](#condition) | conditions | 
| `order` | integer | SLA execute and display order |

## endpoints
### List all SLA policies
`get  /ticketing/SlaPolicies`
+ Parameters
    - no parameters
+ Response
    - [SLAPolicy](#SLApolicy) list

### Get a SLA policy
`get  /ticketing/SlaPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - [SLAPolicy](#SLApolicy)

### Create a SLA policy
`post  /ticketing/SlaPolicies`
+ Parameters
    - isEnabled: boolean, if enabled this SLA policy 
    - firstRespond: integer, 
    - nextRespond: integer, 
    - resolution: integer, 
    - operationalHours: boolean, `businessHours`, `calenderHours` 
    - conditionMetType: string
    - logicalExpression
    - slaPolicyCondition: [conditions](#condition)
+ Response
    - [SLAPolicy](#SLApolicy)

### Update a SLA policy
`put  /ticketing/SlaPolicies/{id}`
+ Parameters
    - id: string, SLA policy id 
    - isEnabled: boolean, if enabled this SLA policy 
    - firstRespond: integer, 
    - nextRespond: integer, 
    - resolution: integer, 
    - operationalHours: boolean, `businessHours`, `calenderHours` 
    - conditionMetType: string,
    - logicalExpression: string,
    - slaPolicyCondition: [conditions](#condition)
+ Response
    - [SLAPolicy](#SLApolicy)

### Enable a SLA policy
`post  /ticketing/SlaPolicies/{id}:enable`
+ Parameters
    - id: string, SLA policy id 
+ Response
    - [SLAPolicy](#SLApolicy)

### Disable a SLA policy
`post  /ticketing/SlaPolicies/{id}:disable`
+ Parameters
    - id: string, SLA policy id 
+ Response
    - [SLAPolicy](#SLApolicy)

### Delete a SLA policy
`delete  /ticketing/SlaPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - http status code

# WorkingHour
## objects
### workingHoursConfig
| Name | Type | Description | 
| - | - | - | 
| `IfWorkOnSunday` | boolean |  |
| `IfWorkOnMonday` | boolean |  |
| `IfWorkOnTuesday` | boolean |  |
| `IfWorkOnWednesday` | boolean |  |
| `IfWorkOnThursday` | boolean |  |
| `IfWorkOnFriday` | boolean |  |
| `IfWorkOnSaturday` | boolean |  |
| `SundayStartTime` | time |  | 
| `SundayEndTime` | time |  |
| `MondayStartTime` | time |  | 
| `MondayEndTime` | time |  |
| `TuesdayStartTime` | time |  | 
| `TuesdayEndTime` | time |  |
| `WednesdayStartTime` | time |  | 
| `WedesdayEndTime` | time |  |
| `ThursdayStartTime` | time |  | 
| `ThursdayEndTime` | time |  |
| `FridayStartTime` | time |  | 
| `FridayEndTime` | time |  |
| `SaturdayStartTime` | time |  | 
| `SaturdayEndTime` | time |  |

## endpoints
### Get working hour config
`get  /ticketing/workingHoursConfig`
+ Parameters
    - no parameters
+ Response
    - [workingHour](#workingHour) list

### Update working hour config
`put  /ticketing/workingHoursConfig`
+ Parameters
    - workingHours: [workingHoursConfig](#workingHoursConfig)[]
+ Response
    - http status code

# Holiday
## objects
### holiday
| Name | Type | Description |
| - | - | - | 
| `id` | string | the id of the holiday |
| `title` | string | the title of the holiday  |
| `date` | date | the date of the holiday |

## endpoints
### List all holidays
`get  /ticketing/holidays`
+ Parameters
    - no parameters
+ Response
    - [holiday](#holiday) list

### Get a holiday
`get  /ticketing/holidays/{id}`
+ Parameters
    - id: string
+ Response
    - [holiday](#holiday)

### Create a holiday
`post  /ticketing/holidays`
+ Parameters
    - title: string, title of the holiday
    - date: date, date of the holiday
+ Response
    - [holiday](#holiday)

### Update a holiday
`put  /ticketing/holidays/{id}`
+ Parameters
    - id: string
    - title: string, title of the holiday
    - date: date, date of the holiday
+ Response
    - [holiday](#holiday)

### Delete a holiday
`delete  /ticketing/holidays`
+ Parameters
    - id: string
+ Response
    - http status code

# Fields&Mapping 
## objects 
### field 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | field id | 
| `type` | string | `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`, `operator`, `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department` |
| `name` | string | field name | 
| `isSystem` | boolean | if is system field | 
| `isRequired` | boolean | value if is required | 
| `defaultValue` | string | field default value | 
| `linkURL` | string | only available for `link` type fields | 
| `helpText` | string | field help text | 
| `length` | integer | field value max length | 
| `availableIn` | integer | Indicate system field is avalaible in which function. 0:`none`, 1:`triggerCondition`, 2:`view`, 4:`SLA`, 8:`routingRule`, 16:`macro`, 32:`triggerFieldSetup` | 
| `fieldOptions` | [field option](#fieldOption)[] | value option | 
| `fieldMapping` | [fieldMapping](#fieldMapping) | field mapping | 

### fieldOption 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | option id | 
| `name` | string | option name | 
| `value` | string | field value | 
| `order` | integer | option order | 

### fieldMapping
| Name | Type | Description | 
| - | - | - | 
| `fieldId` | string | field id | 
| `chatFieldId` | string | chat field id |
| `offlineMessageFieldId` | string | offline message field id |

## endpoints 
### List fields and their options 
`get  /ticketing/fields` 
+ Parameters
    - isSystem: boolean, if is system field, optional   
    - availableIn: string, `all`, `triggerCondition`, `view`, `SLA`, `routingRule`, `macro`, `triggerFieldSetup`
+ Response 
    - [field](#field) list 

### Get a field
`get  /ticketing/fields/{id}`
+ Parameters
    - id: string, field id
+ Response
    - [field](#field) 

### Create a custom field
`post  /ticketing/fields`
+ Parameters
    - type: string, requited
    - name: string, required, unique
    - isRequired: boolean, default `false`
    - defaultValue: string
    - linkURL: only available for `Link`
    - helpText: string
    - length: integer
    - fieldOptions: [field option](#fieldOption)[]`
    - fieldMapping: [fieldMapping](#fieldMapping) 
+ Response
    - [field](#field) 

### Update a field
`put  /ticketing/fields/{id}`
+ Parameters
    - name: string, unique
    - isRequired: boolean, default `false`
    - defaultValue: string
    - linkURL: only available for `Link`
    - helpText: string
    - length: integer
    - fieldOptions: [field option](#fieldOption)[]
    - fieldMapping: [fieldMapping](#fieldMapping) 
+ Response
    - [field](#field) 

### Delete a field
`delete  /ticketing/fields/{id}`
+ Parameters
    - id, string, field id 
+ Response
    - http status code

### Mapping fields
`put  /ticketing/fieldmappings`
+ Parameters
    - fieldMappings: [fieldMapping](#fieldMapping) list
+ Response
    - fieldMappings: [fieldMapping](#fieldMapping) list


# BlockedEmailSenders 
## objects 
### blocked email sender 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of blocked sender |
| `emailOrdomain` | string | email, domain | 
| `blockLevel` | string | `blockasJunk`, `reject` | 

## endpoints 
### List blocked email senders 
`get  /ticketing/blockedEmailSenders` 
+ Parameters 
    - pageIndex: integer
    - pageSize: integer
    - emailOrdomain: string, domain, email address 
+ Response 
    - [block sender](#blocked-email-sender) list 
    - total: integer
    - previousPage: string, next page uri, the first page return null
    - nextPage: string, the last page return null
### Get a blocked email sender
`get  /ticketing/blockedEmailSenders/{id}`
+ Parameters
    - id: string
+ Response
    - [block email sender](#blocked-email-sender) 

### Add/update a blocked email sender 
`put  /ticketing/blockedEmailSenders` 
+ Parameters 
    - `emailOrdomain`, string, domain, email address 
    - `blockLevel`, string,
+ Response 
    - [block email sender](#blocked-email-sender) 

### Remove a blocked email sender 
`delete  /ticketing/blockedEmailSenders/{id}` 
+ Parameters 
   - id: string
+ Response 
    - http status code

# Junks 
## objects 
### junk 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of junk |  
| `channelId`| string | channel id | 
| `body` | string | body | 
| `type` | string | type: `html` or `text` | 
| `metadata` | string | json format | 
| `isReadByAgent`| boolean | if read by agent |
| `sentById`| string | id of sent by |
| `sentByType`| string | type of sent by: `contact` |
| `Time` | datetime | the received time of the junk message | 

## endpoints 
### List junk
`get  /ticketing/junks` 
- Parameters 
    - keywords: string
    - pageIndex: integer
    - pageSize: integer, default 20, max value 50
    - time: default search the last 90 days, format: `time=startTime, endTime`
- Response 
    - junks: [junk](#junk) list 
    - total: integer
    - previousPage: string, next page uri, the first page return null
    - nextPage: string, the last page return null

+ Includes

    | Includes | Description |
    | - | - |
    | sentBy | `get  /ticketing/junks?include=sentBy` | 

### Get a junk 
`get  /ticketing/junks/{id}` 
- Parameters 
    - id: string, junk id 
- Response 
    - [junk](#junk) 

### Post a junk 
`post  /ticketing/junks/` 
- Parameters 
    - [junk](#junk) 
- Response 
    - [junk](#junk) 

### Update a junk 
`put  /ticketing/junks/{id}` 
- Parameters 
    - id: string, junk id 
    - isReadByAgent: boolean, 
- Response 
    - [junk](#junk) 

### Restore a junk to a ticket 
`post  /ticketing/junks/{id}:notJunk` 
- Parameters 
    - id: string, email id 
- Response 
    - [ticket](#ticket) 

### Delete a junk email 
`delete  /ticketing/junks/{id}` 
- Parameters 
    - id: string, junk email id 
- Response 
    - http status code 

# Channel Accounts 

## objects 

### channelAccount 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id | 
| `name` | string | account name |   
| `channelAppId` | string | app id |
| `accountOriginalId` | string | channel account original id |
| `isEnabled` | bool | if is enabled |
| `isDefault` | bool | if is default |
| `screenName` | bool | screen name |
| `avatarUrl` | bool | avatar Url |
| `isEnabledBot` | bool | if is enabled bot |
| `selectedBotId` | string | selected bot id |
| `percentageToBotWhenOnline` | integer | Percentage of new ticket to bot when agents are online |
| `percentageToBotWhenOffline` | integer | Percentage of new ticket to bot when agents are offline |
| `channelIds` | string[] | channel id array |

## endpoints 
### List channel accounts 
`get  /ticketing/channelAccounts` 
- Parameters
    - no parameters
- Response 
    - [channelAccount](#channelAccount)[] 

### Get channel account by id
`get  /ticketing/channelAccounts/{id}` 
- Parameters
    - id: string
- Response 
    - [channelAccount](#channelAccount) 

### Add a channel account 
`post  /ticketing/channelAccounts` 
- Parameters
    - channelAccount: [channelAccount](#channelAccount) 
- Response 
    - [channelAccount](#channelAccount)

### Update a channel account 
`put  /ticketing/channelAccounts/{id}` 
- Parameters
    - [channelAccount](#channelAccount)
- Response 
    - [channelAccount](#channelAccount)

### Enable bot for a channel account 
`post  /ticketing/channelAccounts/{id}:enableBot` 
- Parameters
    - string: channel account id
- Response 
    - [channelAccount](#channelAccount)

### Disable bot for a channel account 
`post  /ticketing/channelAccounts/{id}:disableBot` 
- Parameters
    - string: channel account id
- Response 
    - [channelAccount](#channelAccount)

### Delete a channel account 
`delete  /ticketing/channelAccounts/{id}` 
- Parameters
    - id: string,
- Response 
    - http status code

# Includes
- Following APIs can use `Includes` as parameters to get related objects.

    | Endpoints | Support including parameters |
    | - | - |
    | `get  /ticketing/tickets` | agentAssignee, departmentAssignee, contactOrVisitor, createdBy, lastRepliedBy, lastMessage |
    | `get  /ticketing/tickets/{id}` | agentAssignee, departmentAssignee, contactOrVisitor, createdBy, lastRepliedBy, messages, eventLogs |
    | `get  /ticketing/tickets/{id}/messages` | sentBy |
    | `get  /ticketing/recycleBinTickets` | agentAssignee, departmentAssignee, contactOrVisitor, createdBy, lastRepliedBy |
    | `get  /ticketing/recycleBinTickets/{id}` | agentAssignee, departmentAssignee, contactOrVisitor, createdBy, lastRepliedBy, messages |
    | `get  /ticketing/recycleBinTickets/{id}/messages` | sentBy |
    | `get  /ticketing/portalTickets/{id}` | contact, messages |
    | `get  /ticketing/portalTickets` | contact |
    | `get  /ticketing/portalTickets/{id}/messages` | sentBy | 
    | `get  /ticketing/junks/` | sentBy | 

- Sample:
    - request: `get  /ticketing/tickets/{id}?include=agentAssignee,createdBy,messages`
    - response: 