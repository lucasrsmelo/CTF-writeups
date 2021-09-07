# Gang Busted

![gang_busted_description](https://user-images.githubusercontent.com/34749742/132276116-3c033395-d87e-4bca-aa04-abc244ab25a6.png)

Once I've downloaded and unzipped the archive, the main directory extracted was "data" and inside that I found this:

![Directories](https://user-images.githubusercontent.com/34749742/132276082-cb7f6e25-dab4-4b7a-9b2a-fd8e2d1bb00b.png)

When I listed the directory, I found that it was some acquired Android data.
Most of these directories were empty. To clean this, I ran the following command inside the "data" directory:

```bash
$ find . -empty -type d -delete
``` 
**This is a key point:** In Android filesystem, every application stores its data under the **/data/data** folder. Furthermore, Android uses SQLite to store most data (emails, text messages, etc).

According to the challenge description, we must find the social media platform that were used. In this case, the most likely platform is Skype:

<!---
COLOCAR A IMAGEM DO DIRETÓRIO AQUI, DESTACANDO O SKYPE
-->

It gives us the first part of the flag:
```
GrabCON{Skype_<email>_<group_name>_<member_name>}
```
Then, there's a directory called "databases" inside the skype folder. This is the place where the Skype data is stored.
Next steps, I used the **DB Browser for SQLite** to help me in the analysis.

<!---
COLOCAR IMAGEM DO DB BROWSER AQUI
-->

This tool is very straightforward. Just open the desired database and start the analysis.

After searching all those databases, the **s4l-live:.cid.6c41bc4408002e1f.db** was the very interesting.
To browse the tables, just click in the **Browse data** tab.
I browse all the tables and found some tables that caught my attention.
Then I selected the second row of the **conversationsv14** table and double-clicked the **nsp_data** column, which returns me the following:

```json
{
    "_forceToRecents": 0,
    "_isHighlight": 0,
    "_needsSync": 0,
    "conv": {
        "_convProps": {
            "color": "hsv_0.5723270440251572,1,212_0.5371900826446281,1,242_reverse",
            "consumptionhorizon": "1630472727022;1630473487204;16809682010359575515",
            "consumptionhorizonpublished": "1630472727022;1630473485571;16809682010359575515",
            "isemptyconversation": "False",
            "isfollowed": "False",
            "lastimreceivedtime": "2021-09-01T05:05:20.158Z"
        },
        "_forceSyncThreadDetails": false,
        "_searchTerms": "31337 Hax0r Plan 8:live:.cid.894d225aeeb5246d",
        "_threadMembers": [
            {
                "id": "8:live:.cid.894d225aeeb5246d",
                "role": "Admin"
            },
            {
                "id": "8:live:.cid.6c41bc4408002e1f",
                "role": "Admin"
            }
        ],
        "_threadProps": {
            "capabilities": [
                "AddMember",
                "ChangeTopic",
                "ChangePicture",
                "EditMsg",
                "CallP2P",
                "SendText",
                "SendSms",
                "SendFileP2P",
                "SendContacts",
                "SendVideoMsg",
                "SendMediaMsg",
                "ChangeModerated"
            ],
            "createdat": "1629381096619",
            "creator": "8:live:.cid.6c41bc4408002e1f",
            "creatorcid": "0",
            "historydisclosed": "true",
            "lastjoinat": "1629381096760",
            "membercount": "2",
            "members": "[\"8:live:.cid.894d225aeeb5246d\",\"8:live:.cid.6c41bc4408002e1f\"]",
            "topic": "31337 Hax0r Plan",
            "version": "1629381097916"
        },
        "_timestamp": 1630472727022,
        "convViewVersion": 1630473492319,
        "id": "19:4bcb97fbc4674b7cb0fd69d5ec8fed1a@thread.skype",
        "isBricked": false,
        "isFake": false,
        "lastMessage": {
            "_countsType": 1,
            "_isEphemeral": false,
            "_isMyMessage": 0,
            "_serverMessages": [
                {
                    "clientmessageid": "16809682010359575515",
                    "composetime": "2021-09-01T05:05:20.158Z",
                    "content": "<a href=\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\">https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0</a>",
                    "conversationLink": "https://azwus1-client-s.gateway.messenger.live.com/v1/users/ME/conversations/19:4bcb97fbc4674b7cb0fd69d5ec8fed1a@thread.skype",
                    "conversationid": "19:4bcb97fbc4674b7cb0fd69d5ec8fed1a@thread.skype",
                    "from": "https://azwus1-client-s.gateway.messenger.live.com/v1/users/ME/contacts/8:live:.cid.894d225aeeb5246d",
                    "id": "1630472727022",
                    "messagetype": "RichText",
                    "originalarrivaltime": "2021-09-01T05:05:20.158Z",
                    "properties": {
                        "urlpreviews": "[{\"key\":\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\",\"value\":{\"url\":\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\",\"size\":\"2198\",\"status_code\":\"200\",\"content_type\":\"text/html\",\"site\":\"mega.nz\",\"category\":\"generic\",\"title\":\"File on MEGA\",\"favicon\":\"\",\"thumbnail\":\"https://sa1-urlp.secure.skypeassets.com/infodel30/894cddc7-c2ba-4c48-8a67-04ee5824d712.png\",\"thumbnail_meta\":{\"width\":240,\"height\":240},\"user_pic\":\"\"}}]"
                    },
                    "type": "Message",
                    "version": "1630472727022"
                }
            ],
            "composeTime": 1630472720158,
            "content": "<a href=\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\">https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0</a>",
            "conversationId": "19:4bcb97fbc4674b7cb0fd69d5ec8fed1a@thread.skype",
            "createdTime": 1630472727022,
            "creator": "8:live:.cid.894d225aeeb5246d",
            "cuid": "16809682010359575515",
            "messagetype": "RichText",
            "properties": {
                "urlpreviews": "[{\"key\":\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\",\"value\":{\"url\":\"https://mega.nz/file/TsNFFS5I#_oYRNNTLDD9ZZ47Is-P8K9lQCl8BGC5RDeE65aUS2N0\",\"size\":\"2198\",\"status_code\":\"200\",\"content_type\":\"text/html\",\"site\":\"mega.nz\",\"category\":\"generic\",\"title\":\"File on MEGA\",\"favicon\":\"\",\"thumbnail\":\"https://sa1-urlp.secure.skypeassets.com/infodel30/894cddc7-c2ba-4c48-8a67-04ee5824d712.png\",\"thumbnail_meta\":{\"width\":240,\"height\":240},\"user_pic\":\"\"}}]"
            }
        },
        "memberConsumptionHorizonsSorted": [
            {
                "consumptionHorizon": 1630471256133,
                "consumptionHorizonUpdateTime": 1630471254613,
                "id": "8:live:.cid.6c41bc4408002e1f"
            },
            {
                "consumptionHorizon": 1630472727022,
                "consumptionHorizonUpdateTime": 1630472726999,
                "id": "8:live:.cid.894d225aeeb5246d"
            }
        ],
        "mriNamespace": 19,
        "threadDetailsVersion": 1629381097916
    },
    "counts": {
        "consumptionHorizonTimestamp": 1630472727022,
        "convHashUsedForCalc": "rmx/b4bVPTfy7lbE6a8xdxrVpZI/9tTV0vY5Td9tCcM=",
        "hasUnread": 0,
        "highPriorityUnreadCount": 0,
        "numMessagesSentByUser": 3,
        "unreadCount": 0,
        "unreadCountOverflowed": false
    },
    "syncInfo": {
        "messageHistoryStartTime": 2,
        "messagesStale": false,
        "messagesSyncState": "3c3000000031393a3462636239376662633436373462376362306664363964356563386665643161407468726561642e736b79706501fcc038a8560100008165cb9f7b01000000"
    }
}
```
Analysing this json file, I found the likely group name as well as the group creator id number:

<!---
COLOCAR A EXATA PARTE ONDE FORAM ENCONTRADAS AS EVIDÊNCIAS
-->

At this point, we have the following flag and the group creator member id:
```
GrabCON{Skype_<email>_31337_Hax0r_Plan_<member_name>}
```
```json
"creator": "8:live:.cid.6c41bc4408002e1f"
```

Now we just need to find the member name and its email. To accomplish this, go to the **profilecachev8** table:

<!---
COLOCAR PRINT DA TABELA DOS PERFIS
-->

As we can see, in the line 6 and row **nsp_pk**, the value is the same we've found for the group creator member id. Double-click the column on the side and then the following json is shown:

```json
{
    "_phoneNumbersForDbIndex": [],
    "city": null,
    "color": {
        "colors": [
            "#49409A",
            "#8378DE"
        ],
        "key": "blue",
        "primaryAccent": "#49409A",
        "secondaryAccent": "#8378DE"
    },
    "country": null,
    "displayNameOverride": "evil mike",
    "emails": [
        "sidemaf155@5ubo.com"
    ],
    "fetchedDate": 1630470959118,
    "fullName": "evil mike",
    "gender": 0,
    "mri": "8:live:.cid.6c41bc4408002e1f",
    "phoneHashes": [],
    "phones": [],
    "province": null
}
```

The name is: "**evil mike**" and the email is: "**sidemaf155@5ubo.com**".


Thus, the full flag is:

```
GrabCON{Skype_sidemaf155@5ubo.com_31337_Hax0r_Plan_evil_mike}
```

