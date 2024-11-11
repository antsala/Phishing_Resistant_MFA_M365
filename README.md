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

(1) Permitir configuración de autoservicio.
etc.

https://www.youtube.com/watch?v=7nMKPPLaN7o

