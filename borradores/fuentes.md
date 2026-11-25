# Notas de fuentes: SoundCloud (consulta del 24-nov-2026)

Cada cifra lleva su fuente y fecha. Lo que la fuente no reporta se anota aparte, porque el informe debe declararlo.

## Fuentes primarias

| Clave | Fuente | Fecha |
|---|---|---|
| calcado2014monolith | P. Calçado, «Building Products at SoundCloud, Part I: Dealing with the Monolith», blog SoundCloud Backstage | 11-jun-2014 |
| bryant2015qcon | D. Bryant, nota de InfoQ sobre la charla de Calçado en QCon London 2015 («No Free Lunch, Indeed: Three Years of Micro-services at SoundCloud») | 15-mar-2015 |
| stuart2016monolith | T. Stuart, «Microservices and the monolith», blog SoundCloud Backstage | 26-ago-2016 |
| obrien2022strangler | D. O'Brien y J. Creixell, «The End of the Public API Strangler», blog de SoundCloud | 14-mar-2022 |

## Cifras que sí aparecen

- Usuarios mensuales: de unos 3 millones (2011) a unos 300 millones (bryant2015qcon).
- Contenido subido: unas 12 horas por minuto en 2014 (calcado2014monolith); 11 horas por minuto en 2015 (bryant2015qcon). Las dos cifras difieren: citar cada una con su año.
- API pública usada por miles de aplicaciones de terceros (calcado2014monolith).
- Decisión de adoptar microservicios: 2011 (bryant2015qcon). El Strangler se creó en 2014 y el trabajo serio para retirarlo empezó en enero de 2020, tras seis años de progreso modesto. La migración duró ocho años (obrien2022strangler).
- Un proyecto de extracción tarda varios meses (stuart2016monolith).

## Lo que las fuentes no reportan

- Número de microservicios.
- Número de ingenieros.
- Tráfico (peticiones por segundo o similar).
- Beneficios medidos de la migración (latencia, costes, incidentes). Solo hay descripción cualitativa.
- Cifras de progreso de la migración (stuart2016monolith no incluye métricas).

## Estado antes de migrar (calcado2014monolith)

- Una aplicación Ruby on Rails monolítica (MRI, memcached, MySQL), llamada internamente «Mothership». Contenía la API pública y la aplicación web.
- Desde «Next SoundCloud» (2012) la interfaz principal era la API pública, usada también por los clientes propios.
- El equipo sentía que solo «parchaba» el sistema.

## Motivos (calcado2014monolith, bryant2015qcon)

- Resolver el problema de escalabilidad de fondo y no solo parchearlo.
- Componentes pequeños con APIs bien definidas.
- Evitar que los servicios leyeran la base de datos del monolito.
- Reaccionar a la actividad de usuarios sin polling.
- Contexto: periodo de «hypergrowth».

## Desafíos y soluciones

| Desafío | Qué hicieron | Fuente |
|---|---|---|
| Evitar una refactorización «big-bang» | Dejaron de añadir funciones a Mothership; las nuevas se hacen como microservicios y se extrae código solo al refactorizar | calcado2014monolith |
| Servicios dependientes del monolito | Descartaron el acceso directo a su base de datos; usaron la API pública como interfaz | calcado2014monolith |
| Reaccionar a eventos sin polling | «Semantic Events» publicados en un broker (AMQP/RabbitMQ) | calcado2014monolith |
| API pública limitaba el acceso a datos | API interna con engines de Rails, solo en red privada, con OAuth 2.0 | calcado2014monolith |
| Operación: «noisy neighbours» (LXC sin cgroups), monitoreo con Graphite, saber qué se rompió | Estandarizar dashboards, exponer funciones operativas, pipeline de build fiable; Prometheus (pull) | bryant2015qcon |
| El plan de extracción no avanzaba: varios meses por entidad, dependencia de todos los equipos, servicios que leían la base del monolito | Distribuir el cambio de los puntos de llamada, redefinir «terminado», normas de integración, medir el progreso con monitoreo | stuart2016monolith |
| El Strangler quedó sin mantenimiento: rutas duplicadas, pérdida de conocimiento, riesgos de seguridad por exponer un Rails obsoleto, roturas al portar endpoints | Portaron todos los endpoints, eliminaron el código de la API pública y el Strangler pasó a ser un BFF completo en Scala | obrien2022strangler |

## Para cruzar con el PFC (SSDC)

- Parten de un monolito, como SoundCloud en 2011.
- El equipo es de pocas personas: las prácticas de gobernanza de SoundCloud (normas de integración, monitoreo de la migración) son más relevantes que su infraestructura.
