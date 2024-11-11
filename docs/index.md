# Introducción a Keycloak

Keycloak es una solución de inicio de sesión único (SSO) para aplicaciones web y servicios web RESTful. El objetivo de Keycloak es simplificar la seguridad, facilitando a los desarrolladores de aplicaciones la tarea de proteger las aplicaciones y servicios que han implementado en su organización. Las características de seguridad que normalmente los desarrolladores tendrían que escribir por sí mismos se proporcionan de manera predeterminada y se pueden adaptar fácilmente a los requisitos individuales de tu organización. Keycloak ofrece interfaces de usuario personalizables para el inicio de sesión, el registro, la administración y la gestión de cuentas. También puedes usar Keycloak como una plataforma de integración para conectarlo con servidores LDAP y Active Directory existentes, así como delegar la autenticación a proveedores de identidad externos como Facebook y Google.

## Características

Keycloak proporciona las siguientes características:

    - Inicio y cierre de sesión único para aplicaciones de navegador.
    - Soporte para OpenID Connect.
    - Soporte para OAuth 2.0.
    - Soporte para SAML.
    - Identity Brokering - Autenticación con proveedores de identidad externos mediante OpenID Connect o SAML.
    - Inicio de sesión social - Permite el inicio de sesión con Google, GitHub, Facebook, Twitter y otras redes sociales.
    - User Federation - Sincronización de usuarios desde servidores LDAP y Active Directory.
    - Puente Kerberos - Autentica automáticamente a los usuarios que han iniciado sesión en un servidor Kerberos.
    - Consola de administración para la gestión centralizada de usuarios, roles, mapeos de roles, clientes y configuración.
    - Consola de cuentas que permite a los usuarios gestionar sus cuentas de forma centralizada.
    - Soporte para temas - Personaliza todas las páginas orientadas a los usuarios para integrarlas con tus aplicaciones y marca.
    - Autenticación de dos factores - Soporte para TOTP/HOTP a través de Google Authenticator o FreeOTP.
    - Flujos de inicio de sesión - Registro de usuarios opcional, recuperación de contraseña, verificación de correo electrónico, requisito de actualización de contraseña, etc.
    - Gestión de sesiones - Los administradores y los propios usuarios pueden ver y gestionar las sesiones de usuario.
    - Mapeadores de tokens - Mapea atributos de usuario, roles, etc. en tokens y declaraciones como desees.
    - Políticas de revocación not-before por realm, aplicación y usuario.
    - Soporte para CORS - Los adaptadores de cliente tienen soporte incorporado para CORS.
    - Interfaces de Proveedor de Servicios (SPI) - Un número de SPI para personalizar varios aspectos del servidor. Flujos de autenticación, proveedores de federación de usuarios, mapeadores de protocolos y muchos más.
    - Soporte para cualquier plataforma o lenguaje que tenga una biblioteca OpenID Connect Relying Party o SAML 2.0 Service Provider.

## Operaciones básicas de Keycloak

Keycloak es un servidor independiente que gestionas en tu red. Las aplicaciones se configuran para apuntar a este servidor y estar protegidas por él. Keycloak utiliza estándares de protocolo abierto como OpenID Connect o SAML 2.0 para proteger tus aplicaciones. Las aplicaciones de navegador redirigen el navegador de un usuario desde la aplicación al servidor de autenticación de Keycloak, donde introducen sus credenciales. Esta redirección es importante porque los usuarios están completamente aislados de las aplicaciones, y las aplicaciones nunca ven las credenciales de un usuario. En lugar de ello, las aplicaciones reciben un token de identidad o una aserción que está firmada criptográficamente. Estos tokens pueden contener información de identidad como nombre de usuario, dirección, correo electrónico y otros datos de perfil. También pueden contener datos de permisos para que las aplicaciones puedan tomar decisiones de autorización. Estos tokens también se pueden usar para realizar invocaciones seguras en servicios basados en REST.

## Conceptos y términos clave

Antes de intentar usar Keycloak para proteger tus aplicaciones web y servicios REST, considera estos conceptos y términos clave.

    - **Usuarios**: Entidades que pueden iniciar sesión en tu sistema. Pueden tener atributos asociados como correo electrónico, nombre de usuario, dirección, número de teléfono y fecha de nacimiento. Pueden ser asignados a grupos y tener roles específicos asignados a ellos.
    - **Autenticación**: El proceso de identificar y validar a un usuario.
    - **Autorización**: El proceso de otorgar acceso a un usuario.
    - **Credenciales**: Son piezas de datos que Keycloak utiliza para verificar la identidad de un usuario. Algunos ejemplos son contraseñas, contraseñas de un solo uso, certificados digitales o incluso huellas dactilares.
    - **Roles**: Identifican un tipo o categoría de usuario. Admin, usuario, gerente y empleado son roles típicos que pueden existir en una organización. Las aplicaciones a menudo asignan acceso y permisos a roles específicos en lugar de a usuarios individuales, ya que tratar con usuarios puede ser demasiado detallado y difícil de gestionar.
    - **Mapeo de roles de usuario**: Define una relación entre un rol y un usuario. Un usuario puede estar asociado con uno o más roles. Esta información de mapeo de roles se puede encapsular en tokens y aserciones para que las aplicaciones decidan los permisos de acceso en varios recursos que gestionan.
    - **Roles compuestos**: Un rol compuesto es un rol que puede estar asociado con otros roles. Por ejemplo, un rol compuesto de superusuario podría estar asociado con los roles de administrador de ventas y administrador de entrada de pedidos. Si un usuario está mapeado al rol de superusuario, también hereda los roles de administrador de ventas y administrador de entrada de pedidos.
    - **Grupos**: Gestionan grupos de usuarios. Se pueden definir atributos para un grupo. También se pueden mapear roles a un grupo. Los usuarios que se convierten en miembros de un grupo heredan los atributos y mapeos de roles que define ese grupo.
    - **Realms**: Un realm gestiona un conjunto de usuarios, credenciales, roles y grupos. Un usuario pertenece e inicia sesión en un realm. Los realms están aislados entre sí y solo pueden gestionar y autenticar a los usuarios que controlan.
    - **Clientes**: Son entidades que pueden solicitar a Keycloak que autentique a un usuario. Con mayor frecuencia, los clientes son aplicaciones y servicios que desean utilizar Keycloak para protegerse y proporcionar una solución de inicio de sesión único. Los clientes también pueden ser entidades que solo desean solicitar información de identidad o un token de acceso para poder invocar de manera segura otros servicios en la red que están protegidos por Keycloak.
    - **Adaptadores de cliente**: Son complementos que instalas en tu entorno de aplicación para poder comunicarte y estar protegido por Keycloak. Keycloak tiene varios adaptadores para diferentes plataformas que puedes descargar. También hay adaptadores de terceros disponibles para entornos que no cubrimos.
    - **Consentimiento**: Es cuando, como administrador, quieres que un usuario dé permiso a un cliente antes de que ese cliente pueda participar en el proceso de autenticación. Después de que un usuario proporcione sus credenciales, Keycloak mostrará una pantalla identificando al cliente que solicita el inicio de sesión y qué información de identidad solicita del usuario. El usuario puede decidir si otorga o no la solicitud.
    - **Scopes de cliente**: Al registrar un cliente, debes definir mapeadores de protocolos y mapeos de alcance de roles para ese cliente. A menudo es útil almacenar un client scope para facilitar la creación de nuevos clientes compartiendo algunas configuraciones comunes. Esto también es útil para solicitar algunos claims o roles de manera condicional, basados en el valor del parámetro scope. Keycloak proporciona el concepto de client scope para esto.
    - **Roles de cliente**: Los clientes pueden definir roles que les son específicos. Básicamente, es un espacio de nombres de roles dedicado al cliente.
    - **Token de identidad**: Un token que proporciona información de identidad sobre el usuario. Parte de la especificación OpenID Connect.
    - **Token de acceso**: Un token que puede proporcionarse como parte de una solicitud HTTP que otorga acceso al servicio que se está invocando. Esto forma parte de la especificación OpenID Connect y OAuth 2.0.
    - **Aserción**: Información sobre un usuario. Esto generalmente se refiere a un blob XML que se incluye en una respuesta de autenticación SAML que proporciona metadatos de identidad sobre un usuario autenticado.
    - **Cuenta de servicio**: Cada cliente tiene una cuenta de servicio integrada que le permite obtener un token de acceso.
    - **Direct Grant**: Una forma en la que un cliente puede obtener un token de acceso en nombre de un usuario mediante una invocación REST.
    - **Mapeadores de protocolo**: Para cada cliente, puedes personalizar qué claims y aserciones se almacenan en el token OIDC o la aserción SAML. Lo haces por cliente creando y configurando mapeadores de protocolo.
    - **Sesión**: Cuando un usuario inicia sesión, se crea una sesión para gestionar la sesión de inicio de sesión. Una sesión contiene información como cuándo inició sesión el usuario y qué aplicaciones han participado en el inicio de sesión único durante esa sesión. Tanto los administradores como los usuarios pueden ver la información de la sesión.
    - **Proveedor de federación de usuarios**: Keycloak puede almacenar y gestionar usuarios. A menudo, las empresas ya tienen servicios LDAP o Active Directory que almacenan información de usuario y credenciales. Puedes configurar Keycloak para validar credenciales desde esos almacenes externos y extraer información de identidad.
    - **Proveedor de identidad**: Un proveedor de identidad (IDP) es un servicio que puede autenticar a un usuario. Keycloak es un IDP.
    - **Federación de proveedores de identidad**: Keycloak se puede configurar para delegar la autenticación a uno o más IDP. El inicio de sesión social a través de Facebook o Google es un ejemplo de federación de proveedores de identidad. También puedes conectar Keycloak para delegar la autenticación a cualquier otro IDP OpenID Connect o SAML 2.0.
    - **Mapeadores de proveedores de identidad**: Al realizar la federación de IDP, puedes mapear tokens entrantes y aserciones a atributos de usuario y sesión. Esto te ayuda a propagar información de identidad desde el IDP externo a tu cliente que solicita la autenticación.
    - **Acciones requeridas**: Son acciones que un usuario debe realizar durante el proceso de autenticación. Un usuario no podrá completar el proceso de autenticación hasta que estas acciones se completen. Por ejemplo, un administrador puede programar que los usuarios restablezcan sus contraseñas cada mes. Se configuraría una acción requerida de actualización de contraseña para todos estos usuarios.
    - **Flujos de autenticación**: Son flujos de trabajo que un usuario debe realizar al interactuar con ciertos aspectos del sistema. Un flujo de inicio de sesión puede definir qué tipos de credenciales se requieren. Un flujo de registro define qué información de perfil debe ingresar un usuario y si se debe utilizar algo como reCAPTCHA para filtrar bots. El flujo de restablecimiento de credenciales define qué acciones debe realizar un usuario antes de poder restablecer su contraseña.
    - **Eventos**: Son flujos de auditoría que los administradores pueden ver y conectar.
    - **Temas**: Cada pantalla proporcionada por Keycloak está respaldada por un tema. Los temas definen plantillas HTML y hojas de estilo que puedes sobrescribir según sea necesario.

