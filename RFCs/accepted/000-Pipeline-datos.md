# RFC 000 WIP: Data Pipeline

+ Recommender: omargorozcor@gmail.com, luis.fer.0987654@gmail.com y ing.nicaes@gmail.com 
+ Date: 23/02/2022	
+ Status: WIP
+ Decider: 
+ Input providers: 
+ Approvers 
+ Approvals:
+ Team: (Business Intelligence)

## Background

Una pipeline de datos es una construcción lógica que representa un proceso dividido en fases. Los pipelines de datos se caracterizan por definir el conjunto de pasos o fases y las tecnologías involucradas en un proceso de movimiento o procesamiento de datos. 

A Data Pipeline is the process where the idea is to collect the data, send it to a specific location in order to work with it and try to find out if there is some relevant information that can be shared by the team in a Dashboard or other way to post it.


## Problem

Determinar el pipeline de datos que permitirá recolectar toda la información que generen los demás squads. 

Los problemas que se pueden presentar son: 

●	Tipos de Datos diferentes en naturaleza y formato
●	Datos generados en tiempo real
●	Múltiples fuentes de datos
●	Escalar la cantidad de datos a procesar
●	Establecer si es necesario procesos de anonimización

Escoger un pipeline adecuado de datos permitirá crear un proceso que recolectará la información de diversas fuentes, las procesará en tiempo real y quedará lista para su análisis, sin comprometer la seguridad de los usuarios ni el rendimiento del procesamiento.


## Proposal

**Apache Airflow**

Es una herramienta open source para gestionar, monitorizar y planificar los flujos de trabajo. Se usa para automatizar trabajos dividiéndolos en subtareas y es común en la automatización de ingesta de datos, acciones de mantenimiento periódicas y tareas de administración.

Airflow también es bastante útil para gestionar procesos de ETL/ELT (Extract, Transform, Load), integra una interfaz de usuario sencilla, permite hacer backups, generar reportes y métricas.

Una persona con conocimientos de Python puede implementar un flujo de trabajo, tiene una gran comunidad activa y puede ejecutar sus tareas en Google Cloud Platform, Amazon Web Services, Microsoft Azure y muchos otros servicios de terceros, por lo que es bastante versátil y potente.

Una gran desventaja de usar esta herramienta es su alta curva de aprendizaje. Probablemente sea necesario conocimientos de DevOps para gestionar todo el proceso debido a lo personalizable y complejo que puede llegar a ser.

Es posible utilizar servicios como docker para solventar dichos problemas y tener una imagen funcional de Airflow, pero es posible que no permita el 100% de personalización sino existen bases sólidas en conjunto del equipo para llegar a ese punto.

Algunos links para conocer un poco más sobre Apache:

https://airflow.apache.org/
https://aprenderbigdata.com/apache-airflow/
https://www.run.ai/guides/machine-learning-operations/apache-airflow


## Definition of success

Los diversos datos de los diferentes squads pueden ser consumidos y procesados en tiempo real buscando replicar una arquitectura orientada a eventos, por lo que están listos para ser analizados y establecer diferentes métricas. Además la curva de aprendizaje del framework para el squad puede ser un skill a desarrollar que es útil para cada uno de los integrantes.
