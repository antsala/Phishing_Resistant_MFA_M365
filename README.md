# Phishing_Resistant_MFA_M365
Usar factores de autenticacion modernos.

## Requisitos

* Tenant de M365.
* MV con Windows 11.

## Introducción

Respecto a la seguridad, sabemos tres cosas.

1) Las contraseñas no son muy seguras.
2) La autenticación multifactor es algo bueno.
3) Queremos una MFA que sea resistente a ataques de phishing.

La cuestión es cómo conseguir el tercer punto. Vamos a aprenderlo.

En este tutorial aprenderemos a crear MFA resistente al phishing usando los siguientes componentes de M365.

* `Passkeys`.
* `Políticas de Acceso Condicional` (Conditional Access Polocies)
* `Fortaleza de autenticación`(Authentication Strength)
* `Windows Hello para la Empresa` (WHFB)
* `Temporary Access Passwords` (Contraseñas temporales o de un solo uso)

La principal idea que debes tener en cuenta es que vamos a sustituir la MFA de M365 "de toda la vida" (Legacy MFA) por las nuevas políticas de autenticación.

Accede a `Microsoft Entra ID`

![Entra](./img/202411111344.png)

Observa la siguiente imagen.

![Dir métodos auth](./img/202411111549.png)

En la sección `Protección`(1), haz clic en `Métodos de autenticación`(2). Observarás la `Directiva de métodos de autenticación` presente en tu tenant de M365. La columna `Método`(3) lista los disponibles, mientras que en `Habilitado`(4) harás que esté disponible (o no) para tus usuarios.

## Passkey (FIDO2)

El método de autenticación `Clave de paso` (**Passkey**) basado en `FIDO2` en Microsoft 365 es un enfoque moderno de autenticación ***sin contraseñas*** que mejora la seguridad y la experiencia de usuario. Utiliza estándares de la [Fido Alliance](https://fidoalliance.org/) y la **W3C** para permitir un acceso seguro basado en claves criptográficas, eliminando la necesidad de contraseñas tradicionales. 

Las `claves de paso` se almacenan de forma segura en dispositivos del usuario, como teléfonos o hardware de autenticación, y autentican al usuario mediante procesos biométricos o códigos PIN locales. Esto reduce significativamente el riesgo de ataques de phishing o de robo de contraseñas, ya que las credenciales nunca se transmiten ni se almacenan en servidores.

En la siguiente imagen puedes ver cómo este tenant no ofrece este medio a autenticación.

![Passkey](./img/202411111549.png)

Para configurarlo haz clic en él.

Si haces clic en `Habilitar`(1), observa como este método de autenticación queda disponible para todos los usuarios den tenant(2). Para configurarlo, haz clic en `Configurar` (3)

![Passkey2](./img/202411111600.png)

Observa la imagen. En ella verás las diferentes formas de configurar este método.

![Passkey2](./img/202411111647.png)

* `Permitir configuración de autoservicio` indica si los usuarios pueden registrar o configurar por sí mismos sus dispositivos FIDO2 sin la intervención del administrador.

* `Exigir la atestación` refiere a la validación de la autenticidad del dispositivo de seguridad (como un token físico o una clave de seguridad USB) cuando se registra para su uso en un sistema. La atestación es un mecanismo de verificación por el cual el dispositivo proporciona evidencia que permite al sistema de autenticación confirmar que es legítimo y que proviene de un fabricante confiable.

* `Exigir las restricciones de clave` se refiere a cómo se deben aplicar y gestionar las claves de autenticación. Esta opción permite especificar que las claves utilizadas por los usuarios para la autenticación deben cumplir con ciertas restricciones o criterios.

    Estas restricciones pueden incluir:

    ***Tipo de clave***: Especificar qué tipo de clave de seguridad puede usarse (por ejemplo, claves con autenticación biométrica o claves con PIN).

    ***Uso de claves residentes o no residentes***: Controlar si las claves de seguridad deben almacenar la información de autenticación en el dispositivo de la clave (clave residente) o si esta debe gestionarse de otra forma (clave no residente).

    ***Mecanismos de seguridad***: Restringir a ciertos niveles de seguridad, como el uso de claves que cumplan con estándares de autenticación específicos (por ejemplo, FIPS, nivel de certificación).

    ***Control de acceso***: Permitir o denegar claves de autenticación según políticas específicas de la organización.

* `AAGUID` (Authenticator Attestation GUID) es un identificador global único asignado a un tipo de autenticador específico. Este identificador permite que los servidores de autenticación reconozcan la clase o modelo de dispositivo autenticador que está siendo utilizado sin revelar detalles específicos sobre la instancia del dispositivo.

    El **AAGUID** se utiliza principalmente en la fase de atestación, cuando un dispositivo autenticador presenta pruebas de que es confiable y legítimo. Por ejemplo, cuando un usuario registra un dispositivo FIDO2 en un sistema, el servidor recibe información que incluye el **AAGUID** para poder identificar de qué tipo de autenticador se trata y decidir si confía en él según sus políticas de seguridad.

Una vez configurada la política `FIDO2` haz clic en el botón ***Guardar***.

## Microsoft Authenticator

Este factor de autenticación está activado y configurado por defecto. Permite usar la aplicación `Microsoft Authenticator`, que es una aplicación de autenticación multifactor (MFA) desarrollada por Microsoft. Funciona generando códigos de verificación temporales o enviando notificaciones de aprobación a dispositivos móviles.

Haz clic en la pestaña ***Configurar*** para acceder a su configuración.

![MA](./img/202411120724.png)

Cuando la opción `Permitir el uso de Microsoft Authenticator OTP` está activada, la aplicación genera un código de un solo uso basado en un algoritmo de tiempo (`TOTP`) que el usuario puede ingresar al autenticarse. Este código es creado automáticamente por la app y se actualiza cada 30 segundos.

El usuario solo necesita abrir la aplicación y ver el código para usarlo al iniciar sesión. Esto es diferente de la autenticación por notificaciones push, en la cual el usuario simplemente aprueba una solicitud en la app.

![OTP](./img/202411120731.png)

[Saber más sobre OTP](https://aka.ms/numbermatchdoc)

El resto de configuraciones son las siguientes.

![OTP2](./img/202411120737.png)

## SMS 

Este método de autenticación envía un mensaje de texto al móvil que ha configurado el usuario en su MFA.

![SMS](./img/202411120740.png)

[Saber más sobre SMS](https://learn.microsoft.com/es-es/entra/identity/authentication/concept-authentication-phone-options#mobile-phone-verification)

## Pase de acceso temporal (TAP)

Es un código de acceso de uso limitado o de tiempo limitado que los usuarios pueden usar como factor de autenticación.

![TAP](./img/202411120743.png)

En la configuración puedes poner la duración y longitud del código.

![TAP2](./img/202411120744.png)

[Saber más sobre TAP](https://learn.microsoft.com/es-es/entra/identity/authentication/howto-authentication-temporary-access-pass)

## Configuración de Tokens OATH de hardware (versión preliminar)


https://www.youtube.com/watch?v=7nMKPPLaN7o

