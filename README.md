# FairPay

App para repartir gastos en grupo, al estilo de Tricount, con una diferencia: además de a partes iguales, permite repartir **por porcentajes personalizados** o **proporcionalmente al sueldo** de cada persona.

Proyecto personal, de la idea a la publicación, construido con **asistencia de IA generativa**. Yo defino el producto, tomo las decisiones de diseño y me encargo de toda la parte de calidad.

## Estado

| Plataforma | Estado |
|---|---|
| **Android** | Versión 1.0 terminada, firmada y lista para Google Play |
| **iOS** | Port en SwiftUI al día en funciones con Android. Pendiente: notificaciones push y publicación |

Las dos apps usan el **mismo backend**, así que personas con Android y con iPhone comparten grupos, gastos y notificaciones.

## Funciones

- **Grupos** con varios administradores, código de invitación y miembros «a mano» (sin cuenta) que otra persona puede reclamar después.
- **Gastos** con categorías, participantes concretos y tres modos de reparto: partes iguales, porcentajes y por sueldo.
- **Saldos y liquidaciones** totales o parciales, con propuesta de cómo saldar las deudas.
- **Estadísticas** por categoría y por persona, y **exportación a PDF**.
- **Notificaciones** de 13 tipos e indicador de «actividad sin ver».
- **Copia de solo lectura** del grupo para quien sale o es expulsado, idéntica a lo que veía.
- Español e inglés, tema claro y oscuro, login con email o Google.

## Calidad: cómo me aseguro de que funciona

- **El dinero cuadra al céntimo en las dos plataformas.** El motor de cálculo (reparto, redondeo, saldos y deudas) se valida con **casos de prueba generados ejecutando el código real de Android**:
  - Una implementación de referencia en Python pasa el 100 % de los casos.
  - El motor en Swift pasa los mismos tests en XCTest.
  - Resultado: saldos idénticos en Android e iOS.
- **Guion de pruebas con dos cuentas** sobre el APK de release firmado: login con Google en release, notificaciones push con la app cerrada y restablecer contraseña.
- **Pruebas en emulador y en dispositivos reales** (Android 16 y iPhone con iOS 26), comparando pantalla a pantalla Android con iOS en cada entrega del port.
- **Errores siempre legibles para la persona usuaria**, nunca el mensaje técnico. Al cerrar sesión no queda rastro de la cuenta anterior en el dispositivo.
- **Seguridad en el servidor:** las acciones que un cliente no puede decidir por sí mismo (unirse, salir, eliminar un grupo) pasan por funciones del servidor que lo validan. Las reglas de la base de datos bloquean el resto.
- **Requisitos de Google Play revisados antes de publicar:** target SDK 36 y alineación de 16 KB de las librerías nativas.

## Stack

| Capa | Tecnología |
|---|---|
| Android | Kotlin, Jetpack Compose, Material 3 |
| iOS | Swift, SwiftUI, Swift Charts |
| Backend | Firebase: Authentication, Firestore, Cloud Functions (TypeScript), Cloud Messaging, Hosting |
| Pruebas | Casos de prueba compartidos (JSON), XCTest, implementación de referencia en Python, pruebas manuales guiadas |
