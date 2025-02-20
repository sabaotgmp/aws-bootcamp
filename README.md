# Infraestructura AWS con CloudFormation

Este proyecto utiliza AWS CloudFormation para desplegar una infraestructura básica en AWS. La plantilla crea los siguientes recursos:

## Recursos creados

1. **VPC (Red Virtual Privada)**

   - Red principal con un rango de direcciones IP `10.0.0.0/16`.
   - Soporte para nombres de dominio DNS y resolución de nombres.

2. **Subredes**

   - **Subred Pública** (`10.0.1.0/24`): Permite acceso a Internet.
   - **Subred Privada** (`10.0.2.0/24`): Sin acceso directo a Internet.

3. **Gateway de Internet**

   - Permite la comunicación entre la subred pública y la web.
   - Se adjunta a la VPC.

4. **Tabla de Rutas**

   - Se crea una tabla de rutas pública.
   - Se asocia a la subred pública.
   - Incluye una ruta que permite acceso a Internet a través del Gateway de Internet.

5. **Grupo de Seguridad**

   - Permite tráfico HTTP (`puerto 80`) desde cualquier dirección IP.
   - Permite todo el tráfico saliente.

6. **Bucket S3**

   - Se crea un bucket S3 con versionado activado.
   - Su nombre se genera dinámicamente con el ID de la cuenta AWS.

7. **Rol IAM**

   - Permite que la instancia EC2 acceda a S3 con permisos completos (`s3:*`).

8. **Instancia EC2**

   - Se crea una instancia de Ubuntu (versión configurable).
   - Arquitectura `x86_64` o `arm64` (configurable).
   - Se despliega en la subred pública.
   - Asocia el grupo de seguridad.
   - Tiene permisos IAM para interactuar con S3.

## Salidas de la Plantilla

- **InstanceId**: ID de la instancia EC2 creada.
- **PublicIP**: Dirección IP pública de la instancia EC2.
