

# Acerca de este catálogo de Logic Apps

Este repositorio contiene ejemplos de flujos de trabajo de automatización y respuesta de seguridad, diseñados para mejorar las operaciones de ciberseguridad. Cada carpeta incluye una plantilla ARM de un flujo de trabajo que se activa utilizando un desencadenador de Microsoft Sentinel.

## Instrucciones para implementar una plantilla personalizada

Después de seleccionar un flujo de trabajo en el portal de Azure:

1. Busca "Implementar una plantilla personalizada".
2. Haz clic en "Crear tu propia plantilla en el editor".
3. Pega el contenido del flujo de trabajo desde GitHub.
4. Haz clic en "Guardar".
5. Completa los datos necesarios y haz clic en "Comprar".
6. Una vez completada la implementación, deberás autorizar cada conexión.

   - Haz clic en el recurso de conexión de Microsoft Sentinel.
   - Haz clic en "Editar conexión API".
   - Haz clic en "Autorizar".
   - Inicia sesión.
   - Haz clic en "Guardar".
   - Repite los pasos para otras conexiones.

Para el "Azure Log Analytics Data Collector", deberás añadir el ID del área de trabajo y la clave. Ahora puedes editar el flujo de trabajo en Logic Apps.

## Instrucciones para convertir un flujo de trabajo en una plantilla

### Opción 1: Generador de Plantillas ARM para Logic App/Flujos de Trabajo

1. Descarga la herramienta y ejecuta el script de PowerShell.

[![Download](./src/Download.png)](https://aka.ms/Playbook-ARM-Template-Generator)  
   
2. Extrae la carpeta y abre el archivo `Playbook_ARM_Template_Generator.ps1` en Visual Studio Code, Windows PowerShell o PowerShell Core.

**Nota:** El script se ejecuta desde la máquina del usuario. Debes permitir la ejecución de scripts en PowerShell. Para hacerlo, ejecuta el siguiente comando:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

3. Después de autenticarse, deberás seleccionar:

- **Suscripción**
- **Flujos de trabajo**

Luego de seleccionar los flujos de trabajo, el script te pedirá que elijas la ubicación en tu unidad local para guardar la plantilla ARM.

**Nota:** La herramienta convierte las conexiones de Microsoft Sentinel a MSI durante la exportación.

### Opción 2: Manual

Una vez que hayas creado un flujo de trabajo que deseas exportar para compartir, dirígete al recurso de Logic App en Azure.

**Nota:** Estas son instrucciones genéricas; pueden existir otros pasos dependiendo de la complejidad del flujo de trabajo o de los conectores utilizados.

1. **Haz clic en** "Exportar plantilla" desde el menú de recursos en el portal de Azure.
2. **Copia** el contenido de la plantilla.
3. **Utiliza** VS Code para crear un archivo JSON con el nombre `azuredeploy.json`.
4. **Pega** el código en el nuevo archivo.
5. En la sección de parámetros, puedes eliminar todos los parámetros y agregar los siguientes campos mínimos. Los usuarios podrán editar los parámetros al implementar tu plantilla. Puedes añadir más parámetros según los requisitos de tu flujo de trabajo.

   ```json
   "parameters": {
       "PlaybookName": {
           "defaultValue": "<PlaybookName>",
           "type": "string"
       },
       "UserName": {
           "defaultValue": "<username>@<domain>",
           "type": "string"
       }
   }
   ```

El nombre del flujo de trabajo y el nombre de usuario son requisitos mínimos que se usarán para las conexiones.

6. En la sección de variables, crea una variable para cada conexión que el flujo de trabajo esté utilizando. Para construir una variable de cadena, utiliza el siguiente fragmento. Asegúrate de reemplazar connectorname con el nombre real del conector.

```json
[concat('<connectorname>-', parameters('PlaybookName'))]
```

Por ejemplo, si estás utilizando conexiones de Azure Active Directory y Microsoft Sentinel en el flujo de trabajo, crea dos variables con los nombres reales de las conexiones. Las variables serán los nombres de las conexiones. Aquí estamos creando un nombre de conexión usando la conexión (AzureAD) y "-" y el nombre del flujo de trabajo.

```json
"variables": {
    "AzureADConnectionName": "[concat('azuread-', parameters('PlaybookName'))]",
    "AzureSentinelConnectionName": "[concat('azuresentinel-', parameters('PlaybookName'))]"
}

```
7. A continuación, añade recursos que se crearán para cada conexión.

```json
"resources": [
    {
        "type": "Microsoft.Web/connections",
        "apiVersion": "2016-06-01",
        "name": "[variables('AzureADConnectionName')]",
        "location": "[resourceGroup().location]",
        "properties": {
            "displayName": "[parameters('UserName')]",
            "customParameterValues": {},
            "api": {
                "id": "[concat('/subscriptions/', subscription().subscriptionId, '/providers/Microsoft.Web/locations/', resourceGroup().location, '/managedApis/azuread')]"
            }
        }
    }
]
```
* El nombre usa la variable que creamos.
* La ubicación utiliza el grupo de recursos seleccionado como parte de la implementación.
* El displayName utiliza el parámetro de nombre de usuario.
* Por último, puedes construir la cadena para el ID usando cadenas más propiedades de la suscripción y el grupo de recursos.
Repite estos pasos para cada conexión necesaria.

8. En el recurso `Microsoft.Logic/workflows` bajo parameters / $connections, habrá un valor para cada conexión. Actualiza cada uno como se muestra a continuación.

9. En el recurso `Microsoft.Logic/workflows` bajo parameters / $connections, habrá un valor para cada conexión. Actualiza cada uno como se muestra a continuación.
```json
"parameters": {
    "$connections": {
        "value": {
            "azuread": {
                "connectionId": "[resourceId('Microsoft.Web/connections', variables('AzureADConnectionName'))]",
                "connectionName": "[variables('AzureADConnectionName')]",
                "id": "[concat('/subscriptions/', subscription().subscriptionId, '/providers/Microsoft.Web/locations/', resourceGroup().location, '/managedApis/azuread')]"
            },
            "azuresentinel": {
                "connectionId": "[resourceId('Microsoft.Web/connections', variables('AzureSentinelConnectionName'))]",
                "connectionName": "[variables('AzureSentinelConnectionName')]",
                "id": "[concat('/subscriptions/', subscription().subscriptionId, '/providers/Microsoft.Web/locations/', resourceGroup().location, '/managedApis/azuresentinel')]"
            }
        }
    }
}
```
* El `connectionId` usará una cadena y una variable.
* El `connectionName` es la variable.
* El ID es la cadena que usamos anteriormente para el ID al crear el recurso.
* 
En el recurso `Microsoft.Logic/workflows`, también necesitarás el campo `dependsOn`, que es una lista de `resourceId`. La cadena para cada `resourceId` se construye utilizando este fragmento, seguido de un ejemplo que contiene conexiones de Azure AD y Azure Sentinel.

En el recurso Microsoft.Logic/workflows, también necesitarás el campo `dependsOn`, que es una lista de resourceId. La cadena para cada resourceId se construye utilizando este fragmento, seguido de un ejemplo que contiene conexiones de Azure AD y Azure Sentinel.

```json
resourceId('Microsoft.Web/connections', <ConnectionVariableName>)]
```
```json
"dependsOn": [
    "[resourceId('Microsoft.Web/connections', variables('AzureADConnectionName'))]",
    "[resourceId('Microsoft.Web/connections', variables('AzureSentinelConnectionName'))]"
]
```
10. Guarda el archivo JSON.

11. Crea un archivo Readme.md con una breve descripción del flujo de trabajo.

12. Prueba la implementación de tu plantilla siguiendo las instrucciones para implementar una plantilla personalizada. Asegúrate de que la implementación se realice correctamente.

13. Si necesitas ejemplos de una plantilla de flujo de trabajo, consulta el archivo azuredeploy.json de flujos de trabajo existentes en el repositorio.

Información tomada, traducida y adaptada de [v-atulyadav en GitHub](https://github.com/v-atulyadav).


