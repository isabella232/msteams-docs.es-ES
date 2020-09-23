---
author: heath-hamilton
description: Obtenga información sobre cómo crear una pestaña de canal para su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: Crear una pestaña de canal de Teams
ms.openlocfilehash: d0846c3af23fd9df6013f989e9f455f711d05a5f
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210343"
---
# <a name="build-a-teams-channel-tab"></a><span data-ttu-id="e7e40-103">Crear una pestaña de canal de Teams</span><span class="sxs-lookup"><span data-stu-id="e7e40-103">Build a Teams channel tab</span></span>

<span data-ttu-id="e7e40-104">En este tutorial, creará una ficha básica de *canal*, una página de contenido a pantalla completa para un canal de equipo o un chat.</span><span class="sxs-lookup"><span data-stu-id="e7e40-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="e7e40-105">A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de una ficha de canal (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).</span><span class="sxs-lookup"><span data-stu-id="e7e40-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e7e40-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e7e40-106">Before you begin</span></span>

<span data-ttu-id="e7e40-107">Necesita una aplicación básica que se ejecute para empezar.</span><span class="sxs-lookup"><span data-stu-id="e7e40-107">You need a basic running app to get started.</span></span> <span data-ttu-id="e7e40-108">Si no tiene una, siga la [compilación y ejecute las instrucciones de la primera aplicación de Teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="e7e40-108">If you don't have one, follow the [build and run your Teams first app instructions](../build-your-first-app/build-and-run.md).</span></span> <span data-ttu-id="e7e40-109">Al crear el proyecto de la aplicación, elija solo la opción de la **ficha canal de grupo o de Teams** .</span><span class="sxs-lookup"><span data-stu-id="e7e40-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="e7e40-110">La asignación</span><span class="sxs-lookup"><span data-stu-id="e7e40-110">Your assignment</span></span>

<span data-ttu-id="e7e40-111">No hace mucho tiempo, su organización ha creado una ficha de Microsoft Teams con información sobre cómo ponerse en contacto con las funciones importantes (Departamento de soporte técnico, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="e7e40-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="e7e40-112">Sin embargo, como el ámbito de la pestaña solo es para uso personal, cada usuario debe instalar la ficha para verla y la adopción es inferior a la esperada.</span><span class="sxs-lookup"><span data-stu-id="e7e40-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="e7e40-113">En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="e7e40-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="e7e40-114">Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7e40-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="e7e40-115">En su lugar, un usuario puede instalar la pestaña en un canal o chatear para obtener el beneficio de todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="e7e40-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e7e40-116">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="e7e40-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="e7e40-117">Identificar algunas de las propiedades del manifiesto de la aplicación y scaffolding relevantes para las pestañas del canal</span><span class="sxs-lookup"><span data-stu-id="e7e40-117">Identify some of the app manifest properties and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="e7e40-118">Crear contenido de ficha</span><span class="sxs-lookup"><span data-stu-id="e7e40-118">Create tab content</span></span>
> * <span data-ttu-id="e7e40-119">Crear contenido para la página de configuración de una pestaña</span><span class="sxs-lookup"><span data-stu-id="e7e40-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="e7e40-120">Permitir la configuración y la instalación de una pestaña</span><span class="sxs-lookup"><span data-stu-id="e7e40-120">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="e7e40-121">Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="e7e40-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="e7e40-122">Identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="e7e40-122">Identify relevant app project components</span></span>

<span data-ttu-id="e7e40-123">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="e7e40-123">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="e7e40-124">Echemos un vistazo a los componentes principales para crear una pestaña de canal.</span><span class="sxs-lookup"><span data-stu-id="e7e40-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="e7e40-125">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e7e40-125">App manifest</span></span>

<span data-ttu-id="e7e40-126">El siguiente fragmento de código del manifiesto de la aplicación muestra [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , que incluye las propiedades y los valores predeterminados que son relevantes para las pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="e7e40-126">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* <span data-ttu-id="e7e40-127">`configurationUrl`: La dirección URL del host de la página de configuración de pestañas (debe ser HTTPS).</span><span class="sxs-lookup"><span data-stu-id="e7e40-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="e7e40-128">`canUpdateConfiguration`: Si se establece en `true` , los usuarios pueden cambiar la configuración de las pestañas, cambiar el nombre de la pestaña o quitarla de un canal o un chat.</span><span class="sxs-lookup"><span data-stu-id="e7e40-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="e7e40-129">`scopes`: Especifica si los usuarios pueden instalar la aplicación en los canales ( `team` ) y los chats ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="e7e40-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="e7e40-130">Se requiere al menos un valor.</span><span class="sxs-lookup"><span data-stu-id="e7e40-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="e7e40-131">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e7e40-131">App scaffolding</span></span>

<span data-ttu-id="e7e40-132">El scaffolding de la aplicación proporciona un `TabConfig.js` archivo, que se encuentra en el `src/components` directorio del proyecto, para representar la página de configuración de la pestaña (próximamente, esto es más).</span><span class="sxs-lookup"><span data-stu-id="e7e40-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="e7e40-133">Crear el contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="e7e40-133">Create your tab content</span></span>

<span data-ttu-id="e7e40-134">Abra el manifiesto de la aplicación ( `manifest.json` ) en el `.publish` Directorio y establezca las siguientes propiedades en [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , que define la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="e7e40-134">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

<span data-ttu-id="e7e40-135">Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="e7e40-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="e7e40-136">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="e7e40-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="e7e40-137">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="e7e40-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="e7e40-138">Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="e7e40-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="e7e40-139">Crear la página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="e7e40-139">Create your tab configuration page</span></span>

<span data-ttu-id="e7e40-140">Cada ficha de canal tiene una página de configuración, un modal con al menos una opción de configuración que se muestra al instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7e40-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="e7e40-141">De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.</span><span class="sxs-lookup"><span data-stu-id="e7e40-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="e7e40-142">Agregue contenido a la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="e7e40-142">Add some content to your configuration page.</span></span> <span data-ttu-id="e7e40-143">Vaya al directorio del proyecto `src/components` , Abra `TabConfig.js` e inserte contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="e7e40-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> <span data-ttu-id="e7e40-144">Como mínimo, proporcione información breve sobre la aplicación en esta página, ya que esto puede ser la primera vez que los usuarios aprenden sobre ella.</span><span class="sxs-lookup"><span data-stu-id="e7e40-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="e7e40-145">También puede incluir opciones de configuración personalizadas o un [flujo de trabajo de autenticación](../tabs/how-to/authentication/auth-aad-sso.md), que es común en las páginas de configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="e7e40-145">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="e7e40-146">Permitir la configuración y la instalación de la ficha</span><span class="sxs-lookup"><span data-stu-id="e7e40-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="e7e40-147">Para que los usuarios puedan configurar e instalar correctamente la ficha canal, debe agregar la dirección URL de host que configuró al [crear y ejecutar su primera aplicación](../build-your-first-app/build-and-run.md) en el componente de página de configuración.</span><span class="sxs-lookup"><span data-stu-id="e7e40-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](../build-your-first-app/build-and-run.md) to the configuration page component.</span></span>

<span data-ttu-id="e7e40-148">Vaya a `TabConfig.js` y busque `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="e7e40-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="e7e40-149">Para `"contentUrl"` , reemplace la `localhost:3000` parte de la dirección URL con el dominio en el que hospeda el contenido de la pestaña (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="e7e40-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="e7e40-150">Además, asegúrese de que `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="e7e40-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="e7e40-151">De forma predeterminada, pero si se establece en `false` , el botón **Guardar** se deshabilita en la página Configuración.</span><span class="sxs-lookup"><span data-stu-id="e7e40-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="e7e40-152">Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="e7e40-152">Provide a suggested tab name</span></span>

<span data-ttu-id="e7e40-153">Al instalar una pestaña para uso personal, el nombre para mostrar es la `name` propiedad en la `staticTabs` parte del manifiesto de la aplicación (por ejemplo, **mis contactos**).</span><span class="sxs-lookup"><span data-stu-id="e7e40-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="e7e40-154">Al instalar una pestaña de canal, se muestra el nombre de la aplicación (por ejemplo, **primera aplicación**) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e7e40-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="e7e40-155">Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo**).</span><span class="sxs-lookup"><span data-stu-id="e7e40-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="e7e40-156">En `TabConfig.js` , vuelva a `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="e7e40-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="e7e40-157">Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="e7e40-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="e7e40-158">Use el nombre proporcionado o cree el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="e7e40-158">Use the provided name or create your own.</span></span> <span data-ttu-id="e7e40-159">Recuerde que en el manifiesto está permitiendo a los usuarios cambiar el nombre si lo desean.</span><span class="sxs-lookup"><span data-stu-id="e7e40-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="e7e40-160">Ver la ficha canal</span><span class="sxs-lookup"><span data-stu-id="e7e40-160">View the channel tab</span></span>

<span data-ttu-id="e7e40-161">Para ver las páginas de contenido y configuración de la pestaña de canal, debe instalarla en un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="e7e40-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="e7e40-162">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7e40-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="e7e40-163">Seleccione **cargar una aplicación personalizada** y elija la aplicación `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="e7e40-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="e7e40-164">Elija **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="e7e40-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="e7e40-165">Seleccione **configurar una pestaña**. Aparece la página Configuración.</span><span class="sxs-lookup"><span data-stu-id="e7e40-165">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::
1. <span data-ttu-id="e7e40-167">Seleccione **Guardar** para configurar la pestaña. Se muestra el contenido.</span><span class="sxs-lookup"><span data-stu-id="e7e40-167">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="e7e40-169">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="e7e40-169">Well done</span></span>

<span data-ttu-id="e7e40-170">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="e7e40-170">Congratulations!</span></span> <span data-ttu-id="e7e40-171">Tiene una aplicación de Microsoft Teams con una pestaña de canal para mostrar contenido útil en canales y chats.</span><span class="sxs-lookup"><span data-stu-id="e7e40-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="e7e40-172">Obtén más información</span><span class="sxs-lookup"><span data-stu-id="e7e40-172">Learn more</span></span>

* <span data-ttu-id="e7e40-173">[Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="e7e40-173">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="e7e40-174">[Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="e7e40-174">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="e7e40-175">[Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e7e40-175">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="e7e40-176">[Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="e7e40-176">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="e7e40-177">Crear una ficha sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="e7e40-177">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="e7e40-178">Lección siguiente</span><span class="sxs-lookup"><span data-stu-id="e7e40-178">Next lesson</span></span>

<span data-ttu-id="e7e40-179">Sabe cómo crear una pestaña para la colaboración.</span><span class="sxs-lookup"><span data-stu-id="e7e40-179">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="e7e40-180">¿Desea intentar compilar un tipo diferente de aplicación de Teams?</span><span class="sxs-lookup"><span data-stu-id="e7e40-180">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7e40-181">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="e7e40-181">Build a bot</span></span>](../build-your-first-app/build-bot.md)