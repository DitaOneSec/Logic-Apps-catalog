# Get-VTURLPositivesComment

## Descripción
Este playbook está diseñado para integrarse con Microsoft Sentinel y proporcionar una respuesta automática a incidentes relacionados con URLs maliciosas detectadas. Utiliza la API de VirusTotal para analizar URLs y registrar el número total de detecciones positivas como un comentario en el incidente.

## Funcionalidad
Al activarse por un incidente que incluye una URL, este playbook:
- Consulta la API de VirusTotal.
- Obtiene y registra el número de detecciones positivas.
- Añade un comentario en el incidente dentro de Microsoft Sentinel.
- Notifica al equipo de seguridad mediante Microsoft Teams si se configura.

## Configuración
### Prerrequisitos
- Una cuenta de Azure con acceso a Microsoft Sentinel.
- Una clave de API de VirusTotal. Obtén una clave en: [VirusTotal](https://www.virustotal.com/gui/join-us)

### Parámetros Requeridos
- `Region`: La región en la que se despliega el playbook.
- `Playbook Name`: El nombre asignado al playbook.
- `User Name`: Utilizado para pre-configurar el nombre de usuario en las conexiones de Azure.

### Pasos de instalación
1. Desplegar el playbook utilizando uno de los siguientes botones, según corresponda:
   
   [![Desplegar en Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FGet-VTURLPositivesComment%2Fazuredeploy.json)

   [![Desplegar en Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FPlaybooks%2FGet-VTURLPositivesComment%2Fazuredeploy.json)

2. Una vez desplegado, ingresar a la Logic App en Azure y completar los pasos de autenticación para cada conexión necesaria. Los pasos que requieran atención mostrarán un signo de exclamación.

### Configuración de Conexiones
Cada paso de la Logic App que requiera una conexión autenticada indicará específicamente cómo y dónde completar esta información. Generalmente, se requiere la intervención manual para asegurar que las credenciales sean correctas y estén actualizadas.

## Uso
Una vez configurado, el playbook operará automáticamente en respuesta a los incidentes generados en Microsoft Sentinel que incluyan URLs. No se requieren pasos adicionales para su operación rutinaria.

## Soporte
Para obtener soporte técnico o resolver dudas sobre la configuración y operación de este playbook, por favor dirígete al [Foro de Microsoft Azure](https://techcommunity.microsoft.com/t5/azure/ct-p/Azure).

## Contribuciones
Las contribuciones a este playbook son bienvenidas. Por favor, revisa el proceso de contribución en la documentación oficial de Microsoft Sentinel antes de enviar cualquier cambio.
