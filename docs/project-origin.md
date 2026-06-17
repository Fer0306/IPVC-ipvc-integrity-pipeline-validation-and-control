> ℹ️ **Note:** This document is written in Spanish. You can use your browser to translate it into English.
> The Spanish version is preserved intentionally as part of the project's authorship and intellectual identity.

# 🌱 Origen del proyecto — IPVC (Integrity Pipeline Validation and Control)  

**Autor:** Fernando Flores Alvarado  
**Proyecto:** IPVC — Integrity Pipeline Validation and Control  
**Licencia:** CC BY 4.0 (documentación)  
Información detallada sobre versiones, fechas, estado y metadatos completos, consulta [`VERSION.md`](../VERSION.md).  

---

## El detonador  

Todo comenzó con una frase que escuché en la comunidad de seguridad: *"ataque a la cadena de suministros"*.  

Poco después, Andrew van der Stock, Director Ejecutivo de OWASP, publicó un mensaje en el canal de líderes advirtiendo sobre un incremento significativo de Pull Requests maliciosos en proyectos OWASP — generados incluso por bots de IA — con el objetivo de comprometer la cadena de suministro de software.  

Esa combinación encendió una pregunta en mi cabeza: ¿qué es esto exactamente, y cómo funciona?  

---

## La investigación  

Me puse a investigar. No tenía experiencia previa con pipelines de CI/CD ni con la cadena de suministros de software, así que empecé desde cero.  

Lo que encontré fue esto: un pipeline CI/CD es esencialmente un flujo lineal de procesos automatizados. Cada vez que un desarrollador sube un cambio, ese flujo se activa — revisa el código, construye la aplicación, la prueba, la escanea y la despliega — sin intervención humana en cada paso.  

Al observar esa arquitectura — procesos lineales, automatizados, secuenciales — algo me llamó la atención de inmediato: **no hay ningún punto entre etapas que valide que lo que acaba de pasar es exactamente lo que se esperaba**. El flujo simplemente continúa.  

Ahí estaba el problema.  

---

## El momento de la decisión  

Al verlo, me dije: *esto es importante, hay que ayudar.*  

Y honrando el principio que guía todo mi trabajo:  

> *“Compartir con responsabilidad es inspirar para construir el futuro.”*
> — Fernando Flores Alvarado  

Me decidí a crear una solución. Así nació IPVC.  

---

## El origen de la idea — BotellaControl  

IPVC no nació de la nada. Nació de la combinación natural de dos proyectos que ya existían, ambos parte de un ecosistema que llamo **BotellaControl**:  

### RHC — Randomized Header Channel  
**Proyecto OWASP:** [RHC for CSRF Protection](https://github.com/OWASP/www-project-randomized-header-channel-for-csrf-protection)  

RHC protege la integridad de los flujos de comunicación HTTP. Su principio central: lo que se envía por un canal debe ser verificable en el otro extremo. Si algo fue alterado en el trayecto, el receptor lo detecta.  

→ **RHC aportó a IPVC: la idea de validar la integridad de lo que viaja entre dos puntos de un flujo.**  

---

### WebAI Inference Throttling  
**Repositorio:** [webai-inference-throttling](https://github.com/Fer0306/webai-inference-throttling)  

WebAI resuelve un problema diferente: cómo ejecutar modelos de Machine Learning en tiempo real en el navegador sin sobrecargar el dispositivo. La solución fue una arquitectura de cuatro capas inteligentes independientes, donde cada capa decide de forma autónoma si actúa o no — procesa solo cuando hay un cambio real, no en cada frame.  

Su principio central: **no se trata de procesar más, sino de saber cuándo no procesar.**  

→ **WebAI aportó a IPVC: la idea de un flujo de capas donde cada una tiene control autónomo sobre si continúa o se detiene.**  

---

### La síntesis — IPVC  

De RHC tomé la integridad. De WebAI tomé el control por capas. Y los apliqué al problema de los pipelines CI/CD:  

> **Control de un flujo de procesos, validando su integridad continua.**  

Cada check-point en IPVC es exactamente eso: una capa que decide de forma autónoma si el flujo puede continuar, basándose en si la integridad de la etapa anterior fue respetada.  

---

## El componente adicional — Registro Centralizado de Escáneres  

Durante la investigación encontré otro problema que nadie había resuelto: existe una gran cantidad de herramientas de escaneo de seguridad desarrolladas por emprendedores y proyectos de la comunidad, pero están dispersas, sin clasificación, sin un lugar central donde encontrarlas.  

Si alguien quiere saber qué escáner usar para su tipo de aplicación, tiene que buscar por toda la internet, invertir tiempo, y aún así no tiene garantía de que lo que encuentre sea lo correcto o lo más adecuado.  

IPVC propone resolver esto con un **Registro Centralizado de Escáneres**: un único lugar donde estas soluciones estén clasificadas por tipo de aplicación y tipo de análisis, de modo que el pipeline pueda seleccionar automáticamente la herramienta correcta — sin intervención manual del desarrollador.  

Esto también abre la puerta a que proyectos existentes de escaneo puedan integrarse como parte de un ecosistema más grande, en lugar de operar de forma aislada.  

---

## Los tres proyectos — una visión de conjunto  

| Proyecto | Qué protege | Cómo lo hace |
|---|---|---|
| **RHC** | La integridad de un flujo de comunicación | Validando lo que viaja entre cliente y servidor |
| **WebAI** | La eficiencia de un flujo de procesamiento | Controlando cuándo cada capa actúa |
| **IPVC** | La integridad de un flujo de procesos | Validando cada etapa antes de continuar |

Los tres nacen del mismo principio: **un flujo sin control es un flujo vulnerable.**  

---
**© 2026 Fernando Flores Alvarado — IPVC (Integrity Pipeline Validation and Control)**  
Publicado bajo [Creative Commons BY 4.0](../LICENSE_CC.md).  

> *“Compartir con responsabilidad es inspirar para construir el futuro.”*  
