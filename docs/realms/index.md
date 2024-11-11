#  Configuración de realms

Teniendo una cuenta con acceso a la Consola de Administración, puedes configurar realms. Un realm es un espacio donde gestionas objetos, incluidos usuarios, aplicaciones, roles y grupos. Un usuario pertenece a un realm e inicia sesión en él. Una implementación de Keycloak puede definir, almacenar y gestionar tantos realms como permita el espacio en la base de datos.

## Uso de la Consola de Administración

1. Ve a la URL de la Consola de Administración. Por ejemplo, para localhost, usa esta URL: [http://localhost:8080/admin/](http://localhost:8080/admin/)

    ![Signin](../images/sign.png)

2. Ingresa el nombre de usuario y la contraseña con permisos de administración. Esta acción mostrará la Consola de Administración.

    ![Signin](../images/administration.png)

3. Ten en cuenta los menús y otras opciones que puedes usar:

    - Haz clic en el menú etiquetado como **Master** para elegir un realm que desees gestionar o para crear uno nuevo.

        ![Signin](../images/master.png)

    - Haz clic en la lista en la parte superior derecha para ver tu cuenta o cerrar sesión.

        ![Signin](../images/sign_out.png)


    - Haz clic en un icono de signo de interrogación (?) para mostrar un texto de ayuda que describe ese campo. La imagen del punto 2 muestra la ayuda en acción.

!!! info

    Los archivos exportados desde la Consola de Administración no son adecuados para copias de seguridad o transferencia de datos entre servidores. Solo las exportaciones en tiempo de arranque son adecuadas para copias de seguridad o transferencia de datos entre servidores.

## El realm master
