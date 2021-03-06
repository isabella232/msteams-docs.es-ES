---
title: Controlar eventos de bot
description: Describe cómo controlar eventos en bots para Microsoft Teams.
keywords: eventos de bots de Teams
ms.date: 05/20/2019
ms.author: lajanuar
author: laujan
ms.openlocfilehash: cb3463b8cfb14920644f16f84a09260739a82ede
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877046"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Controlar eventos de bot en Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams envía notificaciones a su bot para cambios o eventos que ocurren en ámbitos donde el bot está activo. Puede usar estos eventos para desencadenar la lógica del servicio, como los siguientes:

* Desencadenar un mensaje de bienvenida cuando se agrega un bot a un equipo
* Información del grupo de consultas y caché cuando se agrega el bot a un chat en grupo
* Actualizar la información almacenada en caché de la información del canal o la pertenencia del equipo
* Quitar la información almacenada en caché de un equipo si se quita el bot
* Cuando un usuario le gusta un mensaje de bot?

Cada evento de bot se envía como un `Activity` objeto en el que `messageType` define qué información se encuentra en el objeto. Para los mensajes de tipo `message` , vea [enviar y recibir mensajes](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Los eventos de grupo y de equipo, que normalmente se desactivan `conversationUpdate` en el tipo, tienen información de eventos de Microsoft teams que se pasan como parte del `channelData` objeto y, por lo tanto, el controlador de eventos debe consultar la `channelData` carga de los equipos `eventType` y metadatos específicos del evento adicionales.

En la siguiente tabla se enumeran los eventos que el bot puede recibir y en los que se puede realizar una acción.

|Tipo|Objeto payload|EventType de Teams |Descripción|Ámbito|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Miembro agregado al equipo](#team-member-or-bot-addition)| todos |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[El miembro se quitó del equipo](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Se cambió el nombre del equipo](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Se ha creado un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Se cambió el nombre de un canal](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Se ha eliminado un canal](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Mensaje de reacción a bot](#reactions)| todos |
| `messageReaction` |`reactionsRemoved`|| [Se ha eliminado la reacción del mensaje de bot](#reactions)| todos |

## <a name="team-member-or-bot-addition"></a>Adición de un miembro del equipo o bot

El [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) evento se envía a su bot cuando recibe información sobre las actualizaciones de pertenencia para equipos en los que se ha agregado. También recibe una actualización cuando se ha agregado por primera vez específicamente para conversaciones personales. Tenga en cuenta que la información del usuario ( `Id` ) es única para su bot y puede almacenarse en caché para su uso en el futuro por parte del servicio (por ejemplo, enviar un mensaje a un usuario específico).

### <a name="bot-or-user-added-to-a-team"></a>Bot o usuario agregado a un equipo

El `conversationUpdate` evento con el `membersAdded` objeto en la carga se envía cuando se agrega un bot a un equipo o se agrega un nuevo usuario a un equipo en el que se ha agregado un bot. Microsoft Teams también agrega `eventType.teamMemberAdded` en el `channelData` objeto.

Como este evento se envía en ambos casos, debe analizar el `membersAdded` objeto para determinar si la adición fue un usuario o el bot en sí. Para la segunda, un procedimiento recomendado es enviar un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) al canal para que los usuarios puedan comprender las características que proporciona el bot.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Código de ejemplo: comprobar si Bot fue el miembro agregado

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>Ejemplo de esquema: bot agregado al equipo

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>Usuario agregado a una reunión

El `conversationUpdate` evento con el `membersAdded` objeto en la carga se envía cuando un usuario se agrega a una reunión privada programada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión. 

> [!NOTE]
>
>* Cuando se agrega un usuario anónimo a una reunión, el objeto de carga membersAdded no tiene `aadObjectId` campo.
>* Cuando se agrega un usuario anónimo a una reunión, `from` el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si el usuario anónimo fue agregado por otro moderador.

#### <a name="schema-example-user-added-to-meeting"></a>Ejemplo de esquema: usuario agregado a la reunión

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>Bot agregado solo para contexto personal

El bot recibe un `conversationUpdate` con `membersAdded` cuando un usuario lo agrega directamente al chat personal. En este caso, la carga que el bot recibe no contiene el `channelData.team` objeto. Debe usarlo como filtro en caso de que desee que el bot ofrezca un [mensaje de bienvenida](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) diferente según el ámbito.

> [!NOTE]
> En el caso de los bots de ámbito personal, el bot solo recibirá el `conversationUpdate` evento una sola vez, incluso si el bot se quita y se vuelve a agregar. Para el desarrollo y las pruebas, puede que le resulte útil agregar una función auxiliar que le permita restablecer su bot por completo. Vea un [ ejemplo deNode.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) o un [ejemplo de C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) para obtener más información sobre la implementación de esto.

#### <a name="schema-example-bot-added-to-personal-context"></a>Ejemplo de esquema: bot agregado a contexto personal

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a>Miembro o bot quitado del equipo

El `conversationUpdate` evento con el `membersRemoved` objeto en la carga se envía cuando el bot se quita de un equipo, o bien cuando se quita un usuario de un equipo en el que se ha agregado un bot. Microsoft Teams también agrega `eventType.teamMemberRemoved` en el `channelData` objeto. Al igual que con el `membersAdded` objeto, debe analizar el objeto del identificador de la `membersRemoved` aplicación de bot para determinar quién se ha quitado.

### <a name="schema-example-team-member-removed"></a>Ejemplo de esquema: miembro del equipo quitado

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="user-removed-from-a-meeting"></a>Usuario quitado de una reunión

El `conversationUpdate` evento con el `membersRemoved` objeto en la carga se envía cuando un usuario se quita de una reunión programada privada. Los detalles del evento se enviarán incluso cuando los usuarios anónimos se unan a la reunión. 

> [!NOTE]
>
>_ Cuando se quita un usuario anónimo de una reunión, el objeto de carga membersRemoved no tiene `aadObjectId` campo.
>* Cuando se quita un usuario anónimo de una reunión, `from` el objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otro presentador quitó al usuario anónimo.

#### <a name="schema-example-user-removed-from-meeting"></a>Ejemplo de esquema: el usuario quitó la reunión

{       "membersRemoved":        {           "ID": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"         }       ],       "tipo": "conversationUpdate",       "timestamp": "2020-09-29T21:15:08.6391139 z",       "ID": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",       "channelId": "msteams",       "serviceUrl": " https://canary.botapi.skype.com/amer/ ",       "from": {         "ID": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",         "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"       },       "Conversation": {    
        "isGroup": true,         "tenantId": "e15762ef-a8d8-416B-871C-25516354f1fe",         "ID": "19: meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread. V2"       },       "recipient": {         "ID": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",         "Name": "EchoBot1_Rename"       },       "channelData": {         "tenant": {           "ID": "e15762ef-a8d8-416B-871C-25516354f1fe"         },         "Source": null,         "Meeting": {           "ID": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA = ="         }       }    }   

## <a name="team-name-updates"></a>Actualizaciones de nombres de equipo

> [!NOTE]
> No hay ninguna funcionalidad para consultar todos los nombres de los equipos, y el nombre del equipo no se devuelve en cargas de otros eventos.

El bot recibirá una notificación cuando se haya cambiado el nombre al equipo en el que se encuentra. Recibe un `conversationUpdate` evento con `eventType.teamRenamed` en el `channelData` objeto. Tenga en cuenta que no hay notificaciones para la creación o eliminación del equipo porque los bots solo existen como parte de los equipos y no tienen visibilidad fuera del ámbito en el que se han agregado.

### <a name="schema-example-team-renamed"></a>Ejemplo de esquema: nombre del equipo

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a>Actualizaciones de canal

El bot recibe una notificación cuando se crea, se cambia el nombre o se elimina un canal en un equipo en el que se ha agregado. `conversationUpdate`Una vez más, se recibe el evento y se envía un identificador de evento específico de equipo como parte del `channelData.eventType` objeto, donde los datos del canal `channel.id` son el GUID para el canal y `channel.name` contiene el propio nombre del canal.

Los eventos de canal son los siguientes:

* **channelCreated** &emsp; Un usuario agrega un nuevo canal al equipo
* **channelRenamed** &emsp; Un usuario cambia el nombre de un canal existente
* **channelDeleted** &emsp; Un usuario quita un canal

### <a name="full-schema-example-channelcreated"></a>Ejemplo de esquema completo: channelCreated

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Extracto de esquema: channelData para channelRenamed

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Extracto de esquema: channelData para channelDeleted

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a>Comunicar

El `messageReaction` evento se envía cuando un usuario agrega o quita su reacción a un mensaje enviado originalmente por el bot. `replyToId` contiene el identificador del mensaje específico.

### <a name="schema-example-a-user-likes-a-message"></a>Ejemplo de esquema: un usuario le gusta un mensaje

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>Ejemplo de esquema: un usuario no le gusta un mensaje

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```
