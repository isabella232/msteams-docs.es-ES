---
title: Mensajes proactivos
description: Describe los bots puede iniciar una conversación en Microsoft Teams.
keywords: escenarios de la conversación de mensajería proactiva de Teams
ms.openlocfilehash: adb677bf348065713911d576289c432f8aba3960
ms.sourcegitcommit: b822584b643e003d12d2e9b5b02a0534b2d57d71
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2020
ms.locfileid: "44704456"
---
# <a name="proactive-messaging-for-bots"></a>Mensajería proactiva para bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un mensaje proactivo es un mensaje enviado por un bot para iniciar una conversación. Es posible que desee que el bot inicie una conversación por varios motivos, entre los que se incluyen:

* Mensajes de bienvenida para conversaciones de bot personal
* Respuestas de sondeo
* Notificaciones de eventos externos

El envío de un mensaje para iniciar una nueva conversación es diferente al de enviar un mensaje en respuesta a una conversación existente: cuando el bot inicia una nueva conversación, no hay ninguna conversación preexistente para publicar el mensaje en. Para poder enviar un mensaje proactivo debe:

1. [Decide qué vas a decir](#best-practices-for-proactive-messaging)
1. [Obtener el identificador único del usuario y el identificador de inquilino](#obtain-necessary-user-information)
1. [Enviar el mensaje](#examples)

Al crear mensajes proactivos a los que se **debe** llamar `MicrosoftAppCredentials.TrustServiceUrl` y pasar la dirección URL del servicio antes de crear el, `ConnectorClient` se usará para enviar el mensaje. Si no lo hace, la aplicación recibirá una `401: Unauthorized` respuesta. Vea [los ejemplos siguientes](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Procedimientos recomendados para la mensajería proactiva

El envío de mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios. Sin embargo, desde su perspectiva puede parecer que este mensaje no se solicita completamente y, en el caso de los mensajes de bienvenida, será la primera vez que interactuen con la aplicación. Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionarle la información suficiente para que puedan comprender por qué se les está enviando un mensaje.

Generalmente, los mensajes proactivos se dividen en dos categorías, mensajes de bienvenida o notificaciones.

### <a name="welcome-messages"></a>Mensajes de bienvenida

Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que para la mayoría de las personas que reciben el mensaje no tendrán contexto por el motivo por el que lo reciben. También es la primera vez que interactuarán con la aplicación; es su oportunidad para crear una buena primera impresión. Los mejores mensajes de bienvenida incluirán:

* **¿Por qué reciben este mensaje?** El usuario debe ser muy claro por qué reciben el mensaje. Si el bot se ha instalado en un canal y se ha enviado un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se ha instalado y que podrían instalarlo.
* **Qué ofrece.** ¿Qué puede hacer con la aplicación? ¿Qué valor puede aportar a ellos?
* **Qué debería hacer a continuación.** Invitar a probar un comando o interactuar con la aplicación de alguna manera.

### <a name="notification-messages"></a>Mensajes de notificación

Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para emprender acciones comunes en función de la notificación y un conocimiento claro de la razón por la que se produjo la notificación. Por lo general, los mensajes de notificación son correctos:

* **Qué ha pasado.** Una indicación clara de lo que ha sucedido para provocar la notificación.
* **Qué ocurrió.** Debe estar claro qué elemento/Thing se actualizó para provocar la notificación.
* **Quién lo llevó a cabo.** Quién llevó a cabo la acción que hizo que se enviara la notificación.
* **Qué pueden hacer al respecto.** Facilite a los usuarios que realicen acciones basadas en las notificaciones.
* **Cómo se pueden dejar de participar.** Debe proporcionar una ruta de acceso para que los usuarios puedan optar por las notificaciones adicionales.

## <a name="obtain-necessary-user-information"></a>Obtener información de usuario necesaria

Los bots pueden crear nuevas conversaciones con un usuario individual de Microsoft Teams obteniendo el *identificador único* del usuario y el *identificador de inquilino.* Puede obtener estos valores mediante uno de los métodos siguientes:

* Mediante [la recopilación de la lista de equipos](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) desde un canal en el que está instalada la aplicación.
* Mediante el almacenamiento en la memoria caché cuando un usuario [interactúa con el bot en un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Cuando se @mentioned a un usuario [en una conversación de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) a la que pertenece el bot.
* Al almacenarlos en la memoria caché cuando [recibe el `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) evento cuando la aplicación está instalada en un ámbito personal o se agregan nuevos miembros a un canal o chat de grupo que

### <a name="proactively-install-your-app-using-graph"></a>Instalar de forma proactiva la aplicación con Graph

> [!Note]
> La instalación de aplicaciones de forma proactiva con Graph se encuentra actualmente en versión beta.

En ocasiones, es posible que sea necesario enviar un mensaje de forma proactiva a los usuarios que no hayan instalado ni interactúen con la aplicación anteriormente. Por ejemplo, desea usar el Communicator de la [compañía](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización. Para este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para sus usuarios y, a continuación, almacenar en caché los valores necesarios del `conversationUpdate` evento que la aplicación recibirá en el momento de la instalación.

Solo puede instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.

Consulte [install apps for users](/graph/teams-proactive-messaging) en la documentación de Graph para obtener detalles completos. También hay un [ejemplo en .net](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Ejemplos

Asegúrese de autenticar y de tener un token de portador antes de crear una nueva conversación mediante la API de REST.

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

Debe proporcionar el identificador de usuario y el identificador de inquilino. Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Este identificador es el identificador de conversación único de chat personal. Almacene este valor y vuelva a usarlo para interacciones futuras con el usuario.

### <a name="using-net"></a>Uso de .NET

En este ejemplo se usa el paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a>Uso de Node.js

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

*Vea también* [ejemplos del marco de bot](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="creating-a-channel-conversation"></a>Crear una conversación de canal

El bot agregado por el equipo puede exponer en un canal para crear una nueva cadena de respuesta. Si usa el SDK de Node.js Teams, use `startReplyChain()` que le proporcione una dirección completa con el identificador de actividad correcto y el identificador de conversación. Si usa C#, vea el ejemplo siguiente.

Como alternativa, puede usar la API de REST y enviar una solicitud POST al [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) recurso.

### <a name="net-example-from-this-sample"></a>Ejemplo de .NET (de [este ejemplo](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```
