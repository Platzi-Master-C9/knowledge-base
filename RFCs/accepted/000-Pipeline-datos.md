# RFC 01 WIP: Data Pipeline

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

Las fuentes indican de dónde provienen los datos. Las fuentes comunes incluyen sistemas de administración de bases de datos relacionales como MySQL, CRM como Salesforce y HubSpot, ERP como SAP y Oracle, herramientas de administración de redes sociales e incluso sensores de dispositivos IoT. Un pipeline de datos debe ser capaz de consumir la información que se analizará desde diversas fuentes de datos.

## Problem

Determinar el pipeline de datos que permitirá recolectar toda la información que generen los demás squads. 

Los problemas que se pueden presentar son: 

* Datos sobre aspectos de diferente naturaleza y formato
* Datos que se generan constantemente y deben ser recolectados en tiempo real
* Datos que generados por diferentes squads y por lo tanto provienen de diversas fuentes
* Enorme cantidad de datos a procesar
* Datos sobre información confidencial

Escoger un pipeline adecuado de datos permitirá crear un proceso adecuado de procesamiento de datos que recolectará la información de diversas fuentes, las procesará en tiempo real y quedará lista para su análisis, sin comprometer la seguridad de los usuarios ni el rendimiento del procesamiento.

## Proposal

**Apache Airflow**

Es una herramienta open source para gestionar, monitorizar y planificar flujos de trabajo. Se usa para automatizar trabajos dividiéndolos en subtareas y es común en la automatización de ingesta de datos, acciones de mantenimiento periódicas y tareas de administración.

Airflow también es bastante útil para gestionar procesos de ETL (Extract, Transform, Load), integra una interfaz de usuario sencilla, permite hacer backups, generar reportes y métricas.

Cualquier persona con conocimientos de Python puede implementar un flujo de trabajo, tiene una gran comunidad activa y puede ejecutar sus tareas en Google Cloud Platform, Amazon Web Services, Microsoft Azure y muchos otros servicios de terceros, por lo que es bastante versátil y potente.

Una gran desventaja de usar esta herramienta es su alta curva de aprendizaje. Probablemente sea necesario conocimientos de DevOps para gestionar todo el proceso debido a lo personalizable y complejo que puede llegar a ser.

Algunos links para conocer un poco más sobre Apache:

https://airflow.apache.org/
https://aprenderbigdata.com/apache-airflow/
https://www.run.ai/guides/machine-learning-operations/apache-airflow

## Definition of success

Los diversos datos de los diferentes squads pueden ser consumidos y procesados en tiempo real sin problemas, por lo que están listos para ser analizados y establecer diferentes métricas. Además la curva de aprendizaje del framework para el squad no es tan compleja como para llevar a cabo este proceso.
