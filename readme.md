# Observability: Metric, Logging, and Tracing

Un sistema distribuido es uno en el cual el fallo de una computadora que ni siquera sabía que existía puede hacer que mi propia computador quede inutilizable - Leslie Camport

Monitoring me permite responder solo las preguntas que yo ya tenía preparadas.

## Observability

En la teoría de control, observability es una medida de que tan bien los estados internos de un sistema pueden ser inferidos por conocimiento de sus outputs externos. Observability y controllability de un sistema son matematicamente duales.

En otras palabras, es posible entender lo que pasa en el interior de mi código y de mis sistemas simplemente haciendo preguntas usando mis herramientas? Puedo responder cualquier pregunta nueva que se me ocurra, o solamente las que yo haya preparado?

### Pilares de observability

- Metrics
- Logging
- Tracing

## Logging

Un log es inmutable, un registro de una marca de tiempo de eventos discretos que ocurrieron durante el tiempo.

<img src="./src/img3.jpeg" height=300>

> Lista de logs desplegados en Datadog

### Ejemplo

Un itinerario de vuelo es un buen ejemplo de este principio: Todos registramos a los pasajeros y los miembros del equipo antes de que salga el vuelo, asi sabemos quienes están en el avión en un tiempo especifico.

## Tracing

Un rastro es una representación de una serie de eventos distribuidos casualmente relacionados que codifican el flujo de solicitudes de extremo a extremo a través de un sistema distribuido.

<img src="./src/img4.png" height=300>

> Un rastro distribuido usando ELK stack

### Ejemplo

El tracing funciona como la caja negra de un avión durante un choque: ayuda a entender como pasaron las cosas durante el accidente, a descubrir la cadena de eventos que dieron lugar al problema. Provee una perspectiva de bajo nivel de comprensión: qué ocasionó algo en el programa, con qué argumentos lo hizo, en qué orden lo hizo, cuánto duró cada paso.

## Metrics

Las metrics son representaciones numéricas de información medida en intervalos de tiempo.

<img src="./src/img5.png" height=400>

> Métricas desplegadas en Grafana usando Prometheus

### ¿Qué métricas?

Google recomienda las **Four Golden Signals**

- latency: Tiempo para atender a una solicitud.
- traffic: solicitudes/segundo
- error: Tasa de error de las solicitudes
- saturation: Plenitud de un servicio.

## Alerting

Es una parte fundamental, yo quiero estar siempre enterado de si las cosas van bien o no.

### Alertas basadas en métricas [state]

¿Mi servicio está activo y/o se puede dañar?

```
absent (up{kubernetes_name="doccserver"}) or
sum(up{kubernetes_name="doccserver"}) == 0
```

¿Tengo el número esperado de loadbalancers?

```
sum(up{kubernetes_name="loadbalancer"}) < 3
```

### Alertas basadas en métricas [límite]

¿Está nuestro loadbalancer en su 50% de capacidad en términos de sesiones?

```
max(haproxy_frontend_current_sessions / haproxy_frontend_limit_sessions)
BY (kubernetes_node_name, frontend) 100 > 50
```

¿El 50% de los tests están tomando más de 10 minutos?

```
max(test_duration_seconds{quantile="0.5", result="pass"})
BY (test_name) > 600
```
