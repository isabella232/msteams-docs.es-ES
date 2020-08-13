---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Toolkit
ms.topic: overview
ms.openlocfilehash: 33005174dc1e12e6473522e7d7ee09920a989689
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652179"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="53b24-104">Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53b24-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="53b24-105">El kit de herramientas de Microsoft Teams permite crear aplicaciones de Team personalizadas directamente en el entorno de desarrollo integrado (IDE) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53b24-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="53b24-106">El kit de herramientas de Microsoft Teams le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="53b24-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53b24-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53b24-107">Prerequisites</span></span>

1. [<span data-ttu-id="53b24-108">Habilitar la vista previa para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="53b24-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="53b24-109">Asegúrese de que \*\* <span>ASP.ne</span>T y el módulo de desarrollo web\*\* se hayan agregado a la instancia de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53b24-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="53b24-110">Puede comprobarlo siguiendo los pasos descritos en la documentación sobre [Cómo modificar Visual Studio agregando o quitando cargas de trabajo y componentes](/visualstudio/install/modify-visual-studio?view=vs-2019) .</span><span class="sxs-lookup"><span data-stu-id="53b24-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019) documentation.</span></span>

![módulo de Visual Studio asp.net](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="53b24-112">Si desea probar la aplicación mediante su implementación desde Visual Studio, tendrá que tener instalado IIS (Internet Information Services) en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="53b24-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="53b24-113">Visual Studio no incluye IIS y no se incluye en la configuración predeterminada de Windows 10, Windows 8 o Windows 7; sin embargo, puede descargar la versión más reciente desde el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=48264.)</span><span class="sxs-lookup"><span data-stu-id="53b24-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264.)</span></span>

![Vista de la página de descarga de IIS](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="53b24-115">Instalar el kit de herramientas de Teams</span><span class="sxs-lookup"><span data-stu-id="53b24-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="53b24-116">El kit de herramientas de Microsoft Teams para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) o directamente desde el menú **extensiones** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53b24-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="53b24-117">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="53b24-117">Using the toolkit</span></span>

- [<span data-ttu-id="53b24-118">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="53b24-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="53b24-119">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="53b24-120">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="53b24-121">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="53b24-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="53b24-122">Validar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="53b24-123">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="53b24-124">Configurar un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="53b24-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="53b24-125">Seleccione **crear un nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="53b24-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="53b24-126">Elija **aplicación de Microsoft Teams** y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="53b24-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="53b24-127">Llegará a la pantalla **configurar el nuevo proyecto** , donde podrá elegir el **nombre del proyecto**, la **Ubicación**y el nombre de la **solución**.</span><span class="sxs-lookup"><span data-stu-id="53b24-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="53b24-128">Active la casilla etiquetar la **solución y el proyecto en el mismo directorio**.</span><span class="sxs-lookup"><span data-stu-id="53b24-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="53b24-129">Una ventana emergente con la etiqueta **Agregar funciones** le permitirá elegir una o más funcionalidades para la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="53b24-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="53b24-130">Seleccione el botón **siguiente** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="53b24-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="53b24-131">Una ventana emergente con la etiqueta **Agregar funciones** le permitirá elegir las propiedades de cada funcionalidad seleccionada.</span><span class="sxs-lookup"><span data-stu-id="53b24-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="53b24-132">Seleccione **Finalizar** y estará en la página de aterrizaje de **Microsoft Teams Toolkit** .</span><span class="sxs-lookup"><span data-stu-id="53b24-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="53b24-133">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-133">Configure your app</span></span>

<span data-ttu-id="53b24-134">En esencia, la aplicación de Microsoft Teams adopta tres componentes:</span><span class="sxs-lookup"><span data-stu-id="53b24-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="53b24-135">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53b24-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="53b24-136">Un servidor que responde a las solicitudes de contenido que se mostrarán en Microsoft Teams, por ejemplo, contenido de la ficha HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="53b24-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="53b24-137">Un paquete de la [aplicación](/concepts/build-and-test/apps-package.md) teams que consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="53b24-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="53b24-138">La manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="53b24-138">The manifest.json</span></span>
  > - <span data-ttu-id="53b24-139">Un [icono de color](../resources/schema/manifest-schema.md#icons) de la aplicación para que se muestre en el catálogo de aplicaciones públicas o de la organización</span><span class="sxs-lookup"><span data-stu-id="53b24-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="53b24-140">Un [icono de esquema](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividad de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="53b24-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="53b24-141">Cuando se instala una aplicación, el cliente de Microsoft Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL en la que se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="53b24-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="53b24-142">Si aún no lo ha hecho, tendrá que iniciar sesión en su cuenta de Microsoft 365 o para continuar con el proceso de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="53b24-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="53b24-143">Si no tiene una cuenta de 365 de Microsoft, puede registrarse para obtener una suscripción del [programa de desarrolladores de microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) .</span><span class="sxs-lookup"><span data-stu-id="53b24-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="53b24-144">Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="53b24-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="53b24-145">Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53b24-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="53b24-146">*Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="53b24-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="53b24-147">Pasos de la configuración </span><span class="sxs-lookup"><span data-stu-id="53b24-147">Configuration steps</span></span>

1. <span data-ttu-id="53b24-148">Para configurar la aplicación, en la página de aterrizaje de **Microsoft Teams Toolkit** , seleccione **Editar paquete** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53b24-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="53b24-149">En el menú desplegable **mis entornos** , seleccione **desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="53b24-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="53b24-150">Encontrarás en la página de detalles de la **aplicación** donde puedes editar los campos de propiedades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53b24-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="53b24-151">Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="53b24-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="53b24-152">Más información</span><span class="sxs-lookup"><span data-stu-id="53b24-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="53b24-153">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-153">Package your app</span></span>

<span data-ttu-id="53b24-154">Al modificar la página de detalles de la **aplicación** o actualizar el **manifiesto**, o los archivos **. env** en la carpeta **. Publish** de la aplicación, se generará automáticamente el archivo de **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="53b24-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="53b24-155">El archivo de Development.zip incluye tres archivos necesarios: el **manifest.jsen** y [dos archivos de icono](../concepts/build-and-test/apps-package.md#icons).</span><span class="sxs-lookup"><span data-stu-id="53b24-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="53b24-156">Instalar y ejecutar la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="53b24-156">Install and run your app locally</span></span>

1. <span data-ttu-id="53b24-157">En el menú desplegable **configuraciones de soluciones** , seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="53b24-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![Menú Configuraciones de soluciones](../assets/images/solution-configurations.png)

2. <span data-ttu-id="53b24-159">Seleccione el botón de **ISS Express + Teams** .</span><span class="sxs-lookup"><span data-stu-id="53b24-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="53b24-160">Se iniciará Microsoft Teams y el cuadro de diálogo de instalación de la aplicación debería aparecer en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="53b24-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="53b24-161">Validar la aplicación</span><span class="sxs-lookup"><span data-stu-id="53b24-161">Validate your app</span></span>

<span data-ttu-id="53b24-162">La página **validar** permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource.</span><span class="sxs-lookup"><span data-stu-id="53b24-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="53b24-163">Simplemente cargue el paquete del manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="53b24-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="53b24-164">Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error.</span><span class="sxs-lookup"><span data-stu-id="53b24-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="53b24-165">Para las pruebas que son difíciles de automatizar, los detalles de la **lista de comprobación preliminar** 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.</span><span class="sxs-lookup"><span data-stu-id="53b24-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="53b24-166">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="53b24-166">Publish your app to Teams</span></span>

<span data-ttu-id="53b24-167">✔ En la Página principal de su proyecto, puede cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de su organización o bien enviar la aplicación al origen de la aplicación para todos los usuarios de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="53b24-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="53b24-168">✔ El administrador de ti consultará estos envíos.</span><span class="sxs-lookup"><span data-stu-id="53b24-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="53b24-169">✔ Puede volver a la página **publicar** para comprobar el estado del envío y saber si su administrador de ti aprobó o rechazó la aplicación. Aquí también puede ir a enviar actualizaciones a la aplicación o cancelar los envíos actualmente activos.</span><span class="sxs-lookup"><span data-stu-id="53b24-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53b24-170">Siguiente paso: mantenimiento y soporte de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="53b24-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>