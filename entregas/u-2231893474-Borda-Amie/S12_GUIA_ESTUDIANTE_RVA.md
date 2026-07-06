# S12 — GUÍA DE TRABAJO DEL ESTUDIANTE
## Curso: Realidad Virtual y Aumentada | PSISP08075
### Semana 12 — Optimización y Rendimiento en XR

---

> **Instrucciones:** Resuelve todas las secciones en orden. Tiempo sugerido: 90 minutos.
> Entrega en el repositorio del curso como archivo `.md` con tu rama `u-codigo-apellido-nombre-gt12`.
> **No está permitido** buscar respuestas en internet para la Sección A y B.

| Campo | Detalle |
|-------|---------|
| **Estudiante** |Borda Garcia Amie Paola |
| **Código** | 2231893474 |
| **Fecha** |5/07/2026|
| **Semana** | 12 — Optimización y Rendimiento en XR |

---

## SECCIÓN A — PREGUNTAS DE OPCIÓN MÚLTIPLE (20 puntos — 2 pts c/u)

**Pregunta 1** *(básica)*

¿Cuántos FPS mínimos exige Meta para aprobar una app en el Quest Store?

- a) 30 FPS
- b) 60 FPS
- c) 72 FPS
- d) 120 FPS

**Respuesta:** c) 72 FPS

---

**Pregunta 2** *(básica)*

¿Cuál es la herramienta principal de Unity para diagnosticar problemas de rendimiento en tiempo real?

- a) Inspector
- b) Unity Profiler
- c) Package Manager
- d) Scene View Stats

**Respuesta:** b) Unity Profiler

---

**Pregunta 3** *(básica)*

¿Qué es un "Draw Call" en el contexto del rendering de Unity?

- a) Una función de C# que dibuja texto en pantalla
- b) Una instrucción que la CPU envía a la GPU para renderizar un objeto
- c) Una llamada al sistema operativo para mostrar la ventana de Unity
- d) El proceso de importar modelos 3D al proyecto

**Respuesta:**  b) Una instrucción que la CPU envía a la GPU para renderizar un objeto

---

**Pregunta 4** *(básica)*

¿Qué condición debe cumplir un objeto para poder aplicarle Static Batching?

- a) Debe tener un Rigidbody
- b) Debe estar marcado como "Static" y no moverse en runtime
- c) Debe tener exactamente el mismo mesh que otro objeto
- d) Debe estar en la misma capa (Layer) que los otros objetos

**Respuesta:** b) Debe estar marcado como "Static" y no moverse en runtime

---

**Pregunta 5** *(intermedia)*

Un modelo 3D tiene 50,000 triángulos en LOD 0. Si el usuario está a 30 metros de distancia y el objeto ocupa el 10% de la pantalla, ¿qué debería mostrar un LOD Group bien configurado?

- a) LOD 0 (50,000 triángulos) porque el objeto está visible
- b) LOD 1 o LOD 2 con menos triángulos, porque el usuario no nota la diferencia a esa distancia
- c) "Culled" (no renderiza) porque el objeto es pequeño en pantalla
- d) LOD 0 siempre, independientemente de la distancia

**Respuesta:**  b) LOD 1 o LOD 2 con menos triángulos, porque el usuario no nota la diferencia a esa distancia

---

**Pregunta 6** *(intermedia)*

Un desarrollador tiene 300 árboles idénticos en su escena con el mismo material. ¿Qué técnica produce mayor reducción de Draw Calls?

- a) Static Batching, porque los árboles no se mueven
- b) GPU Instancing, porque son instancias del mismo mesh con el mismo material
- c) LOD Groups, porque reduce la cantidad de triángulos
- d) Occlusion Culling, porque no renderiza los que están ocultos

**Respuesta:** b) GPU Instancing, porque son instancias del mismo mesh con el mismo material

---

**Pregunta 7** *(intermedia)*

¿Por qué crear `new List<>()` dentro de `void Update()` es un problema de rendimiento?

- a) Porque List no se puede crear dentro de métodos de Unity
- b) Porque genera un objeto nuevo en el heap en cada frame, aumentando la presión sobre el Garbage Collector
- c) Porque Unity no soporta listas genéricas en tiempo de ejecución
- d) Porque List.Add() es más lento que los arrays simples

**Respuesta:** b) Porque genera un objeto nuevo en el heap en cada frame, aumentando la presión sobre el Garbage Collector

---

**Pregunta 8** *(avanzada)*

En el Unity Profiler, observas que `Camera.Render` toma 45ms y `Scripts Update` toma 2ms por frame. ¿Qué tipo de problema tiene la aplicación?

- a) CPU bound — los scripts son el cuello de botella
- b) GPU bound — el problema está en el rendering
- c) Memory bound — hay demasiada memoria usada
- d) Physics bound — las colisiones son el problema

**Respuesta:**  b) GPU bound — el problema está en el rendering

---

**Pregunta 9** *(avanzada)*

¿Cuál es la ventaja del formato de textura ASTC sobre una textura sin comprimir (RGBA32) en Android?

- a) ASTC es más rápido de cargar desde el disco pero ocupa más memoria en GPU
- b) ASTC reduce el tamaño en memoria de GPU hasta en un 75-80%, mejorando el rendimiento
- c) ASTC solo funciona en dispositivos con Android 10 o superior
- d) ASTC mejora la calidad visual pero no tiene impacto en rendimiento

**Respuesta:** b) ASTC reduce el tamaño en memoria de GPU hasta en un 75-80%, mejorando el rendimiento

---

**Pregunta 10** *(avanzada)*

¿Qué es el "GC.Collect" que aparece en el Unity Profiler y por qué causa stutters?

- a) Un método que recolecta datos de juego para análisis estadístico
- b) El proceso del Garbage Collector que libera memoria de objetos no usados, pausando temporalmente todos los demás procesos
- c) Una llamada automática que guarda el estado del juego cada cierto tiempo
- d) El proceso de Unity para compilar los scripts en tiempo de ejecución

**Respuesta:** b) El proceso del Garbage Collector que libera memoria de objetos no usados, pausando temporalmente todos los demás procesos

---

## SECCIÓN B — COMPLETAR Y RELACIONAR (20 puntos)

### Parte B1 — Completar espacios en blanco (10 pts — 2 pts c/u)

1. El valor de tiempo por frame para alcanzar 90 FPS es 11.11 milisegundos. Si algún proceso supera ese valor, la app baja de 90 FPS.

2. Para aplicar GPU Instancing, el material del objeto debe tener activada la opción   Enable GPU Instancing en el Inspector del material.

3. El comando de Unity para acceder al Profiler es: Window → Analysis → Profiler.

4. Cuando un objeto 3D tiene LOD configurado y la cámara se aleja lo suficiente, el sistema lo marca como Culled, es decir, deja de renderizarlo completamente.

5. `GetComponent<Renderer>()` llamado en `void **Start**()` (método de inicio, una sola vez) es la práctica correcta para cachear la referencia.

---

### Parte B2 — Relacionar columnas (10 pts — 1 pt c/u)

| Columna A — Técnica / Concepto | Tu respuesta | Columna B — Descripción |
|-------------------------------|-------------|------------------------|
| 1. Static Batching | C | A. No renderiza objetos que están detrás de otros |
| 2. GPU Instancing | D | B. Reduce triángulos según la distancia a la cámara |
| 3. LOD Group | B | C. Agrupa objetos estáticos con el mismo material en 1 Draw Call |
| 4. Occlusion Culling | A | D. Renderiza muchas copias del mismo mesh en 1 Draw Call |
| 5. Baked Lighting | E | E. Pre-calcula la iluminación y la guarda en texturas |
| 6. Single Pass Stereo | F | F. Renderiza ambos ojos en una sola pasada (VR) |
| 7. GC Alloc | G | G. Memoria en heap generada por objetos temporales |
| 8. MaterialPropertyBlock | H | H. Permite propiedades únicas por instancia sin romper batching |
| 9. Draw Call | I | I. Instrucción CPU → GPU para renderizar un objeto |
| 10. Fixed Foveated Rendering | J | J. Menor resolución en bordes del campo visual VR |

---

## SECCIÓN C — ANÁLISIS Y REFLEXIÓN (30 puntos)

### Pregunta C1 (8 pts)

Un estudiante tiene este código en su proyecto AR:

```csharp
void Update()
{
    GameObject obj = GameObject.Find("CuboAR");
    obj.GetComponent<Renderer>().material.color = new Color(
        Mathf.Sin(Time.time), 0.5f, 0.5f);
    Debug.Log("Color actualizado: " + obj.name);
}
```

a) Identifica **todos** los problemas de rendimiento en este código (mínimo 3). (4 pts)

b) Reescribe el código optimizado manteniendo la funcionalidad (el color sigue cambiando con el tiempo). (4 pts)

private Renderer _renderer;
private static readonly int ColorID = Shader.PropertyToID("_Color");
private MaterialPropertyBlock _propBlock;

void Start()
{
    GameObject obj = GameObject.Find("CuboAR");
    if (obj != null) {
        _renderer = obj.GetComponent<Renderer>();
    }
    _propBlock = new MaterialPropertyBlock();
}

void Update()
{
    if (_renderer == null) return;
    
    // Usamos MaterialPropertyBlock para no instanciar materiales nuevos
    float lerp = Mathf.Sin(Time.time);
    _renderer.GetPropertyBlock(_propBlock);
    _propBlock.SetColor(ColorID, new Color(lerp, 0.5f, 0.5f));
    _renderer.SetPropertyBlock(_propBlock);
}

### Pregunta C2 (8 pts)

Compara **Baked Lighting** y **Real-time Lighting** en el contexto de una app AR móvil:

a) Explica cuál es más apropiada para una escena AR estática (objetos que no se mueven) y justifica tu respuesta en términos de rendimiento. (4 pts)
El Baked Lighting es más apropiado. En AR móvil, el presupuesto de GPU es muy limitado. El baking calcula luces y sombras en el editor y las guarda en texturas (lightmaps), eliminando el costo de cálculo de iluminación en tiempo real. Esto permite ahorrar batería y mantener FPS estables.

b) ¿En qué escenario específico de AR sería NECESARIO usar iluminación en tiempo real en lugar de baked? (4 pts)
Sería necesario en un escenario donde interactuamos con el entorno de forma dinámica, por ejemplo: si el usuario tiene una linterna virtual que ilumina objetos, o si hay un ciclo día/noche en tiempo real donde las sombras deben rotar según la posición del sol.

### Pregunta C3 — Mini caso de análisis (14 pts)

**Situación:** Tu equipo desarrolló la siguiente experiencia AR para el proyecto grupal: una sala de exhibición virtual con 150 cuadros 3D (cada uno con textura única de 2048×2048 sin comprimir), 20 luces en tiempo real, un script `ExhibicionManager.cs` que en `Update()` busca todos los cuadros con `FindObjectsOfType<CuadroAR>()` y calcula la distancia a la cámara, y sombras activadas en todos los objetos. El resultado: 8 FPS en un celular Snapdragon 720G.

**Pregunta C3a** (7 pts): Identifica los 4 problemas principales de rendimiento en orden de gravedad. Para cada uno: nombra el problema, explica por qué es grave y propón la técnica de optimización específica.

1.- Texturas 2K sin comprimir: 150 cuadros con texturas pesadas saturarán la VRAM del     celular inmediatamente. Solución: Comprimir a ASTC y reducir resolución a 512 o 1024.

2.- 20 Luces en tiempo real: Es inviable para un Snapdragon 720G. Solución: Usar Baked Lighting para el entorno y dejar máximo 1 o 2 luces dinámicas.

3.- FindObjectsOfType en Update: Buscar 150 objetos cada frame mata el rendimiento de la CPU. Solución: Hacer la búsqueda una sola vez en Start() y guardar los cuadros en una Lista o Array.

4.- Sombras activadas en todo: El cálculo de mapas de sombras es muy costoso. Solución: Desactivar sombras en objetos pequeños y usar sombras "baked" o "blob shadows".

**Pregunta C3b** (7 pts): El docente dice: "Primero midan, después optimicen". Describe el proceso exacto de 5 pasos que seguirías en Unity para diagnosticar correctamente el problema antes de tocar una sola línea de código o un solo ajuste de material.

1.- Habilitar el Profiler: Conectar el celular a Unity y ver si el cuello de botella es CPU o GPU.

2.- Revisar el Frame Debugger: Ver cuántos Draw Calls hay y por qué no se están agrupando (batching).

3.- Analizar Memory Profiler: Comprobar si las texturas están ocupando demasiada memoria de video (VRAM).

4.- Comprobar el Physics Profiler: Descartar que el cálculo de distancias o colisiones esté afectando.

5.- GPU Profiler (en dispositivo): Verificar si el Overdraw (muchos objetos transparentes o capas una sobre otra) es el culpable.

## SECCIÓN D — PREGUNTAS AVANZADAS Y DE CASO (30 puntos)

### Caso profesional (15 pts)

**Contexto:** La empresa *Lima XR Studios* ganó un contrato para desarrollar una app de entrenamiento VR para mineros de la empresa Antamina (Perú). La simulación muestra un túnel minero de 500m de largo con: 2,000 objetos 3D (rocas, equipos, señales de seguridad), 8 tipos de materiales distintos (pero muchos objetos comparten el mismo material), explosiones de partículas dinámicas, física activa para simular caída de rocas, y 15 scripts de lógica de entrenamiento corriendo en Update. El headset objetivo es Meta Quest 2 (GPU: Adreno 650, 6GB RAM).

**Pregunta D1** (5 pts): Diseña una **estrategia de optimización completa** para este proyecto. Organiza tu respuesta en una tabla con: técnica aplicada, por qué aplica a este caso específico, impacto esperado en FPS, y si requiere modificar los assets 3D o solo configuración de Unity.

| Técnica Aplicada | ¿Por qué aplica a este caso específico? | Impacto esperado en FPS | ¿Modifica Assets o solo Configuración? |
| :--- | :--- | :--- | :--- |
| **Occlusion Culling** | El túnel es largo (500m). No tiene sentido renderizar rocas o equipos que están detrás de las paredes o en curvas. | **Muy Alto (+20-30 FPS)** | Solo Configuración |
| **GPU Instancing** | Hay 2,000 objetos, muchos son rocas y señales idénticas. Permite dibujarlos todos en un solo Draw Call. | **Alto** | Solo Configuración (Material) |
| **LOD Groups** | Los equipos mineros y rocas lejanas no necesitan todos sus polígonos si el usuario está a 50 metros. | **Medio / Alto** | Modifica Assets (requiere modelos 3D simplificados) |
| **Compresión ASTC** | El Quest 2 tiene memoria limitada. ASTC reduce el peso de las texturas en la VRAM sin perder mucha calidad. | **Medio** | Solo Configuración (Import settings) |
| **Baked Lighting** | Las luces del túnel son fijas. Calcular sombras en tiempo real para 2,000 objetos mataría el rendimiento. | **Muy Alto** | Solo Configuración (Baking de Lightmaps) |
| **Static Batching** | Las paredes del túnel y señales de seguridad no se mueven. Unity las combina en un solo bloque de renderizado. | **Alto** | Solo Configuración (Marcar como Static) |

**Pregunta D2** (5 pts): El físico de "caída de rocas" usa Rigidbody en 500 objetos simultáneamente. Propón una solución que mantenga el realismo visual de la simulación sin comprometer el rendimiento. (Pista: no todas las rocas necesitan física activa al mismo tiempo.)

Usar un sistema de Object Pooling y Activación por Proximidad (Trigger Zones).
Solución técnica: Desactivar por completo los componentes Rigidbody y Collider de las 500 rocas por defecto, o marcarlas como isKinematic = true.
Lógica: Colocar Triggers invisibles a lo largo del túnel. Solo cuando el minero entra en una zona específica (ej. zona de derrumbe), el script activa el Rigidbody únicamente de las 10-15 rocas que realmente caerán en ese momento. Una vez que caen y quedan estáticas en el suelo, se desactiva nuevamente su Rigidbody y se marcan como estáticas (isKinematic = true).

**Pregunta D3** (5 pts): "¿Cómo implementarías un sistema de LOD automático en runtime para el túnel, donde el nivel de detalle cambia dinámicamente según la posición del usuario y el FPS actual?"

Se puede implementar un script observador que mida el frame rate dinámicamente y ajuste el multiplicador global de calidad de LODs mediante la API de Unity QualitySettings.lodBias.
Si el FPS baja del umbral crítico (ej. < 72 FPS en Quest 2), el sistema reduce el QualitySettings.lodBias (por ejemplo, de 1.0 a 0.5), lo que fuerza a Unity a mostrar las versiones low-poly (LOD 1 o LOD 2) más cerca del jugador, liberando carga de GPU.
Si el rendimiento es estable y sobra margen (> 85 FPS), el lodBias se restaura gradualmente para ofrecer la máxima fidelidad gráfica.

---

### Pregunta de diseño (8 pts)

> "¿Cómo implementarías un sistema de 'Adaptive Quality' para tu proyecto XR que automáticamente reduce la calidad visual cuando el FPS cae por debajo de 60, y la restaura cuando el FPS sube? Describe la lógica del script en pseudocódigo o C# real."

using UnityEngine;
using UnityEngine.XR;

public class AdaptiveQualityXR : MonoBehaviour
{
    [SerializeField] private float targetFPS = 60.0f;
    [SerializeField] private float evaluationInterval = 2.0f;
    
    private float _timeAccumulator = 0.0f;
    private int _frameCount = 0;
    private float _currentViewportScale = 1.0f;

    void Update()
    {
        _timeAccumulator += Time.unscaledDeltaTime;
        _frameCount++;

        if (_timeAccumulator >= evaluationInterval)
        {
            float currentFPS = _frameCount / _timeAccumulator;
            AdjustQuality(currentFPS);

            _timeAccumulator = 0.0f;
            _frameCount = 0;
        }
    }

    private void AdjustQuality(float fps)
    {
        // Si los FPS caen por debajo del objetivo
        if (fps < targetFPS - 5.0f)
        {
            if (_currentViewportScale > 0.5f)
            {
                _currentViewportScale -= 0.1f;
                XRSettings.renderViewportScale = _currentViewportScale;
                QualitySettings.shadowDistance = Mathf.Max(10f, QualitySettings.shadowDistance - 10f);
            }
        }
        // Si el rendimiento es excelente, recuperamos calidad gradualmente
        else if (fps > targetFPS + 10.0f && _currentViewportScale < 1.0f)
        {
            _currentViewportScale += 0.05f;
            XRSettings.renderViewportScale = _currentViewportScale;
            QualitySettings.shadowDistance += 5f;
        }
    }
}

---

### Pregunta de pensamiento crítico (7 pts)

> "Un compañero propone: 'Para optimizar nuestra app AR, vamos a reducir la resolución de pantalla del celular al 50% — así el GPU renderiza menos píxeles y ganamos FPS'. ¿Cuál es el riesgo de esta estrategia y en qué contextos XR específicos podría ser aceptable vs. inaceptable?"

 El riesgo de la estrategía es reducir la resolución de renderizado al 50% disminuye drásticamente el píxel fill rate, pero causa una gran degradación de la imagen, produciendo aliasing severo, borrosidad generalizada y pérdida de legibilidad.

 En qué contextos XR es ACEPTABLE:
En aplicaciones o juegos VR de acción rápida donde el jugador está en constante movimiento y prioriza la fluidez (FPS estables) por sobre los detalles visuales estáticos para evitar el mareo.

En qué contextos XR es INACEPTABLE:
En aplicaciones AR/VR médicas, industriales o educativas (como la simulación minera de Antamina) donde el usuario necesita leer etiquetas de advertencia, textos de interfaces (UI), interpretar diagramas técnicos o identificar fisuras finas en materiales. En estos casos, la borrosidad genera fatiga visual extrema y errores operativos.

---

## RÚBRICA DE AUTOEVALUACIÓN

| Criterio | Cumplido |
|----------|---------|
| Respondí las 10 preguntas de opción múltiple | ☑ |
| Completé los 5 espacios en blanco de B1 | ☑ |
| Relacioné todas las 10 columnas de B2 | ☑ |
| En C1 identifiqué mínimo 3 problemas y escribí código optimizado | ☑ |
| En C2 expliqué la diferencia con ejemplo concreto | ☑ |
| En C3 identifiqué 4 problemas con técnicas específicas | ☑ |
| En D1 mi tabla de estrategia tiene mínimo 5 técnicas | ☑ |
| En D2 propuse solución de física que no requiere 500 Rigidbodies activos | ☑ |
| Entregué como `.md` en la rama correcta de GitHub | ☑ |

---

*PSISP08075 | Universidad Autónoma del Perú | Ingeniería de Sistemas | Semana 12 | 2026-1*
