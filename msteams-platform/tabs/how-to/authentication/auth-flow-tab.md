---
title: Flujo de autenticación para pestañas
description: Describe el flujo de autenticación en las pestañas
keywords: pestañas de flujo de autenticación de Teams
ms.openlocfilehash: 6c669162f407924f0844b89625f5c5791e96b6f7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675962"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Flujo de autenticación de Microsoft Teams para pestañas

> [!Note]
> Para que la autenticación funcione para su pestaña en clientes móviles, debe asegurarse de que está usando al menos la versión 1.4.1 del SDK de Teams para JavaScript.

OAuth 2,0 es un estándar abierto para la autenticación y autorización usado por Azure AD y muchos otros proveedores de identidades. Una descripción básica de OAuth 2,0 es un requisito previo para trabajar con la autenticación en Microsoft Teams. [esta es una buena introducción](https://aaronparecki.com/oauth-2-simplified/) que es más fácil de seguir que la [especificación formal](https://oauth.net/2/). El flujo de autenticación para fichas y bots es un poco diferente porque las pestañas son muy similares a los sitios web para que puedan usar OAuth 2,0 directamente; los bots no son y deben hacer algunas cosas de manera diferente, pero los conceptos básicos son idénticos.

para obtener un ejemplo que muestra el flujo de autenticación para pestañas y bots mediante node usando el [tipo de concesión implícito 2,0 de OAuth](https://oauth.net/2/grant-types/implicit/).

![Diagrama de secuencia de autenticación de pestaña](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. El usuario interactúa con el contenido de la página de configuración de ficha o de contenido, normalmente un botón con la etiqueta "iniciar sesión" o "iniciar sesión".
2. La pestaña crea la dirección URL de su página de inicio de autenticación, opcionalmente con información de los marcadores de posición `microsoftTeams.getContext()` de la dirección URL o llamando al método del SDK del cliente de Microsoft Teams para simplificar la experiencia de autenticación del usuario. Por ejemplo, al autenticar con Azure AD, si el `login_hint` parámetro se establece en la dirección de correo electrónico del usuario, es posible que el usuario ni siquiera tenga que iniciar sesión si lo ha hecho recientemente, porque Azure ad usará las credenciales almacenadas en caché del usuario, si es posible: el elemento emergente parpadeará brevemente y luego desaparecerá.
3. A continuación, la ficha `microsoftTeams.authentication.authenticate()` llama al método y registra `successCallback` las `failureCallback` funciones y.
4. Microsoft Teams abrirá la página de inicio en un iframe en una ventana emergente. La página de inicio genera `state` datos aleatorios, los guarda para su futura validación y redirige al extremo del `/authorize` proveedor de identidades `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` como para Azure ad. Reemplace `<tenant id>` con su propio identificador de espacio empresarial (context. TID).
    * Al igual que otros flujos de autenticación de aplicaciones en Microsoft Teams, la página de inicio debe estar `validDomains` en un dominio que se encuentra en la lista y en el mismo dominio que la página de redireccionamiento posterior al inicio de sesión.
    * **Importante**: el flujo de concesión implícita de OAuth 2,0 llama `state` a un parámetro en la solicitud de autenticación que contiene datos de sesión únicos para evitar un [ataque de falsificación de solicitud entre sitios](https://en.wikipedia.org/wiki/Cross-site_request_forgery). En los ejemplos siguientes se usa un GUID generado aleatoriamente para `state` los datos.
5. En el sitio del proveedor, el usuario inicia sesión y concede acceso a la pestaña.
6. El proveedor lleva al usuario a la página de redireccionamiento de OAuth 2,0 de la pestaña con un token de acceso.
7. La pestaña comprueba que el valor `state` devuelto coincida con lo que se guardó anteriormente `microsoftTeams.authentication.notifySuccess()`y que llame a las llamadas `successCallback` , que a su vez llama a la función registrada en el paso 3.
8. Teams cierra la ventana emergente.
9. La pestaña muestra la interfaz de usuario de configuración o actualiza o vuelve a cargar el contenido de las pestañas, según desde dónde empezó el usuario.

## <a name="treat-tab-context-as-hints"></a>Tratar el contexto de la pestaña como sugerencias

Aunque el contexto de la pestaña proporciona información útil acerca del usuario, no use esta información para autenticar al usuario si los obtiene como parámetros URL en la dirección URL de contenido de la `microsoftTeams.getContext()` pestaña o mediante una llamada a la función en el SDK del cliente de Microsoft Teams. Un actor malintencionado podría invocar la dirección URL de contenido de pestaña con sus propios parámetros y una página web que suplanta a Microsoft Teams podría cargar la URL de contenido de la pestaña en un `getContext()` iframe y devolver sus propios datos a la función. Debe tratar la información relacionada con la identidad en el contexto de pestañas simplemente como sugerencias y validarlas antes de usarlas.

## <a name="samples"></a>Ejemplos

Para ver el código de ejemplo que muestra el proceso de autenticación de la pestaña, consulte:

* [Ejemplo de autenticación de pestañas de Microsoft Teams (nodo)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Ejemplo de autenticación de la pestaña de Microsoft Teams (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>Más detalles

Para obtener un tutorial de implementación detallado sobre la autenticación de pestañas dirigidas a Azure Active Directory, vea:

* [Autenticar a un usuario en una pestaña de Microsoft Teams](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [Autenticación silenciosa](~/tabs/how-to/authentication/auth-silent-AAD.md)
