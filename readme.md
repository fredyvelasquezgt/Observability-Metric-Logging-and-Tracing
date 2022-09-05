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

Un los es inmutable, una registro de una marca de tiempo de eventos discretos que ocurrieron durante el tiempo.

## Tracing

Un rastro es una representación de una serie de eventos distribuidos casualmente relacionados que codifican el flujo de solicitudes de extremo a extremo a través de un sistema distribuido.

## Metrics

Las metrics son representaciones numéricas de información medida en intervalos de tiempo.
