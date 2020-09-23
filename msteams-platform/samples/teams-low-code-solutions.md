---
title: Soluciones de código de bajo nivel para aplicaciones personalizadas de Teams
author: laujan
description: Detalle de soluciones de código bajo y sin código de Microsoft disponibles para Microsoft Teams
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 4b112a674df76d0bd33e1b461d6b2f194f764f7b
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210347"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a><span data-ttu-id="a86ca-103">Crear aplicaciones personalizadas de bajo código para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a86ca-103">Create low-code custom apps for Microsoft Teams</span></span>

<span data-ttu-id="a86ca-104">[Microsoft Teams](/microsoftteams/platform) es tanto extensible como adaptable.</span><span class="sxs-lookup"><span data-stu-id="a86ca-104">[Microsoft Teams](/microsoftteams/platform) is both extensible and adaptive.</span></span> <span data-ttu-id="a86ca-105">Esto significa que tiene la libertad de crear aplicaciones personalizadas para Teams que cumplan las distintas necesidades de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a86ca-105">This means that you have the freedom to build custom applications for Teams that meet the distinct needs of your users.</span></span> <span data-ttu-id="a86ca-106">Aunque puede crear aplicaciones desde cero, con la demanda actual de soluciones rápidas, una opción de bajo código puede ser tan solo lo que necesita para crear aplicaciones elegantes en un intervalo de tiempo comprimido.</span><span class="sxs-lookup"><span data-stu-id="a86ca-106">Although you can create apps from scratch, with today's demand for speedy solutions, a low-code option may be just what you need to build elegant apps within a compressed time frame.</span></span>

<span data-ttu-id="a86ca-107">Las plataformas de código de bajo rendimiento proporcionan un enfoque intuitivo para el desarrollo de software y requieren poca o ninguna codificación para crear aplicaciones y procesos.</span><span class="sxs-lookup"><span data-stu-id="a86ca-107">Low code platforms provide an intuitive approach to software development and require little or no coding to build applications and processes.</span></span> <span data-ttu-id="a86ca-108">Los desarrolladores de ciudadanos están habilitados para crear fácilmente aplicaciones personalizadas y desarrolladores profesionales que puedan acelerar el proceso de implementación y desarrollo de aplicaciones exponencialmente.</span><span class="sxs-lookup"><span data-stu-id="a86ca-108">Citizen developers are enabled to easily build custom apps and professional developers can accelerate the app development and deployment process exponentially.</span></span> <span data-ttu-id="a86ca-109">La mayoría de las plataformas de código insuficiente constan de una interfaz visual, conectores para servicios back-end y un sistema de administración del ciclo de vida de aplicaciones integrado para crear, depurar, implementar y mantener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a86ca-109">Most low-code platforms consist of a visual interface, connectors to back-end services, and a built in app lifecycle management system to build, debug, deploy and maintain applications.</span></span> <span data-ttu-id="a86ca-110">Microsoft proporciona varias puertas de enlace innovadoras para crear rápidamente aplicaciones compatibles con Teams con atributos de bajo código:</span><span class="sxs-lookup"><span data-stu-id="a86ca-110">Microsoft provides several innovative gateways to rapidly build great Teams-compatible apps using low-code attributes:</span></span>

1. [<span data-ttu-id="a86ca-111">Plataforma de energía de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a86ca-111">Microsoft Power Platform</span></span>](#teams-and-microsoft-power-platform)
1. [<span data-ttu-id="a86ca-112">Plantillas de aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a86ca-112">Microsoft Teams app templates</span></span>](#teams-app-templates)

## <a name="teams-and-microsoft-power-platform"></a><span data-ttu-id="a86ca-113">Teams y Microsoft Power Platform</span><span class="sxs-lookup"><span data-stu-id="a86ca-113">Teams and Microsoft Power Platform</span></span>

<span data-ttu-id="a86ca-114">Microsoft Power Platform (/Power-Platform) combina cuatro tecnologías sólidas de Microsoft en una sola plataforma de aplicaciones eficaz.</span><span class="sxs-lookup"><span data-stu-id="a86ca-114">Microsoft Power Platform(/power-platform) combines four robust Microsoft technologies in one powerful application platform.</span></span> <span data-ttu-id="a86ca-115">Power BI, Power Apps, Power automaticing (anteriormente Microsoft Flow) y Power virtual Agents le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales en un entorno unificado e integrado:</span><span class="sxs-lookup"><span data-stu-id="a86ca-115">Power BI, Power Apps, Power Automate (formerly Microsoft Flow) and Power Virtual Agents empower you to build solutions, automate processes, analyze data,  and create virtual agents within a unified and integrated environment:</span></span>

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Servicios de plataforma de alimentación":::

### <a name="-teams-and-power-bi"></a><span data-ttu-id="a86ca-117">✔ Teams y Power BI</span><span class="sxs-lookup"><span data-stu-id="a86ca-117">✔ Teams and Power BI</span></span>

<span data-ttu-id="a86ca-118">La [pestaña Power BI para Microsoft Teams](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) agrega compatibilidad con informes en el área de trabajo de Microsoft Teams y permite a los usuarios [compartir contenido interactivo de Power BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams) y [colaborar con otros](/power-bi/collaborate-share/service-collaborate-microsoft-teams) canales y chats de equipos interactivos.</span><span class="sxs-lookup"><span data-stu-id="a86ca-118">The [Power BI tab for Microsoft Teams](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) adds support for reports in the Teams workspace and allows users to [share interactive Power BI content](/power-bi/collaborate-share/service-embed-report-microsoft-teams) and [collaborating with others inTeams](/power-bi/collaborate-share/service-collaborate-microsoft-teams) channels and chats.</span></span> <span data-ttu-id="a86ca-119">Puede crear contenido empaquetado de [aplicaciones de Power BI](/power-bi/collaborate-share/service-create-distribute-apps) desde cero y distribuirlo como una aplicación o puede [crear una aplicación de plantilla en Power BI](/connect-data/service-template-apps-create).</span><span class="sxs-lookup"><span data-stu-id="a86ca-119">You can create packaged [Power BI app](/power-bi/collaborate-share/service-create-distribute-apps) content from scratch and distribute as an app or you can [Create a template app in Power BI](/connect-data/service-template-apps-create).</span></span> <span data-ttu-id="a86ca-120">Además, use la nueva [aplicación de Power BI en Teams](https://go.microsoft.com/fwlink/?linkid=2143643) para llevar toda la experiencia básica del servicio de Power BI a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-120">Additionally, use the new [Power BI app in Teams](https://go.microsoft.com/fwlink/?linkid=2143643) to bring your entire basic Power BI service experience into Teams.</span></span>

### <a name="-teams-and-power-apps"></a><span data-ttu-id="a86ca-121">✔ Teams y Power apps</span><span class="sxs-lookup"><span data-stu-id="a86ca-121">✔ Teams and Power Apps</span></span>

<span data-ttu-id="a86ca-122">Con [Power apps](/powerapps/powerapps-overview), puede crear aplicaciones empresariales que se conecten a los datos profesionales y que se adapten a las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="a86ca-122">With [Power Apps](/powerapps/powerapps-overview), you can build business apps that connect to your business data and are tailored to your organization's  needs.</span></span>  <span data-ttu-id="a86ca-123">Power apps permite una amplia variedad de escenarios de aplicaciones para resolver los desafíos empresariales a través de las [aplicaciones de canvas](/powerapps/maker/#canvas-apps).</span><span class="sxs-lookup"><span data-stu-id="a86ca-123">Power Apps enables a wide range of app scenarios to solve business challenges via [canvas apps](/powerapps/maker/#canvas-apps).</span></span> <span data-ttu-id="a86ca-124">Una vez que se ha creado la aplicación, se puede exportar desde el portal de Power App Maker e [incrustada en Microsoft Teams](/power-platform/admin/embed-app-teams).</span><span class="sxs-lookup"><span data-stu-id="a86ca-124">Once your app is built, it can be exported from the Power Apps maker portal and [embedded in Microsoft Teams](/power-platform/admin/embed-app-teams).</span></span>

<span data-ttu-id="a86ca-125">La nueva [aplicación Power apps](https://go.microsoft.com/fwlink/?linkid=2143374) en Microsoft Teams proporciona una experiencia integrada para los responsables de las aplicaciones para crear y editar aplicaciones y flujos de trabajo dentro de Microsoft Teams, y publicarlos y compartirlos rápidamente para que los usuarios del equipo los usen sin tener que cambiar entre varias aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="a86ca-125">The new [Power Apps app](https://go.microsoft.com/fwlink/?linkid=2143374) in Teams provides an integrated experience for app makers to create and edit apps and workflows within Teams and quickly publish and share them for anyone on the team to use without having to switch between multiple apps and services.</span></span>

### <a name="-teams-and-power-automate"></a><span data-ttu-id="a86ca-126">✔ Teams y automatización de la energía</span><span class="sxs-lookup"><span data-stu-id="a86ca-126">✔ Teams and Power Automate</span></span>

<span data-ttu-id="a86ca-127">Con la [aplicación Automated Power en Teams](/power-automate/flows-teams), puede [crear flujos para automatizar tareas de trabajo repetitivas](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) directamente en el entorno de Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-127">With the [Power Automate app in Teams](/power-automate/flows-teams), you can [create flows to automate repetitive work tasks](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) directly within the Teams environment.</span></span> <span data-ttu-id="a86ca-128">Puede [desencadenar un flujo de cualquier mensaje en Microsoft Teams](/power-automate/trigger-flow-teams-message) y [usar tarjetas adaptables dentro de la automatización](/power-automate/create-adaptive-cards)de la energía.</span><span class="sxs-lookup"><span data-stu-id="a86ca-128">You can [trigger a flow from any message in Microsoft Teams](/power-automate/trigger-flow-teams-message) and [use adaptive cards within Power Automate](/power-automate/create-adaptive-cards).</span></span> <span data-ttu-id="a86ca-129">Además, puede crear flujos para personalizar y agregar más valor a Microsoft Teams desde la nueva [aplicación Power apps](https://go.microsoft.com/fwlink/?linkid=2143539) en Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-129">Additionally, you can build flows to customize and add further value to Microsoft Teams from within the new [Power Apps app](https://go.microsoft.com/fwlink/?linkid=2143539) in Teams.</span></span>

### <a name="-teams-and-power-virtual-agents"></a><span data-ttu-id="a86ca-130">✔ De equipos y agentes virtuales de Power</span><span class="sxs-lookup"><span data-stu-id="a86ca-130">✔ Teams and Power Virtual Agents</span></span>

<span data-ttu-id="a86ca-131">[Power virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es una solución de interfaz gráfica guiada sin código, integrada en Microsoft Power Platform y bot Framework, que permite a todos los miembros de su equipo crear y mantener chatbotss de conversación enriquecidas que se integren fácilmente con la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-131">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a no-code, guided graphical interface solution, built on the Microsoft Power Platform and the Bot Framework, that empowers every member of your team to create and maintain rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="a86ca-132">Todo el contenido creado por los agentes de Power virtual se representa de forma natural en Teams y los bots de los agentes virtuales de energía, se relaciona con los usuarios del lienzo de chat nativo de Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-132">All content authored in Power Virtual Agents renders naturally in Teams and Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="a86ca-133">Puede [integrar el Chatbot de agentes de Power virtual](/power-virtual-agents/publication-add-bot-to-microsoft-teams) en Microsoft Teams a través del [portal de Power virtual Agents](https://powervirtualagents.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a86ca-133">You can [integrate your Power Virtual Agents chatbot](/power-virtual-agents/publication-add-bot-to-microsoft-teams) to Teams via the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com).</span></span>

<span data-ttu-id="a86ca-134">Con la nueva [aplicación de agentes de Power Virtual Agent](https://aka.ms/pva-teams-docs) en Teams, puede crear, administrar y publicar fácilmente conversaciones Chatbots desde Microsoft Teams y compartir los bots con otras personas de la organización para que puedan chatear y tengan respuestas a sus preguntas.</span><span class="sxs-lookup"><span data-stu-id="a86ca-134">With the new [Power Virtual Agents app](https://aka.ms/pva-teams-docs) in Teams, you can create, manage, and publish conversational chatbots easily from within Teams and share your bots with other people in your organization so they can chat and have their questions answered.</span></span>

## <a name="teams-app-templates"></a><span data-ttu-id="a86ca-135">Plantillas de aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a86ca-135">Teams app templates</span></span>

:::image type="content" source="../assets/images/power-platform-and-teams/app-template-illustration.png" alt-text="Ilustración de la solución de la aplicación":::

### <a name="-app-template-catalog"></a><span data-ttu-id="a86ca-137">Catálogo de plantillas de aplicaciones de ✔</span><span class="sxs-lookup"><span data-stu-id="a86ca-137">✔ App template catalog</span></span>

<span data-ttu-id="a86ca-138">[Las plantillas de aplicación](../samples/app-templates.md) son aplicaciones de producción listas para Microsoft teams que se pueden controlar desde la comunidad, desde código abierto y están disponibles en github.</span><span class="sxs-lookup"><span data-stu-id="a86ca-138">[App templates](../samples/app-templates.md) are production-ready apps for Microsoft Teams that are community driven, open-source, and available on GitHub.</span></span> <span data-ttu-id="a86ca-139">Cada plantilla contiene instrucciones detalladas para implementar e instalar esa aplicación en su organización, ya que proporciona una aplicación lista para usar que puede instalar y empezar a usar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="a86ca-139">Each template contains detailed instructions for deploying and installing that app for your organization, providing a ready-to-use app that you can install and begin using immediately.</span></span> <span data-ttu-id="a86ca-140">También está disponible el código fuente completo, de modo que puede explorarlo en detalle o bifurcar el código y modificarlo para satisfacer sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="a86ca-140">The complete source code is available as well, so you can explore it in detail, or fork the code and alter it to meet your specific needs.</span></span>

### <a name="-virtual-assistant-for-teams"></a><span data-ttu-id="a86ca-141">✔ Asistente virtual para Teams</span><span class="sxs-lookup"><span data-stu-id="a86ca-141">✔ Virtual Assistant for Teams</span></span>

<span data-ttu-id="a86ca-142">Asistente Virtual es una plantilla de código abierto de Microsoft que le permite crear una solución de conversación robusta y mantener un control total sobre la experiencia del usuario, la personalización de marca organizacional y los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="a86ca-142">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="a86ca-143">Puede configurar el asistente virtual para [la integración en el entorno de Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro).</span><span class="sxs-lookup"><span data-stu-id="a86ca-143">You can configure your virtual assistant for [integration into the Teams environment](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a86ca-144">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a86ca-144">Additional Resources</span></span>

:::image type="content" source="../assets/images/power-platform-and-teams/blogs-and-resources.png" alt-text="Ilustración de blogs y recursos":::

### <a name="-teams-shift-connectors"></a><span data-ttu-id="a86ca-146">Conectores de cambio de ✔ Teams</span><span class="sxs-lookup"><span data-stu-id="a86ca-146">✔ Teams Shift Connectors</span></span>

<span data-ttu-id="a86ca-147">Los [equipos cambian los conectores de administración](../samples/shifts-wfm-connectors.md) de la fuerza de trabajo son integraciones integradas de producción, de código abierto y basadas en la comunidad que ofrecen una experiencia y un proceso rápido sin problemas para la transformación digital de los trabajadores de Firstline con turnos de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-147">[Teams Shifts Work Force Management connectors](../samples/shifts-wfm-connectors.md) are production-ready, open-source, and community-driven integrations that offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> <span data-ttu-id="a86ca-148">Cada conector proporciona una guía detallada para la implementación y la integración en la organización.</span><span class="sxs-lookup"><span data-stu-id="a86ca-148">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="a86ca-149">El código fuente completo está disponible en nuestro repositorio de GitHub, donde se puede explorar en detalle o bifurcado y adaptarlo a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="a86ca-149">The complete source code is available in our GitHub repo where it can be explored in detail and/or forked and tailored to meet your specific needs.</span></span>

### <a name="-power-platform-learn-modules"></a><span data-ttu-id="a86ca-150">Módulos de aprendizaje de ✔ Power Platform</span><span class="sxs-lookup"><span data-stu-id="a86ca-150">✔ Power Platform Learn modules</span></span>

|<span data-ttu-id="a86ca-151">Tema</span><span class="sxs-lookup"><span data-stu-id="a86ca-151">Topic</span></span>|
|-----|
|<span data-ttu-id="a86ca-152">**Power BI**</span><span class="sxs-lookup"><span data-stu-id="a86ca-152">**Power BI**</span></span>|
|[<span data-ttu-id="a86ca-153">Power BI para responsables de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a86ca-153">Power BI for App Makers</span></span>](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)|
|[<span data-ttu-id="a86ca-154">Power BI para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="a86ca-154">Power BI for Developers</span></span>](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|<span data-ttu-id="a86ca-155">**Power Apps**</span><span class="sxs-lookup"><span data-stu-id="a86ca-155">**Power Apps**</span></span>|
|[<span data-ttu-id="a86ca-156">Power apps para los responsables de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a86ca-156">Power Apps for app makers</span></span>](/learn/browse/?products=power-apps&roles=maker)|
|[<span data-ttu-id="a86ca-157">Power apps para desarrolladores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a86ca-157">Power Apps for app developers</span></span>](/learn/browse/?products=power-apps)|
|<span data-ttu-id="a86ca-158">**Power Automate**</span><span class="sxs-lookup"><span data-stu-id="a86ca-158">**Power Automate**</span></span>|
|[<span data-ttu-id="a86ca-159">Automatizar la alimentación para los responsables de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a86ca-159">Power Automate for App Makers</span></span>](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)|
|[<span data-ttu-id="a86ca-160">Automatizar la alimentación para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="a86ca-160">Power Automate for Developers</span></span>](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|<span data-ttu-id="a86ca-161">**Power Virtual Agents**</span><span class="sxs-lookup"><span data-stu-id="a86ca-161">**Power Virtual Agents**</span></span>|
|[<span data-ttu-id="a86ca-162">Agentes de Power virtual para los responsables de aplicaciones y desarrolladores</span><span class="sxs-lookup"><span data-stu-id="a86ca-162">Power Virtual Agents for App Makers and Developers</span></span>](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)

### <a name="-project-oakdale-preview"></a><span data-ttu-id="a86ca-163">✔ Project Oakdale (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a86ca-163">✔ Project Oakdale (preview)</span></span>

<span data-ttu-id="a86ca-164">[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) es una nueva plataforma de datos de bajo código para la próxima vez en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-164">[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) is a new low-code data platform for coming soon to Microsoft Teams.</span></span> <span data-ttu-id="a86ca-165">Permitirá a los desarrolladores crear soluciones de plataforma de energía directamente en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a86ca-165">It will allow developers to create Teams Power Platform solutions directly within Teams.</span></span> <span data-ttu-id="a86ca-166">*Vea* la [Página de Microsoft Project Oakdale del blog de Microsoft Teams](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a86ca-166">*See* our [Teams Blog Microsoft Project Oakdale page](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams) for more information.</span></span>

### <a name="-microsoft-blog-insights"></a><span data-ttu-id="a86ca-167">✔ De información del blog de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a86ca-167">✔ Microsoft Blog insights</span></span>

[<span data-ttu-id="a86ca-168">Una visión más detallada de las capacidades de la plataforma de datos en Project Oakdale</span><span class="sxs-lookup"><span data-stu-id="a86ca-168">A Closer Look at Data Platform Capabilities in Project Oakdale</span></span>](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[<span data-ttu-id="a86ca-169">Anuncio de las actualizaciones de plataformas de energía y Teams para ayudar a los clientes a adaptarse a la tarea remota</span><span class="sxs-lookup"><span data-stu-id="a86ca-169">Announcing Power Platform and Teams updates to help customers adapt to remote work</span></span>](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[<span data-ttu-id="a86ca-170">Teams está modelando el futuro del trabajo con características de bajo código para mejorar el área de trabajo digital</span><span class="sxs-lookup"><span data-stu-id="a86ca-170">Teams is shaping the future of work with low code features to enhance your digital workspace</span></span>](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)