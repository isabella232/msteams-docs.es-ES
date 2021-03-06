---
title: Agregar autenticación a la extensión de mensajería
author: clearab
description: Cómo agregar autenticación a una extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675774"
---
# <a name="add-authentication-to-your-messaging-extension"></a>Agregar autenticación a la extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identificar al usuario

Todas las solicitudes a los servicios incluyen el identificador ofuscado del usuario que realizó la solicitud, así como el nombre para mostrar del usuario y el identificador de objeto de Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Se `id` garantiza `aadObjectId` que los valores y son los del usuario de Teams autenticado. Se pueden usar como claves para buscar credenciales o cualquier estado almacenado en la memoria caché del servicio. Además, cada solicitud contiene el identificador de inquilino de Azure Active Directory del usuario, que se puede usar para identificar la organización del usuario. Si procede, la solicitud también contiene los identificadores de equipo y de canal desde los que se originó la solicitud.

## <a name="authentication"></a>Autenticación

Si su servicio requiere la autenticación del usuario, debe iniciar sesión en el usuario antes de que pueda usar la extensión de mensajería. Si ha escrito un bot o una pestaña que inicia sesión en el usuario, esta sección debería resultarle familiar.

La secuencia es la siguiente:

1. El usuario emite una consulta o se envía automáticamente la consulta predeterminada a su servicio.
2. El servicio comprueba si el usuario se ha autenticado primero mediante la inspección del identificador de usuario de Teams.
3. Si el usuario no se ha autenticado, vuelva a `auth` enviar una respuesta `openUrl` con una acción sugerida que incluya la dirección URL de autenticación.
4. El cliente de Microsoft Teams inicia una ventana emergente que hospeda la página web con la dirección URL de autenticación especificada.
5. Después de que el usuario inicie sesión, debe cerrar la ventana y enviar un "código de autenticación" al cliente de Teams.
6. A continuación, el cliente de Microsoft Teams envía la consulta a su servicio, que incluye el código de autenticación pasado en el paso 5.

El servicio debe comprobar que el código de autenticación recibido en el paso 6 coincida con el del paso 5. Esto garantiza que un usuario malintencionado no intente imitar ni poner en peligro el flujo de inicio de sesión. De hecho, "cierra el bucle" para finalizar la secuencia de autenticación segura.

### <a name="respond-with-a-sign-in-action"></a>Responder con una acción de inicio de sesión

Para solicitar a un usuario no autenticado que inicie sesión, responda con una acción sugerida `openUrl` de tipo que incluya la dirección URL de autenticación.

#### <a name="response-example-for-a-sign-in-action"></a>Ejemplo de respuesta de una acción de inicio de sesión

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> Para que la experiencia de inicio de sesión se hospede en una ventana emergente de Teams, la parte de dominio de la dirección URL debe estar en la lista de dominios válidos de la aplicación. (Vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en el esquema del manifiesto).

### <a name="start-the-sign-in-flow"></a>Iniciar el flujo de inicio de sesión

La experiencia de inicio de sesión debe ser eficaz y ajustarse en una ventana emergente. Debe integrarse con el [SDK cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client), que usa el paso de mensajes.

Al igual que con otras experiencias incrustadas que se ejecutan dentro de Microsoft Teams, el `microsoftTeams.initialize()`código dentro de la ventana debe llamar primero. Si el código realiza un flujo de OAuth, puede pasar el identificador de usuario de Teams a la ventana, que puede pasarla a la dirección URL de inicio de sesión de OAuth.

### <a name="complete-the-sign-in-flow"></a>Completar el flujo de inicio de sesión

Cuando la solicitud de inicio de sesión se completa y redirige de nuevo a la página, debe realizar los siguientes pasos:

1. Generar un código de seguridad. (Puede ser un número aleatorio). Debe almacenar en caché este código en el servicio, junto con las credenciales obtenidas a través del flujo de inicio de sesión (por ejemplo, los tokens 2,0 de OAuth).
2. Llamar `microsoftTeams.authentication.notifySuccess` y pasar el código de seguridad.

En este momento, la ventana se cierra y el control se pasa al cliente de Teams. El cliente ahora puede volver a emitir la consulta de usuario original, junto con el código de `state` seguridad de la propiedad. El código puede usar el código de seguridad para buscar las credenciales almacenadas anteriormente para completar la secuencia de autenticación y, a continuación, completar la solicitud del usuario.

#### <a name="reissued-request-example"></a>Ejemplo de solicitud reemitiendo

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

