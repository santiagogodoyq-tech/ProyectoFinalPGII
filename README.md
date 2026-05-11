# ProyectoFinalPGII
Sara Benjumea Gallego
Santiago Godoy Quitian
1 Pensamiento computacional
Abstracción:
¿Qué se solicita?
Se solicita crear una aplicación que permita gestionar eventos, compra de entradas y perfiles de usuarios, mientras se tiene en cuenta los asientos, si esta ocupados o no, mantener registros de los pagos, ademas de tener en cuenta las anomalías y registrarlas como incidencias.
¿Qué informacion es relevante?
La informacion relevante son los usuarios, eventos, el recinto, las zonas, los asientos, las compras, entradas, incidencias, reportes y métricas.
¿Cómo se agrupa la informacion relevante?
Usuario: idUsuario, nombre, correo, teléfono, métodos de pago.
Evento: idEvento, nombre, categoría, descripción, ciudad, fecha, estado del evento, políticas y un recinto asociado.
Recinto: idRecinto, nombre, dirección, ciudad. 
Zona: idZona, nombre, capacidad, precio base 
Asientos: idAsiento, fila, número, estado. 
Compras: idCompra, usuario, evento, fecha, total, estado 
Entradas: idEntrada, zona, asiento, precio final, estado 
Incidencias: idIncidencia, tipo, descripción, fecha, entidad afectada 
Reportes y métricas: ventas, ocupación, cancelaciones, ingresos adicionales.
Descomposición:
 ¿Qué funcionalidades se solicitan?
Registrarse y/o iniciar sesión, gestionar perfil, explorar eventos disponibles con filtros, consultar detalle de un evento, seleccionar entradas por zona y/o asientos, crear, modificar y cancelar una compra antes de confirmarse el pago, pagar la compra y consultar comprobantes, visualizar estado de la compra, agregar servicios adicionales a la compra, consultar historial de compras con filtros por fecha, evento y estado, descargar reportes de sus compras en csv o pdf, gestionar usuarios, gestionar eventos, gestionar recintos y zonas, gestionar asientos y su disponibilidad, gestionar compras, registrar incidencias y cambios de estado, panel de métricas, visualización de métricas, registrar usuario, iniciar sesión y modificar datos del usuario, gestionar métodos de pago simulados, consultar compras asociadas y sus detalles, crear, actualizar, eliminar y consultar eventos, publicar/pausar/cancelar eventos, consultar disponibilidad del evento por zonas y asientos, crear, actualizar, eliminar y consultar recintos, administrar zonas asociadas al recinto, crear, actualizar, eliminar y consultar zonas, definir precio base y capacidad por zona, consultar ocupación por zona, crear/actualizar/eliminar/consultar asientos por zona, cambiar estado del asiento, consultar mapa de asientos y disponibilidad, crear compras nuevas, modificar una compra antes de pagar, cancelar una compra según reglas/políticas, consultar detalle de una compra, generar entradas asociadas a una compra pagada, consultar entradas por compra y por evento, anular entradas por cancelación/reembolso, registrar incidencias y asociarlas a eventos o compras, consultar incidencias por rango de fechas y tipo.
¿Cómo se distribuyen las funcionalidades? 
Usuario: Registrarse y/o iniciar sesión, gestionar perfil, explorar eventos disponibles con filtros, consultar detalle de un evento, seleccionar entradas por zona y/o asientos, crear, modificar y cancelar una compra antes de confirmarse el pago, pagar la compra y consultar comprobantes, visualizar estado de la compra, agregar servicios adicionales a la compra, consultar historial de compras con filtros por fecha, evento y estado, descargar reportes de sus compras en csv o pdf, gestionar usuarios, gestionar eventos, gestionar recintos y zonas, gestionar asientos y su disponibilidad, gestionar compras, registrar incidencias y cambios de estado, panel de métricas, visualización de métricas, registrar usuario, iniciar sesión y modificar datos del usuario, gestionar métodos de pago simulados, consultar compras asociadas y sus detalles.
Evento: Crear, actualizar, eliminar y consultar eventos, publicar/pausar/cancelar eventos, consultar disponibilidad del evento por zonas y asientos.
Recinto: Asientos, crear, actualizar, eliminar y consultar recintos, administrar zonas asociadas al recinto.
Zona: Crear, actualizar, eliminar y consultar zonas, definir precio base y capacidad por zona, consultar ocupación por zona.
Asiento: Crear/actualizar/eliminar/consultar asientos por zona, cambiar estado del asiento, consultar mapa de asientos y disponibilidad
Compra: Crear compras nuevas, modificar una compra antes de pagar, cancelar una compra según reglas/políticas, consultar detalle de una compra
Entrada: Generar entradas asociadas a una compra pagada, consultar entradas por compra y por evento, anular entradas por cancelación/reembolso
Incidencia: Registrar incidencias y asociarlas a eventos o compras, consultar incidencias por rango de fechas y tipo.
¿Qué debo hacer para probar las funcionalidades? 
para probar las funcionalidades se necesitaría crear un usuario corriente y un usuario administrador, con el usuario corriente intentar cambiar los datos, ver y consultar datos de eventos desde usuario, intentar comprar, reembolsar o crear incidencias en diferentes eventos con diferentes políticas, intentar cambiar las compras antes de terminarlas y después de terminarlas, con el usuario administrador intentar cambiar información o eliminar diferentes usuarios corriente, gestionar eventos, recintos, zonas, asientos, disponibilidad y compras, registrar incidencias y cambios de estado, también observar el panel de métricas y visualizarlas, para el recinto, crear uno,  administrar las zonas asociadas, actualizarla y eliminarla, crear asientos cambiarlos de estado, mostrar el mapa de asientos con la disponibilidad, crear y modificar compras, cancelarlas en diferentes eventos con diferentes políticas, usar las compras para generar entradas, consultar las compras junto a su entrada asociada y anularlas junto a su compra, además de forzar incidencias para crear registros y consultarlos según su rango fecha y tipo.
¿Qué puedo reutilizar? 
los patrones de diseño Singleton, Factory method, Builder, Decorator,  Adapter, Facade, Strategy, Observer, State
¿Cómo pruebo/escribo la solución en Java? 
/código en el repositorio/
PATRONES QUE SE IMPLEMENTAN 


3 PATRONES CREACIONALES: 
SINGLETON: 
Resuelve: RF-015 (Disponibilidad de asientos), RF-013 (Gestión de eventos), RF-030 (ocupación por zona), RF-025 (Disponibilidad por zona)
Problema en el contexto de la plataforma:
La plataforma requiere solo un registro para la disponibilidad de los asientos, si existen muchos gestores de disponibilidad, habrian dos usuarios con la posibilidad de hacer reservas al mismo tiempo, generando duplicados y conteos mal hechos, de igual manera, la conexión con los datos y la estadística de ventas son recursos compartidos durante la ejecución. 
¿Por qué singleton y no otro patrón?
Un acceso a datos normal permitiría crear múltiples instancias, lo que rompería la integridad de la disponibilidad. Singleton garantiza una sola fuente, un control de acceso y posibilidad de extensión posterior.
FACTORY METHOD
RF-038 (generación de entradas), RF-007(Pago), RF-009) Servicios adicionales, RF-039 (consultar entradas por compra/venta)
Problema en el contexto de la plataforma:
La plataforma hace distintos tipos de entradas y diferentes comprobantes de pago según el método seleccionado. Poniendo directamente un “newEntradaVIP()” O “newEntradaGeneral()” en el código cliente hace que cada cambio en la lógica obligue a modificar puntos del sistema, violando OCP.
¿Por qué Factory method y no otro patrón?
Usar por ejemplo abstract factory sería excesivo porque no se necesitan varios objetos relacionados sino variantes de un solo producto. Con factory method encapsula la creación en subclases, permitiendo añadir nuevos tipos de entrada sin tocar el código que ya existe.

BUILDER:
RF-034 (Crear compra), RF-035 (modificar compra antes de pagar), RF-009 (Servicios adicionales)
Problema en el contexto de la plataforma:
Una compra es un objeto extenso: tiene entradas de distintas zonas, servicios adicionales opcionales, método de pago y política de cancelación. Construirla con un constructor de muchos parámetros genera un código sensible a errores. Además el usuario puede modificar la compra antes de pagar, lo que requiere una construcción incremental y flexible.
¿Por qué Builder y no otro patrón?
El prototype requeriría un objeto base ya construido para clonar, lo que no se puede usar aquí, un constructor con objetos opcionales o que use setters expone el objeto incompleto, con el builder podemos construir el objeto paso a paso, y valida el estado antes de construirlo y retorna un objeto. Es el patrón para objetos con parámetros opcionales.

PATRONES ESTRUCTURALES:
DECORATOR 
RF-009 (servicios adicionales a la compra), RF-007( Precio final de la compra), RF-005(Selección por zona) RF-029(Precio base por zona)
Problema en el contexto de la plataforma:
Un usuario puede agregar uno o más servicios adicionales adicionales (acceso VIP, seguro de cancelación, merchandising, parqueadero, acceso preferencial) a su compra. Cada servicio modifica el precio y puede añadir comportamiento al procesar el pago. Modelar esto con una herencia crearía muchas subclases, lo que sería demasiado extenso.
¿Por qué Decorador y no otro patrón?
Si se usara composite agrupa objetos del mismo tipo en jerarquías, no sirve para añadir responsabilidades dinámicamente. Herencia generaría explosion de subclases. El decorator envuelve objetos base con capas que añaden precio y comportamiento, se pueden combinar en cualquier orden y añadir nuevos servicios sin modificar el código, con decorator podemos adicionar responsabilidades.

ADAPTER 
RF-046 (generación de reportes CSV/PDF con Apache POI / PDFBox) RF-011 (descargar reportes de usuario), RF-007 (Pago con distintos métodos simulados)
Problema en el contexto de la plataforma:
La plataforma debe integrarse con dos contextos incompatibles: muchos métodos de pago (tarjeta de credito, pse, efectivo) que tienen distintas interfaces, y bibliotecas externas de generación de los reportes que examen APIS completamente diferentes. El código de negocio no debe conocer los detalles de ninguna de estas APIS externas.
¿Por qué Adapter y no otro patrón?
Facade por ejemplo convertiría una interfaz extensa en un subsistema pero no puede convertir una interfaz en otra. Requiere que ambas esten diseñadas juntas. El adapter convierte la interfaz de una clase existente (incompatible) en la interfaz que el cliente espera sin modificar el código fuente de la clase que se adapta.

FACADE 
RF-006  (crear/modificar/cancelar compra), RF-007(pago y comprobantes), RF-019(visualización metricas javAFX), RF-038(generación de entradas, RF-017(Registro de incidencias)
Problema en el contexto de la plataforma:
Confirmar una compra implica coordinar varios subsistemas: validar la disponibilidad de asientos, procesar el pago, generar entradas, registrar la compra en el sistema, enviar notificaciones y actualizar metricas. Sin un punto de entrada unificado, el codigo cliente tendría que conocer y coordinar todos los subsistemas directamente.
¿Por qué Facade y no otro patrón?
Mediator coordina objetos para reducir dependencias entre ellos, pero hace que los objetos conozcan al mediador. Facade da una interfaz simplificada a un subsistema complejo sin que los subsistemas necesiten conocerse, cumpliendo SRP y reduciendo el acoplamiento entre capas.

PATRONES DE COMPORTAMIENTO:
STRATEGY:
RF-007 (Pago con distintos metodos), RF-010(historial con filtros), RF-011 (Exportar CSV o PDF), RF-036 (cancelar compra según politicas)
Problema en el contexto de la plataforma:
El sistema debe soportar múltiples métodos de pago y diferentes políticas de cancelación. Implementar estos algoritmos con if/else o switch hace que agregar un nuevo método de pago o política obligue a modificar la clase Compra (viola OCP y SRP).

¿Por qué Strategy  y no otro patrón?
Template method por ejemplo podría funcionar para definir el esqueleto de algoritmo, pero requiere herencia y ata al cliente a la jerarquía, State puede ser similar pero modela transiciones entre estados de un objeto, no algoritmos intercambiables. Strategy permite inyectar en tiempo de ejecución el algoritmo concreto cumpliendo DIP e ISP, lo que facilita las pruebas unitarias.

OBSERVER
RF-008 (visualizar estado de compra), RF-017 (registrar incidencias), RF-018 (panel de métricas en tiempo real), RF-040 (anular entradas por cancelación), RF-041 (registrar y asociar incidencias)

Problema en el contexto de la plataforma:
Cuando el estado de una compra cambia (de creada a cambiada, de pagada a cancelada, etc.) o cuando un evento cambia de estado (publicado a cancelado), múltiples componentes del sistema deben reaccionar: el módulo de notificaciones debe enviar un correo/mensaje al usuario, el módulo de incidencias debe registrar el cambio, y el panel de métricas debe actualizarse, agrupar directamente la logica del negocio con todos estos efectos secundarios viola SRP. 

¿Por qué Observer y no otro patrón?
Mediator centraliza la comunicación pero crea un único punto de acoplamiento que crece mucho con cada nueva relación. Command  encapsula acciones pero no define el mecanismo de notificación a muchos receptores. Con observer podemos implementar el mecanismo de la publicación o suscripción que desordena completamente al publicador (compra, evento) de los suscriptores ( notificaciones, métricas, incidencias).

STATE 
RF-008 (estados de compra), RF-024 (estados de evento), RF-032 (estado del asiento), RF-033 (mapa de asientos), RF-040 (anular entradas)

Problema en el contexto de la plataforma:
Una compra tiene 6 estados posibles y un evento tiene 5 estados posibles. El comportamiento permitido varía según el estado actual: no se puede pagar una compra cancelada, no se pueden vender entradas de un evento pausado, solo se puede reembolsar una compra pagada o confirmada. Sin el patrón state, el código estaría lleno de condicionales en cada método que comprueban el estado actual, lo que viola SRP y hace el código difícil de mantener.

¿Por qué State y no otro patrón?
Strategy también usa composición con objetos intercambiables, pero modela algoritmos, no el ciclo de vida de un objeto. Chain of responsability pasa una solicitud por una cadena de manejadores, no modela transiciones entre estados. State encapsula el comportamiento específico de cada estado en una clase propia y gestiona las transiciones válidas, eliminando los condicionales del contexto. Cada cambio invalido lanza una excepción desde el estado correspondiente, sin que el contexto sepa nada de las reglas de transición.
