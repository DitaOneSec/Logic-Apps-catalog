# Azure-AD-Disable-User


Para cualquier consulta técnica, por favor contacta a dfernandezm@onesec.mx

[![Desplegar en Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Disable-User%2Fazuredeploy.json)
[![Desplegar en Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Disable-User%2Fazuredeploy.json)

Este playbook está diseñado para ejecutarse desde un incidente de Microsoft Sentinel. Deshabilita las cuentas de usuario de Azure AD asociadas con las entidades de incidentes de Microsoft Sentinel. Este playbook se utiliza en conjunto con nuestro playbook [AS-Azure-AD-Enable-User](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/AS-Azure-AD-Enable-User).

![Azure_AD_Disable_User_Demo_1](Images/Azure_AD_Disable_User_Demo_1.png)

#
### Despliegue

Para configurar y desplegar este playbook:

1. Haz clic en el botón "**Desplegar en Azure**" ubicado abajo y te llevará a la plantilla de despliegue personalizada.

3. En la sección **Detalles del proyecto**:
   - Selecciona la **Suscripción** y el **Grupo de recursos** desde las cajas desplegables a las que te gustaría que se desplegara el playbook.

4. En la sección **Detalles de la instancia**:
   - **Nombre del Playbook**: Puede dejarse como "**AS-Azure-AD-Disable-User**" o puedes cambiarlo.

5. Hacia el fondo, haz clic en "**Revisar + crear**".

   ![Azure_AD_Disable_User_Deploy_1](Images/Azure_AD_Disable_User_Deploy_1.png)

6. Una vez que los recursos hayan sido validados, haz clic en "**Crear**".

   ![Azure_AD_Disable_User_Deploy_2](Images/Azure_AD_Disable_User_Deploy_2.png)

7. Los recursos tardarán aproximadamente un minuto en desplegarse. Una vez completado el despliegue, puedes expandir la sección "**Detalles del despliegue**" para verlos.
   Haz clic en el correspondiente a la Logic App.

   ![Azure_AD_Disable_User_Deploy_3](Images/Azure_AD_Disable_User_Deploy_3.png)

8. Haz clic en el botón "**Editar**". Esto nos llevará al Diseñador de Logic Apps.

   ![Azure_AD_Disable_User_Deploy_4](Images/Azure_AD_Disable_User_Deploy_4.png)

9. Antes de que se pueda ejecutar el playbook, la conexión de Azure AD deberá ser autorizada en el paso indicado, o se puede seleccionar una conexión autorizada existente. Esta conexión se encuentra bajo el tercer paso etiquetado como "**Para cada**".

   ![Azure_AD_Disable_User_Deploy_5](Images/Azure_AD_Disable_User_Deploy_5.png)

10. Expande el paso de "**Conexiones**" y haz clic en el icono de signo de exclamación junto al nombre que coincide con el playbook.

    ![Azure_AD_Disable_User_Deploy_6](Images/Azure_AD_Disable_User_Deploy_6.png)

11. Cuando se te solicite, inicia sesión para validar la conexión.

    ![Azure_AD_Disable_User_Deploy_7](Images/Azure_AD_Disable_User_Deploy_7.png)

**Autor**: Adaptación a playbook creado por Accelerynt
