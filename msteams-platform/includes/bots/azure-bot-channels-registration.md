1. En [Azure portal](https://ms.portal.azure.com/#home), en servicios de Azure, seleccione **crear un recurso**.
1. En el cuadro Buscar, escriba "bot". En la lista desplegable, seleccione Registro de **canales de bot**.
1. Seleccione el botón **crear** .
1. En la hoja de **registro del canal del bot** , especifique la información solicitada sobre el bot.
1. Deje el cuadro **extremo de mensajería** vacío por ahora, escribirá la dirección URL necesaria después de implementar el bot. En la siguiente imagen se muestra un ejemplo de la configuración de registro:

    ![registro de canales de aplicación de bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Haga clic en **identificador y contraseña de Microsoft App** y, a continuación, **cree un nuevo**.
1. Haga clic en **Crear identificador de aplicación en el vínculo portal de registro de aplicaciones** .
1. En la ventana de registro de la **aplicación** que aparece, haga clic en la pestaña **registro nuevo** en la parte superior izquierda.
1. Escriba el nombre de la aplicación de bot que está registrando, hemos usado *BotTeamsAuth* (debe seleccionar su propio nombre único).
1. Para los **tipos de cuenta admitidos** , seleccione *cuentas en cualquier directorio de la organización (cualquier directorio de Azure ad-multiinquilino) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox)*.
1. Haga clic en el botón **registrar** . Una vez completado, Azure muestra la página de *información general* de la aplicación.
1. Copiar y guardar en un archivo el valor del identificador de la **aplicación (cliente)** .
1. En el panel izquierdo, haga clic en **certificado y secretos**.
    1. En *clientes secretos*, haga clic en **nuevo secreto de cliente**.
    1. Agregue una descripción para identificar este secreto con respecto a otros que puede que tenga que crear para esta aplicación.
    1. El valor establecido *expira* en la selección.
    1. Haga clic en **Agregar**.
    1. Copie el secreto de cliente y guárdelo en un archivo.
1. Vuelva a la ventana de **registro del canal de bot** y copie el identificador de *aplicación* y el secreto de *cliente* en los cuadros identificador de aplicación y **contraseña** de **Microsoft** , respectivamente.
1. Haga clic en **Aceptar**.
1. Por último, haga clic en **crear**.

Una vez que Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.  

![Grupo de registro de canales de aplicación de bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

Una vez que se haya creado el registro de los canales de bot, deberá habilitar el canal de Teams.

1. En [Azure portal](https://ms.portal.azure.com/#home), en servicios de Azure, seleccione el **registro del canal de bot** que acaba de crear.
1. En el panel izquierdo, haga clic en **canales**.
1. Haga clic en el icono de Microsoft Teams y elija **Guardar**.
