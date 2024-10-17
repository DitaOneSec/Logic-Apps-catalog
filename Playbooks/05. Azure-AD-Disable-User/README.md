# Azure-AD-Disable-User

Para cualquier duda técnica consulte a dfernandezm@onesec.mx

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Disable-User%2Fazuredeploy.json)


This playbook está pensado para ejecutarse desde un incidente de Microsoft Sentinel. Deshabilitará las cuentas de usuario de Azure AD asociadas con las entidades de los incidentes de Microsoft Sentinel.

![Azure_AD_Disable_User_Demo_1](Images/Azure_AD_Disable_User_Demo_1.png)


#
### Despliegue

Para configurar e implementar este manual:

Abra su navegador y asegúrese de haber iniciado sesión en su espacio de trabajo de Microsoft Sentinel

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FAS-Azure-AD-Disable-User%2Fazuredeploy.json)

Haga clic en el botón “**Deploy to Azure**” en la parte inferior y lo llevará a la plantilla de implementación personalizada.

En la sección **Project details** :

* Elija la **Subscription** y **Resource group** de los cuadros desplegables  

En la sección **Instance details** :  
                                                  
* **Playbook Name**: puede dejarlo como "**AS-Azure-AD-Disable-User**" o puede cambiarlo. 

Hacia la parte inferior, haga clic en "**Review + create**". 

![Azure_AD_Disable_User_Deploy_1](Images/Azure_AD_Disable_User_Deploy_1.png)

Una vez validados los recursos, haga clic en "**Create**".

![Azure_AD_Disable_User_Deploy_2](Images/Azure_AD_Disable_User_Deploy_2.png)

Los recursos deberían tardar alrededor de un minuto en implementarse. Una vez que se complete la implementación, puede expandir la sección "**Deployment details**"  para verlos. Haga clic en el que corresponda a la logic app.


![Azure_AD_Disable_User_Deploy_3](Images/Azure_AD_Disable_User_Deploy_3.png)

Haga clic en el botón "**Edit**" button.. Esto nos llevará al Diseñador de la logic app 


![Azure_AD_Disable_User_Deploy_4](Images/Azure_AD_Disable_User_Deploy_4.png)

Antes de poder ejecutar el playbook, será necesario autorizar la conexión de Azure AD en el paso indicado o, alternativamente, se puede seleccionar una conexión autorizada existente. Esta conexión se puede encontrar en el tercer paso denominado "**For each**".

![Azure_AD_Disable_User_Deploy_5](Images/Azure_AD_Disable_User_Deploy_5.png)

Expande el paso "**Connections**" y haz clic en el ícono del signo de exclamación junto al nombre que coincide con el playbook.
                                                                                                
![Azure_AD_Disable_User_Deploy_6](Images/Azure_AD_Disable_User_Deploy_6.png)

Cuando se le solicite, inicie sesión para validar la conexión.                                                                                              
![Azure_AD_Disable_User_Deploy_7](Images/Azure_AD_Disable_User_Deploy_7.png)
