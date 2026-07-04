# S13 — SESIÓN DE CLASE COMPLETA
## Curso: Realidad Virtual y Aumentada | PSISP08075
### Semana 13 — Accesibilidad en RA y RV

---

| Campo | Detalle |
|-------|---------|
| **Curso** | Realidad Virtual y Aumentada — PSISP08075 |
| **Semana** | 13 |
| **Tema** | Accesibilidad en RA y RV — diseño inclusivo para experiencias XR |
| **Valor transversal** | Creatividad en el análisis de casos inclusivos y los ajustes de accesibilidad al proyecto |
| **Logro de aprendizaje** | Al finalizar la sesión, el estudiante integra criterios de accesibilidad en la experiencia XR, demostrando creatividad en el diseño inclusivo |
| **Duración total** | 3 horas (180 min) + 20 min receso |
| **Modalidad** | Presencial con práctica en equipo |

---

## TABLA DE CONTENIDOS

1. [Cronograma](#cronograma)
2. [INICIO](#inicio)
3. [UTILIDAD](#utilidad)
4. [TRANSFORMACIÓN](#transformacion)
   - 4.1 ¿Qué es accesibilidad en XR y por qué difiere de la web?
   - 4.2 El modelo social de la discapacidad aplicado al diseño XR
   - 4.3 Accesibilidad visual en XR
   - 4.4 Accesibilidad motriz en XR
   - 4.5 Accesibilidad cognitiva en XR
   - 4.6 Accesibilidad auditiva en XR
   - 4.7 Cybersickness como barrera de accesibilidad
   - 4.8 Herramientas y estándares: WCAG-XR, Unity Accessibility, MRTK
5. [RECESO](#receso)
6. [PRÁCTICA](#practica)
7. [CIERRE](#cierre)
8. [Guion verbal sugerido](#guion)
9. [Casos reales recomendados](#casos)
10. [Evaluación formativa](#eval)
11. [Referencias APA 7](#referencias)

---

## CRONOGRAMA {#cronograma}

| # | Bloque | Actividad | Duración | Responsable |
|---|--------|-----------|----------|-------------|
| 1 | INICIO | Rompe-hielo + Logro + Revisión S12 + Diagnóstico | 20 min | Docente |
| 2 | UTILIDAD | Impacto profesional de la accesibilidad XR | 10 min | Docente |
| 3 | TRANSFORMACIÓN | Visual, Motriz, Cognitiva, Auditiva, Cybersickness, Estándares | 70 min | Docente activo |
| — | **RECESO** | — | **20 min** | — |
| 4 | PRÁCTICA | Auditoría de accesibilidad grupal + ejercicio individual | 40 min | Estudiantes |
| 5 | CIERRE | Síntesis + metacognición + puente S14 | 10 min | Docente |

---

## 1. INICIO (20 min) {#inicio}

### a) ROMPE-HIELO — "Un minuto sin una mano" (5 min)

**Instrucción verbal al docente:**

> "Vamos a hacer un experimento de 60 segundos. Pongan la mano no dominante detrás de la espalda — bien escondida, sin usarla. Ahora intenten hacer estas tres cosas: desbloquear el celular, escribir su nombre en un papel, y abrir la mochila para sacar un lápiz. Tienen 60 segundos."

Dejar que lo intenten. Al terminar:

> "¿Qué sintieron? ¿Frustración? ¿Cuánto tiempo les tomó? Ahora imaginen que esa es su condición permanente. Y ahora imaginen que tienen que usar unas gafas de VR donde todos los controles requieren dos manos. ¿Esa app de VR los incluye o los excluye? Eso es accesibilidad: diseñar para que nadie quede afuera."

**Propósito:** la experiencia corporal de la limitación genera empatía inmediata y establece el marco emocional del tema antes de la teoría.

---

### b) LOGRO DE APRENDIZAJE (3 min)

**Guion verbal textual:**

> "Hoy el logro tiene tres dimensiones. Primera: van a entender qué significa accesibilidad en XR — y por qué es diferente y más compleja que en una app web o móvil convencional. Segunda: van a aprender a auditar una experiencia XR usando criterios de accesibilidad real — los mismos que usan las empresas cuando lanzan apps en el Quest Store o en el App Store. Tercera: van a aplicar al menos dos ajustes de accesibilidad concretos a su proyecto grupal.
>
> El valor que trabajamos es la creatividad. No hay una sola solución de accesibilidad que funcione para todos — necesitan creatividad para inventar soluciones que funcionen dentro de las restricciones técnicas de XR y que sean genuinamente útiles para personas con discapacidad. No queremos checkbox de accesibilidad. Queremos diseño que incluya de verdad."

---

### c) REVISIÓN SESIÓN ANTERIOR — S12: Optimización y Rendimiento (7 min)

**Pregunta 1:**

> "¿Qué herramienta de Unity usamos para diagnosticar el cuello de botella de rendimiento? ¿Qué diferencia hay entre un problema CPU bound y uno GPU bound?"

**Respuesta esperada:**
El Unity Profiler (Window → Analysis → Profiler). CPU bound: el cuello de botella está en los scripts, física, Update() — el GPU espera al CPU. GPU bound: el cuello de botella está en rendering (Camera.Render alto ms) — muchos draw calls, shaders pesados, sombras dinámicas. La diferencia importa porque la solución es diferente: CPU bound → optimizar scripts/física; GPU bound → batching, LODs, baked lighting.

**Si responde mal:** "Recuerden la analogía: el CPU le manda trabajo al GPU. Si el CPU tarda mucho = CPU bound. Si el GPU tarda mucho en procesar lo que le mandaron = GPU bound. El Profiler muestra exactamente cuánto tarda cada uno."

---

**Pregunta 2:**

> "¿Cómo funciona GPU Instancing y en qué condición es aplicable?"

**Respuesta esperada:**
GPU Instancing renderiza múltiples instancias del mismo mesh con el mismo material en un solo Draw Call. Para que funcione: mismo mesh, mismo material con "Enable GPU Instancing" activado. El GPU procesa todas las instancias en paralelo con diferentes posiciones/rotaciones/escalas. Ejemplo: 300 árboles idénticos = 1 Draw Call en lugar de 300.

---

**Pregunta 3:**

> "¿Qué es el GC Alloc en el Profiler y cómo se evita en scripts de Unity?"

**Respuesta esperada:**
GC Alloc es la cantidad de memoria en heap generada por objetos temporales en cada frame. El Garbage Collector (GC) limpia esa memoria periódicamente causando pausas (stutters). Se evita: cacheando referencias en Awake (no GetComponent en Update), declarando listas como campos de clase (no new List<> en Update), evitando string concatenation con "+" en Update (usar StringBuilder), y eliminando Debug.Log en Update (I/O síncrono).

---

### d) DIAGNÓSTICO INICIAL (5 min)

**Pregunta 1:** "¿Qué porcentaje de la población mundial tiene algún tipo de discapacidad? ¿Lo saben de memoria?"

**Respuesta esperada:** Según la OMS (2023), aproximadamente el **16% de la población mundial** vive con alguna forma significativa de discapacidad — más de 1,300 millones de personas. Esta cifra no incluye discapacidades temporales (un brazo roto, cirugía ocular reciente) ni situacionales (usar el celular con sol intenso, en un espacio ruidoso). Si se incluyen discapacidades situacionales y temporales, el número supera el 50% de la población en algún momento de su vida.

**Pregunta 2:** "¿Conocen el acrónimo WCAG? ¿Para qué sirve?"

**Respuesta esperada:** WCAG = Web Content Accessibility Guidelines. Son las pautas internacionales de accesibilidad para contenido web, publicadas por el W3C. Define criterios de éxito (Nivel A, AA, AAA) para que el contenido sea: Perceptible, Operable, Comprensible y Robusto (POUR). La mayoría de legislaciones de accesibilidad del mundo (ADA en USA, EN 301 549 en Europa) referencian WCAG como estándar mínimo. XR plantea nuevos desafíos que WCAG web no cubre completamente.

**Pregunta 3:** "¿Conocen alguna app o juego de VR/AR que haya hecho algo especial para personas con discapacidad?"

**Respuesta esperada (aceptar cualquier respuesta correcta):** Xbox Game Pass / Microsoft tiene el controlador adaptativo para personas con movilidad reducida. Sony tiene opciones de accesibilidad en PlayStation VR2 (asistencia de subtítulos, modo de control alternativo). The Last of Us (PS5) implementó 60+ opciones de accesibilidad incluyendo audio descriptivo — fue premiado por organizaciones de discapacidad. Si nadie sabe: es exactamente el punto — la accesibilidad en XR es un área emergente y subdesarrollada.

---

## 2. UTILIDAD (10 min) {#utilidad}

### Por qué la accesibilidad en XR es urgente y rentable

**Dato de impacto:**
La OMS estima que **1 de cada 6 personas en el mundo** vive con alguna discapacidad significativa. El mercado global de tecnología asistiva alcanzará **US$ 32 mil millones en 2024** (Grand View Research, 2024). Las empresas que ignoran la accesibilidad no solo pierden ese mercado — también enfrentan riesgos legales crecientes.

**Caso legal real:**
En 2022, **Beyoncé's Parkwood Entertainment** fue demandada por una fan ciega porque su sitio web no era accesible para lectores de pantalla. El año anterior, **Netflix** fue demandado por la National Association of the Deaf por falta de subtítulos. En XR, las primeras demandas de accesibilidad ya están llegando en EEUU — empresas con apps en el Quest Store sin opciones para personas con visión reducida.

**El "efecto bordillo":**
El término viene del diseño urbano: las rampas en bordillos se diseñaron para sillas de ruedas, pero las usan madres con coches de bebé, repartidores, personas mayores, ciclistas. Lo mismo en tecnología: el modo oscuro se diseñó para personas con fotosensibilidad → lo usa todo el mundo. Los subtítulos se diseñaron para sordos → los usan personas en espacios ruidosos. Las soluciones de accesibilidad mejoran la experiencia de TODOS los usuarios.

**Aplicación en empresas reales XR:**

- **Microsoft HoloLens/MRTK:** las Mixed Reality Toolkit incluye desde 2021 un paquete completo de accesibilidad — high contrast mode, narrator support, reduced motion mode.
- **Meta Quest:** en 2023 Meta lanzó "Quest Accessibility" con soporte para subtítulos automáticos, ajuste de IPD (distancia interpupilar) para condiciones visuales, y opciones de confort anti-cybersickness.
- **Apple Vision Pro (2024):** incluye: VoiceOver (lector de pantalla en 3D), zoom, display accommodations, reducción de transparencias, opciones de confort vestibular.
- **Nianitic (AR):** Pokémon GO agregó controles alternativos para jugadores con movilidad reducida tras una campaña de usuarios con discapacidad motriz.

### Pregunta retadora de apertura

> "Si diseñan una app de VR para cirugía virtual y uno de los cirujanos que la usará tiene daltonismo (no distingue rojo y verde), ¿en qué parte concreta del diseño XR ese daltonismo sería un problema de seguridad, no solo de comodidad?"

**Respuesta esperada:**
Si la app usa color rojo para indicar tejido dañado o arteria cortada y verde para tejido sano, el cirujano con daltonismo rojo-verde (el tipo más común, afecta al 8% de los hombres) no puede distinguirlos. En entrenamiento esto significa errores sin consecuencia; en cirugía real asistida por AR significa riesgo de vida. La solución no es "quitar el color" sino agregar una señal alternativa: forma (icono de advertencia), patrón (rayado vs liso), texto overlay ("ARTERIA"), o sonido. Esta es exactamente la lógica del diseño accesible: no eliminar la información, sino asegurar que llega por más de un canal sensorial.

---

## 3. TRANSFORMACIÓN (70 min) {#transformacion}

### 3.1 ¿Qué es accesibilidad en XR y por qué difiere de la web? (8 min)

**Explicación conceptual:**

La accesibilidad convencional (WCAG para web) asume una interfaz 2D con teclado, ratón y pantalla plana. XR rompe esos supuestos en todas las dimensiones:

```
DIFERENCIAS ENTRE ACCESIBILIDAD WEB Y ACCESIBILIDAD XR
═══════════════════════════════════════════════════════════════════════
DIMENSIÓN          WEB/2D                    XR (AR/VR)
───────────────    ───────────────────────   ────────────────────────────
Espacio            2D (pantalla plana)       3D (entorno inmersivo)
Input              Teclado + ratón           Gestos, gaze, voz, controllers
Navegación         Click/Tab/Swipe           Movimiento físico del cuerpo
Orientación        Arriba/abajo (scroll)     360° (puede ser desorientador)
Proximidad         No importa               La distancia a objetos VR importa
Peso del hardware  0 (pantalla existe)       Peso del headset (400-600g)
Fatiga             Visual principalmente     Visual + física (cuello, brazos)
Náuseas            No aplica                Cybersickness (problema grave)
Emergencia         Cerrar pestaña            Quitarse el headset (pausa física)
═══════════════════════════════════════════════════════════════════════
```

**El estándar emergente: XR Accessibility User Requirements (XAUR)**

El W3C publicó en 2023 el documento **"XR Accessibility User Requirements"** (XAUR) como extensión de WCAG para XR. No es aún una norma obligatoria, pero sí la referencia más completa actual. Define requisitos para: usuarios ciegos, con baja visión, daltonismo, sordos, con dificultades motoras, cognitivas, y sensibles al movimiento.

**PREGUNTA AL GRUPO 1:**

> "Si una app web tiene texto alternativo (alt text) para imágenes para que los lectores de pantalla lo lean, ¿qué equivalente necesitaría una app VR para que un usuario ciego pueda 'ver' los objetos 3D del entorno?"

**Respuesta esperada:**
En VR, los objetos 3D necesitan una descripción verbal que el sistema de text-to-speech puede leer cuando el usuario "apunta" o se acerca a ellos. Microsoft lo implementa como "spatial audio descriptions" en HoloLens: cuando el usuario gira la cabeza hacia un objeto, el sistema dice en voz alta qué es ese objeto y su función. Unity tiene el componente `AccessibilityNode` (en el paquete de Accessibility) que permite asignar una etiqueta accesible y descripción a cualquier GameObject — el lector de pantalla del SO los lee al enfocarlos. Adicionalmente: audio espacial que guía al usuario hacia los objetos (el sonido viene de la dirección del objeto), y hápticos que dan feedback de confirmación.

---

### 3.2 El modelo social de la discapacidad aplicado al diseño XR (7 min)

**Explicación conceptual:**

Existen dos modelos para entender la discapacidad con consecuencias opuestas para el diseño:

```
MODELO MÉDICO                        MODELO SOCIAL
─────────────────────────────────    ─────────────────────────────────
La discapacidad está en la persona.  La discapacidad está en el entorno.
El problema: el cuerpo de la person. El problema: las barreras del diseño.
Solución: "curar" o "compensar"      Solución: eliminar las barreras
Ejemplo: "esa persona no puede usar  Ejemplo: "ese controller VR no fue
  el controller VR porque tiene        diseñado para personas con una
  una mano."                           mano."
Diseño resultante: excluye quien      Diseño resultante: incluye desde el
  no encaje en el estándar.            inicio a todos los usuarios.
```

**El espectro de la discapacidad: permanente, temporal, situacional**

```
                  PERMANENTE    TEMPORAL        SITUACIONAL
                  ──────────    ─────────────   ─────────────────────────
Visual            Ceguera       Post-cirugía    Sol directo en la pantalla
Motriz            Parálisis     Brazo roto      Cargar bebé con un brazo
Auditiva          Sordera       Tapón de cera   Espacio muy ruidoso
Cognitiva         Alzheimer     Traumatismo     Distracción intensa/estrés
Sensorial         Epilepsia     Resaca          Primera vez en VR (mareo)
```

**PREGUNTA AL GRUPO 2:**

> "¿Por qué el modelo social de la discapacidad cambia la responsabilidad del diseño XR de una forma práctica? Den un ejemplo concreto con un usuario de Quest VR."

**Respuesta esperada:**
Con el modelo médico, si un usuario con Parkinson (temblor de manos) no puede usar los controllers de Quest porque los botones son pequeños y requieren presión precisa, la "solución" sería decir "esa persona no puede usar VR". Con el modelo social, la responsabilidad está en el diseño: el controller fue diseñado sin considerar temblor de manos. La solución del modelo social: 1) Agrandar las zonas de toque (botones más grandes o lógica de detección de zona ampliada), 2) Añadir modo "hold" en vez de "tap" (más tolerante al temblor), 3) Implementar control por voz como alternativa. El modelo social transforma "esta persona no puede usar mi app" en "mi app no fue diseñada para esta persona — eso es mi error".

---

### 3.3 Accesibilidad visual en XR (12 min)

**Los 4 tipos de discapacidad visual y sus implicaciones XR:**

```
TIPO                 PREVALENCIA   IMPACTO EN XR                SOLUCIÓN XR
────────────────     ───────────   ─────────────────────────    ─────────────────────
Daltonismo           8% hombres    Colores como único código    Añadir forma/texto/patrón
(rojo-verde)         0.5% mujeres  de información → ilegible
Baja visión          246M personas Texto pequeño ilegible,      Escalado de UI, alto contraste
                                   elementos a distancia VR
Ceguera total        39M personas  Entorno visual completamente Audio descriptions, hápticos
                                   inaccesible sin ayuda
Fotosensibilidad     3-5% pop.     Flashes > 3Hz → convulsiones Modo sin destellos,
(epilepsia)                        (Game Over legal en muchos   máx. flash rate configurado
                                   mercados)
```

**Implementación en Unity — Modo Alto Contraste:**

```csharp
using UnityEngine;
using UnityEngine.UI;

/// <summary>
/// Gestor de accesibilidad visual que aplica modo alto contraste
/// a todos los elementos UI de la escena XR.
/// Se activa desde el menú de configuración de la app.
/// </summary>
public class GestorAccesibilidadVisual : MonoBehaviour
{
    [Header("Paleta de Alto Contraste")]
    // WCAG 2.1 exige ratio de contraste mínimo 4.5:1 (normal) o 3:1 (grande)
    public Color colorTextoAltoContraste  = Color.white;     // #FFFFFF
    public Color colorFondoAltoContraste  = Color.black;     // #000000
    public Color colorAcentoAltoContraste = new Color(1f, 1f, 0f); // Amarillo #FFFF00

    [Header("Escalado de texto")]
    [Range(1f, 3f)]
    public float factorEscalaTexto = 1f; // 1.0 = normal, 1.5 = grande, 2.0 = muy grande

    private bool modoAltoContrasteActivo = false;

    // Colores originales (para poder restaurar)
    private Color[] coloresOriginalesTextos;
    private Text[] todosLosTextos;

    void Start()
    {
        // Cachear todos los textos de la escena al inicio
        todosLosTextos = FindObjectsOfType<Text>();
        coloresOriginalesTextos = new Color[todosLosTextos.Length];

        for (int i = 0; i < todosLosTextos.Length; i++)
            coloresOriginalesTextos[i] = todosLosTextos[i].color;
    }

    /// <summary>
    /// Alterna el modo alto contraste. Llamado desde botón de configuración.
    /// </summary>
    public void ToggleAltoContraste()
    {
        modoAltoContrasteActivo = !modoAltoContrasteActivo;

        if (modoAltoContrasteActivo)
            AplicarAltoContraste();
        else
            RestaurarColoresOriginales();
    }

    void AplicarAltoContraste()
    {
        for (int i = 0; i < todosLosTextos.Length; i++)
        {
            todosLosTextos[i].color    = colorTextoAltoContraste;
            // Escalar también el tamaño de fuente
            todosLosTextos[i].fontSize =
                Mathf.RoundToInt(todosLosTextos[i].fontSize * factorEscalaTexto);
        }

        // Cambiar el fondo del Canvas a negro
        var imagenes = FindObjectsOfType<Image>();
        foreach (var img in imagenes)
            img.color = colorFondoAltoContraste;

        Debug.Log("[Accesibilidad] Alto contraste ACTIVADO");
    }

    void RestaurarColoresOriginales()
    {
        for (int i = 0; i < todosLosTextos.Length; i++)
        {
            todosLosTextos[i].color    = coloresOriginalesTextos[i];
            todosLosTextos[i].fontSize =
                Mathf.RoundToInt(todosLosTextos[i].fontSize / factorEscalaTexto);
        }
        Debug.Log("[Accesibilidad] Alto contraste DESACTIVADO");
    }

    /// <summary>
    /// Verificar si el ratio de contraste cumple WCAG 2.1 AA (mínimo 4.5:1)
    /// </summary>
    public static float CalcularRatioContraste(Color c1, Color c2)
    {
        float l1 = LuminanciaRelativa(c1);
        float l2 = LuminanciaRelativa(c2);
        float mayor = Mathf.Max(l1, l2);
        float menor = Mathf.Min(l1, l2);
        return (mayor + 0.05f) / (menor + 0.05f);
    }

    // Fórmula de luminancia relativa según WCAG 2.1
    static float LuminanciaRelativa(Color c)
    {
        float r = c.r <= 0.03928f ? c.r / 12.92f : Mathf.Pow((c.r + 0.055f) / 1.055f, 2.4f);
        float g = c.g <= 0.03928f ? c.g / 12.92f : Mathf.Pow((c.g + 0.055f) / 1.055f, 2.4f);
        float b = c.b <= 0.03928f ? c.b / 12.92f : Mathf.Pow((c.b + 0.055f) / 1.055f, 2.4f);
        return 0.2126f * r + 0.7152f * g + 0.0722f * b;
    }
}
```

**PREGUNTA AL GRUPO 3:**

> "¿Por qué el texto AR proyectado en un plano con fondo transparente es particularmente problemático para personas con baja visión?"

**Respuesta esperada:**
En AR, el texto se superpone sobre el fondo del mundo real, que es completamente variable e impredecible (puede ser una pared blanca, un fondo oscuro, una superficie con muchos patrones). Si el texto es blanco y el fondo resulta ser blanco (una pared), el ratio de contraste baja a 1:1 — literalmente ilegible. No hay forma de garantizar el contraste mínimo de 4.5:1 (WCAG) cuando el fondo es el mundo real. Soluciones: 1) Panel semiopaco detrás del texto (el "backing panel" — como una caja oscura semi-transparente detrás del texto blanco), 2) Text outline (borde de color opuesto alrededor de cada letra), 3) Permitir al usuario personalizar el color del texto Y el panel de fondo. Sin estas soluciones, el texto AR siempre será ilegible en algún fondo real.

---

**Mini actividad (3 min):**
Abrir un simulador de daltonismo online (https://www.color-blindness.com/coblis-color-blindness-simulator/) y subir una captura de su proyecto XR. Compartir: ¿qué información se pierde con cada tipo de daltonismo?

---

### 3.4 Accesibilidad motriz en XR (12 min)

**Las principales barreras motoras en XR:**

```
BARRERA                          TIPO DE USUARIO AFECTADO
──────────────────────           ────────────────────────────────────
Requerir dos manos               Amputación, parálisis, brazo roto
Movimientos precisos             Parkinson, temblor esencial, artritis
Movimiento físico requerido      Silla de ruedas, movilidad reducida
Duración sostenida del brazo     Todos los usuarios (fatiga "gorilla arm")
Agarre/squeeze del controller    Fuerza manual reducida
Movimientos de cabeza rápidos    Problemas cervicales, mareos

La "fatiga gorilla arm": mantener los brazos levantados en VR
por más de 5 minutos causa fatiga muscular significativa,
incluso en usuarios sin discapacidad.
```

**Estrategias de diseño inclusivo para movilidad reducida:**

```
ESTRATEGIA            IMPLEMENTACIÓN EN UNITY          ALTERNATIVA PARA
────────────────      ───────────────────────────────   ────────────────
Modo gaze-only        GazeCursor + Dwell timer          Sin uso de manos
Control por voz       Dictation + comandos de voz       Sin movimiento de manos
Switch access         1 botón para todas las acciones   Movilidad muy reducida
Asistencia de apunt.  Magnetic cursor (snap to nearest) Temblor, precisión reducida
Modo reposado         Todo accesible desde posición     Cansancio, silla de ruedas
                      sentada sin mover brazos
Tiempo ajustable      No timeout forzado, pausas        Procesamiento lento
```

**Implementación — Dwell Time (selección por mirada):**

```csharp
using UnityEngine;
using UnityEngine.Events;

/// <summary>
/// Permite seleccionar un objeto simplemente mirándolo durante un tiempo
/// configurable. Alternativa a los botones físicos para usuarios con
/// movilidad reducida.
/// Usado en: HoloLens MRTK, Samsung Gear VR, Google Cardboard.
/// </summary>
public class SeleccionPorMirada : MonoBehaviour
{
    [Header("Configuración de Dwell")]
    [Tooltip("Tiempo en segundos para activar la selección por mirada")]
    [Range(0.5f, 5f)]
    public float tiempoDwell = 1.5f;  // 1.5s es el estándar de MRTK

    [Header("Feedback visual (opcional)")]
    public GameObject anilloProgreso; // UI circular de progreso
    public UnityEvent alSeleccionar;  // acción a ejecutar al completar

    private float tiempoMirandoActual = 0f;
    private bool mirandoAhora = false;
    private bool yaActivado = false;   // evitar activación repetida

    /// <summary>
    /// Llamado por el sistema de gaze cuando el cursor entra en este objeto.
    /// Conectar al evento OnPointerEnter del EventTrigger.
    /// </summary>
    public void AlEntrarMirada()
    {
        mirandoAhora = true;
        yaActivado = false;
        tiempoMirandoActual = 0f;

        if (anilloProgreso != null)
            anilloProgreso.SetActive(true);
    }

    /// <summary>
    /// Llamado cuando el cursor sale de este objeto.
    /// </summary>
    public void AlSalirMirada()
    {
        mirandoAhora = false;
        tiempoMirandoActual = 0f;
        yaActivado = false;

        if (anilloProgreso != null)
            anilloProgreso.SetActive(false);
    }

    void Update()
    {
        if (!mirandoAhora || yaActivado) return;

        tiempoMirandoActual += Time.deltaTime;

        // Actualizar el anillo de progreso (si existe)
        ActualizarProgreso(tiempoMirandoActual / tiempoDwell);

        // Completar la selección cuando se alcanza el tiempo dwell
        if (tiempoMirandoActual >= tiempoDwell)
        {
            yaActivado = true;
            alSeleccionar.Invoke();  // disparar la acción configurada en Inspector
            Debug.Log($"[Accesibilidad] Selección por mirada completada: {gameObject.name}");
        }
    }

    void ActualizarProgreso(float progreso)
    {
        // Si hay un anillo de progreso (Image con Fill Method = Radial 360)
        if (anilloProgreso == null) return;
        var img = anilloProgreso.GetComponent<UnityEngine.UI.Image>();
        if (img != null) img.fillAmount = Mathf.Clamp01(progreso);
    }
}
```

**PREGUNTA AL GRUPO 4:**

> "Un usuario en silla de ruedas quiere usar su app VR de entrenamiento de escalada. Obviamente no puede hacer los movimientos físicos de escalar. ¿Qué ajustes de accesibilidad implementarían para que pueda usar la app con sentido?"

**Respuesta esperada:**
El objetivo no es que la persona en silla de ruedas "escale" igual que alguien sin discapacidad — es que la app le sea útil. Posibles enfoques creativos: 1) Modo "observador activo": el usuario puede controlar la cámara para ver técnicas de escalada desde ángulos que físicamente serían imposibles incluso para un escalador → valor educativo sin barrera física. 2) Modo de "upper body only": solo los movimientos de brazos y manos, válidos para entrenar técnica de agarre sin requerir movimiento de piernas o posición de pie. 3) Control adaptativo: gamepad o joystick de boca (sip-and-puff) mapeado a los controles de la app. 4) Niveles de intensidad física: el sistema detecta rango de movimiento disponible y adapta la dificultad. La clave: preguntar a usuarios reales con discapacidad qué encuentran valioso de la app — no asumir.

---

### 3.5 Accesibilidad cognitiva en XR (10 min)

**Personas con dificultades cognitivas que usan XR:**

- Alzheimer y demencia (terapia de reminiscencia en VR — Oxford VR)
- Autismo (entrenamiento de habilidades sociales en VR — Floreo, SpectrVR)
- TDAH (hiperfoco potencialmente útil, pero también sobrecarga sensorial)
- Fobias y PTSD (terapia de exposición VR — Oxford VR, PsyTech)
- Discapacidad intelectual (apps educativas VR adaptadas)
- Usuarios sin experiencia tecnológica (adultos mayores en primera VR)

**Principios de diseño cognitivo en XR:**

```
PRINCIPIO              IMPLEMENTACIÓN XR                 ¿POR QUÉ?
─────────────────      ──────────────────────────────    ─────────────────────────
Una tarea a la vez     Sin multitarea forzada en UI       Carga cognitiva reducida
Instrucciones cortas   Max. 7 palabras por instrucción   Memoria de trabajo (7±2)
Progreso visible       Barra de progreso siempre visible  Orientación en el proceso
Feedback inmediato     Respuesta < 0.1 seg a cada acción No dejar al usuario en duda
Reversibilidad         Botón "deshacer" siempre visible   Reduce ansiedad al explorar
Lenguaje simple        Sin jerga técnica en la UI XR      Compresión universal
Pausas disponibles     Botón de pausa accesible siempre   Control del usuario
Consistencia           Los mismos gestos hacen lo mismo   Aprendizaje por repetición
```

**PREGUNTA AL GRUPO 5:**

> "¿Por qué la VR puede ser especialmente beneficiosa para personas con autismo pero al mismo tiempo puede ser una experiencia abrumadora? ¿Qué ajustes de accesibilidad cognitiva resolverían ese conflicto?"

**Respuesta esperada:**
Personas con autismo a menudo tienen hipersensibilidad sensorial — sonidos fuertes, muchos estímulos visuales simultáneos, ambigüedad social pueden ser abrumadores. Al mismo tiempo, la VR ofrece un entorno controlado donde se puede practicar interacción social sin las consecuencias sociales del mundo real — Floreo Technologies usa exactamente esto para entrenamiento de comunicación social. Los ajustes que resuelven el conflicto: 1) "Modo calma": reducir el número de objetos, sonidos y movimientos en la escena, 2) Sin sorpresas: el usuario ve exactamente qué va a pasar antes de que ocurra (preview de cada interacción), 3) Control total del ritmo: nunca hay timeout ni presión de tiempo, 4) Salida rápida siempre disponible: el usuario puede pausar o salir en cualquier momento sin consecuencia, 5) Personalización sensorial: ajuste individual de volumen, brillo, contraste, velocidad de eventos.

---

### 3.6 Accesibilidad auditiva en XR (8 min)

**Implementación de subtítulos espaciales en AR/VR:**

```csharp
using UnityEngine;
using TMPro;

/// <summary>
/// Subtítulos 3D que siguen al usuario en VR/AR.
/// Siempre visibles en la parte inferior del campo visual,
/// independientemente de a dónde mire el usuario.
/// Patrón usado por: Apple Vision Pro, Meta Quest captions.
/// </summary>
public class SubtitulosXR : MonoBehaviour
{
    [Header("UI de subtítulos")]
    public TextMeshProUGUI textoSubtitulo;
    public GameObject panelSubtitulo;

    [Header("Posicionamiento relativo a la cámara")]
    [Tooltip("Distancia al frente de la cámara en metros")]
    public float distanciaAlFrente = 2f;

    [Tooltip("Desplazamiento vertical (negativo = abajo del centro)")]
    public float offsetVertical = -0.5f;

    [Header("Opciones de usuario")]
    public bool subtitulosActivos = true;
    public Color colorTexto = Color.white;
    public Color colorFondo  = new Color(0, 0, 0, 0.7f); // negro semitransparente

    private Camera camaraXR;

    void Start()
    {
        camaraXR = Camera.main;
        panelSubtitulo.SetActive(subtitulosActivos);
        AplicarEstilo();
    }

    void LateUpdate()
    {
        if (!subtitulosActivos) return;

        // Anclar el panel de subtítulos delante de la cámara
        // LateUpdate garantiza que se aplica después de que la cámara se movió
        Vector3 posicionObjetivo = camaraXR.transform.position
            + camaraXR.transform.forward * distanciaAlFrente
            + camaraXR.transform.up     * offsetVertical;

        panelSubtitulo.transform.position = posicionObjetivo;

        // El panel siempre mira hacia la cámara
        panelSubtitulo.transform.LookAt(camaraXR.transform);
        panelSubtitulo.transform.Rotate(0, 180f, 0);
    }

    /// <summary>
    /// Mostrar un subtítulo por una duración determinada.
    /// Llamar desde scripts de audio, narración o interacción.
    /// </summary>
    public void MostrarSubtitulo(string texto, float duracion = 3f)
    {
        if (!subtitulosActivos) return;
        textoSubtitulo.text = texto;
        panelSubtitulo.SetActive(true);
        Invoke(nameof(OcultarSubtitulo), duracion);
    }

    void OcultarSubtitulo() => textoSubtitulo.text = "";

    void AplicarEstilo()
    {
        textoSubtitulo.color = colorTexto;
        // El fondo se aplica al Image del panel
        var fondo = panelSubtitulo.GetComponent<UnityEngine.UI.Image>();
        if (fondo != null) fondo.color = colorFondo;
    }

    public void ToggleSubtitulos()
    {
        subtitulosActivos = !subtitulosActivos;
        panelSubtitulo.SetActive(subtitulosActivos);
    }
}
```

**PREGUNTA AL GRUPO 6:**

> "¿Por qué los subtítulos en VR son más complejos de implementar que en una película o app 2D? ¿Qué problema específico de VR presentan y cómo lo resuelve el script anterior?"

**Respuesta esperada:**
En una película o app 2D, los subtítulos están en una posición fija de la pantalla (abajo centrado) y siempre son visibles. En VR, el usuario puede mirar en cualquier dirección (360°). Si los subtítulos están en una posición fija del mundo 3D (ej: en una pared de la escena), cuando el usuario mira a la derecha, los subtítulos quedan fuera del campo visual y son invisibles. El problema: el usuario tiene que mirar hacia los subtítulos, pero mirar hacia los subtítulos le quita el foco de lo que está pasando en la escena. El script soluciona esto anclando el panel de subtítulos relativo a la cámara (head-locked), de manera que siempre aparece en la misma posición del campo visual del usuario (abajo del centro), sin importar a dónde mire. Esto imita exactamente cómo Apple Vision Pro y Meta Quest implementan sus subtítulos.

---

### 3.7 Cybersickness como barrera de accesibilidad (8 min)

**Definición:**
El cybersickness (o Virtual Reality Sickness) es el conjunto de síntomas análogos al mareo de movimiento — náusea, desorientación, dolor de cabeza, sudoración — causados por discordancia entre las señales visuales (movimiento en VR) y las señales vestibulares (el cuerpo no se mueve).

```
FACTORES QUE AUMENTAN EL CYBERSICKNESS
═════════════════════════════════════════════════════════════════
Factor                  Por qué causa malestar
──────────────────────  ────────────────────────────────────────
FPS < 72               Cada frame perdido = destello perceptible
Latencia > 20ms         Cabeza se mueve antes de que la imagen actualice
FOV incorrecto          Si el FOV del render no coincide con el óptico del lente
Locomoción artificial   Moverse con joystick cuando el cuerpo no se mueve físicamente
Aceleración brusca      El cerebro espera inercia pero no la hay
Parpadeo visual         Cualquier flash regular activa reflejo de náusea
Distancia IPD           Si la distancia interpupilar no está calibrada
═════════════════════════════════════════════════════════════════

USUARIOS MÁS VULNERABLES:
- Mujeres (hasta 2x más susceptibles que hombres — razones hormonales/vestibulares)
- Menores de edad (sistema vestibular en desarrollo)
- Adultos mayores (mayor sensibilidad del sistema vestibular)
- Personas con migrañas o vértigo previo
- Primeros usuarios de VR (adaptación requiere exposición gradual)
```

**Técnicas de mitigación de cybersickness:**

```
TÉCNICA                 IMPLEMENTACIÓN XR                EFECTIVIDAD
───────────────────     ─────────────────────────────    ─────────────
Vignette dinámico       Oscurecer bordes al moverse      Alta — reduce FOV percibido
Teleportación           Moverse teletransportándose       Muy alta — elimina locomoción
Velocidad reducible     Slider de velocidad de movim.    Media — control al usuario
Horizonte fijo          Línea de horizonte siempre nivel  Alta — referencia visual
Descansos programados   Aviso de descanso cada 20 min     Alta — prevención
Reducción de FOV        Estrechar campo de visión al moverse Media — algunos no lo notan
```

**PREGUNTA AL GRUPO 7:**

> "Si su proyecto VR tiene locomoción artificial (el usuario se mueve con joystick), ¿qué 3 técnicas de mitigación de cybersickness implementarían en orden de facilidad de implementación en Unity?"

**Respuesta esperada:**
En orden de facilidad: 1) **Vignette dinámico** (fácil): Post-Processing Volume en Unity con Vignette — al detectar movimiento del joystick, aumentar la intensidad del vignette. Con una corrutina simple: cuando el joystick está activo, aumentar el valor de vignette; cuando para, reducirlo. 2) **Teleportación** (medio): implementar un sistema de teleportación con indicator (el arco de parábola que muestra el destino) en lugar de locomoción continua. Unity XR Interaction Toolkit ya incluye el componente `TeleportationArea` y `TeleportationAnchor`. 3) **Velocidad configurable** (muy fácil): exponer la variable de velocidad de movimiento como un slider en el menú de opciones del juego. El usuario puede reducir la velocidad si siente malestar. Costo: 30 minutos de implementación.

---

### 3.8 Herramientas y estándares: WCAG-XR, Unity Accessibility, MRTK (7 min)

**Ecosistema de estándares:**

```
ESTÁNDAR/HERRAMIENTA          ORGANIZACIÓN    APLICACIÓN XR
────────────────────────────  ──────────────  ─────────────────────────────
WCAG 2.1                      W3C             Base de accesibilidad (web)
XR Accessibility User         W3C             Extensión de WCAG para XR
  Requirements (XAUR)         XAAG
MRTK Accessibility (v3)       Microsoft       HoloLens 2 + Unity
Unity Accessibility Package   Unity Tech.     Unity multi-plataforma
Apple Accessibility           Apple           Vision Pro + iOS AR
Meta Accessibility SDK        Meta            Quest series
Game Accessibility            IGDA            Videojuegos en general
  Guidelines (GAG)
```

**Unity Accessibility Package — configuración básica:**

```
Instalación:
Window → Package Manager → Unity Registry → Accessibility → Install

Componentes principales:
1. AccessibilityNode: agrega información accesible a cualquier GameObject
   - Label: nombre del objeto para el lector de pantalla
   - Hint: descripción de la acción al interactuar
   - Role: tipo de elemento (button, image, text)
   - IsActive: si está activo para el sistema de accesibilidad

2. AccessibilityHierarchy: gestiona qué nodos son visibles para el AT
   (Assistive Technology — lectores de pantalla, etc.)

3. AssistiveTechnology: clase para comunicar con el lector de pantalla del SO
   AssistiveTechnology.Announce("Objeto seleccionado: " + nombre);
```

**PREGUNTA AL GRUPO 8:**

> "¿Qué significa que una app XR cumpla WCAG 2.1 'Nivel AA'? ¿Es suficiente para ser legalmente accesible en Perú o en la Unión Europea?"

**Respuesta esperada:**
WCAG 2.1 define tres niveles: A (mínimo básico), AA (estándar recomendado para la mayoría de contextos), AAA (máxima accesibilidad, difícil de cumplir en su totalidad). Nivel AA incluye: contraste mínimo 4.5:1 para texto, subtítulos para audio, control por teclado, sin pérdida de contenido en zoom 200%, etc. En Perú: la Ley N° 29973 (Ley General de la Persona con Discapacidad) y su reglamento obligan a entidades públicas y algunas privadas a cumplir accesibilidad web, pero la referencia técnica específica no siempre es WCAG — la norma técnica peruana específica es más laxa. En la UE: la Directiva EU 2019/882 (European Accessibility Act) exige AA para servicios digitales. Para una app XR comercial en ambos mercados: cumplir AA es el mínimo para no tener riesgo legal, pero AA fue diseñado para web 2D y no cubre completamente XR — por eso se necesita también el XAUR.

---

## RECESO (20 min) {#receso}

---

## 4. PRÁCTICA (40 min) {#practica}

### a) CASO PRÁCTICO GRUPAL (25 min)

**Escenario:**

> El Ministerio de Educación del Perú lanzó un concurso para desarrollar una app de VR educativa para estudiantes de secundaria que enseñe astronomía — los estudiantes pueden "volar" por el sistema solar, explorar planetas, y hacer experimentos de física orbital. La app será usada en 300 colegios públicos en todo el Perú, incluyendo colegios inclusivos con estudiantes con discapacidad visual, auditiva, motriz y cognitiva. El Ministerio exige que la app cumpla los criterios de accesibilidad del XAUR y sea usable sin adaptaciones especiales por estudiantes con cualquiera de las cuatro discapacidades mencionadas.
>
> El equipo de desarrollo ya tiene el prototipo funcional con estas características actuales: narración de audio para cada planeta, texto informativo en pantalla, navegación por joystick con vuelo libre (locomoción artificial), efectos de sonido 3D, y paleta de colores azul-violeta-turquesa.

**Tarea grupal (grupos de 3-4):**

1. Identificar 5 barreras de accesibilidad específicas en el prototipo actual
2. Proponer el ajuste de accesibilidad concreto para cada barrera (técnica + implementación)
3. Priorizar las 5 soluciones de mayor a menor impacto en usuarios reales
4. Diseñar el menú de accesibilidad de la app (¿qué opciones tendría?)
5. Responder: ¿qué ajuste de accesibilidad beneficiaría también a usuarios sin discapacidad?

**Producto concreto esperado:** tabla de 5 barreras + soluciones + boceto del menú de accesibilidad (puede ser dibujado a mano y fotografiado).

**Preguntas de andamiaje:**
- "¿Los colores azul-violeta-turquesa representan un problema para algún tipo de daltonismo? ¿Cuál específicamente?"
- "¿Un estudiante sordo puede aprovechar la narración de audio? ¿Qué alternativa necesita?"
- "¿La locomoción libre con joystick puede causar malestar en algunos usuarios? ¿Qué otros tipos de movimiento hay disponibles en VR?"
- "¿Un estudiante con parálisis cerebral que solo puede usar movimientos de cabeza podría navegar por el sistema solar? ¿Qué necesitaría?"
- "¿El texto informativo es legible para un estudiante con baja visión que usa el headset a 2 metros del texto virtual?"

**Respuesta modelo:**

| # | Barrera | Ajuste | Impacto | Implementación |
|---|---------|--------|---------|---------------|
| 1 | Sin subtítulos para la narración de audio | Subtítulos 3D anclados a la cámara | Usuarios sordos e hipoacúsicos (~466M mundialmente) | SubtitulosXR.cs (código visto en clase) |
| 2 | Locomoción artificial (joystick + vuelo libre) | Modo teleportación alternativo + vignette | Usuarios con cybersickness, vértigo, adultos mayores | XRI TeleportationArea + Vignette en URP |
| 3 | Solo paleta azul-violeta sin alternativa | Símbolos adicionales + palette alternativa | Usuarios con daltonismo (~300M hombres) | Filtros de color + iconos de forma en objetos clave |
| 4 | Sin modo gaze-only / voz | Dwell time + comandos de voz "Ir a Marte" | Usuarios con movilidad reducida | SeleccionPorMirada.cs + Unity Speech Recognition |
| 5 | Texto informativo pequeño, fondo transparente | Backing panel semiopaco + tamaño ajustable | Usuarios con baja visión | Panel oscuro detrás del texto + slider de tamaño |

**Menú de accesibilidad propuesto:**
```
Configuración de Accesibilidad
├── Visual
│   ├── Alto contraste: [ON/OFF]
│   ├── Tamaño de texto: [Pequeño / Normal / Grande / Muy Grande]
│   ├── Paleta de daltonismo: [Normal / Protanopia / Deuteranopia / Tritanopia]
│   └── Reducir transparencias: [ON/OFF]
├── Auditiva
│   ├── Subtítulos: [ON/OFF]
│   ├── Idioma subtítulos: [Español / Quechua / Aymara]
│   └── Tamaño de subtítulos: [Normal / Grande]
├── Movilidad
│   ├── Modo de locomoción: [Libre / Teleportación / Menú de destino]
│   ├── Velocidad de movimiento: [slider 1-10]
│   ├── Control por mirada: [ON/OFF] + tiempo dwell [slider]
│   └── Modo de un solo brazo: [ON/OFF]
└── Cognitiva / Confort
    ├── Velocidad de narración: [Lenta / Normal / Rápida]
    ├── Reducir movimiento: [ON/OFF]
    ├── Aviso de descanso cada: [10 / 20 / 30 minutos]
    └── Tutorial paso a paso: [ON/OFF]
```

---

### b) EJERCICIO INDIVIDUAL (15 min)

**Tarea:** realizar una **auditoría express de accesibilidad** de su propio proyecto grupal.

Abrir el proyecto en Unity e inspeccionar visualmente cada elemento usando esta rúbrica rápida:

```markdown
AUDITORÍA EXPRESS DE ACCESIBILIDAD — PROYECTO [NOMBRE]
Fecha: _______________________

VISUAL
☐/☑ Todos los colores tienen alternativa (forma, texto, patrón)
☐/☑ Hay un panel opaco detrás de todo texto en AR
☐/☑ El tamaño del texto es mínimo 16sp equivalente (≈ legible a 2m en VR)
☐/☑ Los flashes/parpadeos son < 3 por segundo
Problemas encontrados: _________________________________

AUDITIVO
☐/☑ Toda información de audio tiene equivalente visual
☐/☑ Los efectos de sonido tienen alternativa visual (ícono, vibración)
☐/☑ La narración o voz tiene subtítulos disponibles
Problemas encontrados: _________________________________

MOVILIDAD
☐/☑ Existe alternativa si el usuario no puede usar ambas manos
☐/☑ No hay tiempo límite que no se pueda extender
☐/☑ El menú es accesible sin movimiento brusco de cabeza
Problemas encontrados: _________________________________

COGNITIVO
☐/☑ Las instrucciones son cortas (máx. 10 palabras por instrucción)
☐/☑ Hay botón de pausa siempre accesible
☐/☑ El progreso es visible en todo momento
Problemas encontrados: _________________________________

CYBERSICKNESS
☐/☑ Si hay locomoción artificial: existe modo teleportación alternativo
☐/☑ Velocidad de movimiento es ajustable por el usuario
☐/☑ No hay aceleraciones o desaceleraciones bruscas
Problemas encontrados: _________________________________

PUNTUACIÓN: _____ / 15 criterios cumplidos

TOP 3 mejoras de accesibilidad para implementar esta semana:
1. ____________________________________________
2. ____________________________________________
3. ____________________________________________
```

**Criterio de éxito:** el estudiante puede nombrar al menos 3 problemas concretos de accesibilidad en su proyecto y proponer una solución técnica específica para cada uno.

---

## 5. CIERRE (10 min) {#cierre}

### a) SÍNTESIS COLABORATIVA (4 min)

**Pregunta 1:**
> "¿Cuál es la diferencia entre el modelo médico y el modelo social de la discapacidad, y por qué importa esa diferencia para el diseño XR?"

**Respuesta esperada:**
El modelo médico coloca la "discapacidad" en el cuerpo de la persona (el problema es el cuerpo que no funciona "normalmente"). El modelo social coloca la discapacidad en las barreras del entorno (el problema es que el entorno fue diseñado sin considerar la diversidad humana). Para el diseño XR: con el modelo médico, si alguien no puede usar mi app, es "su problema". Con el modelo social, si alguien no puede usar mi app, es "mi error de diseño". Esto cambia completamente la responsabilidad y la acción requerida.

**Pregunta 2:**
> "¿Por qué el cybersickness es una barrera de accesibilidad y no solo un problema de confort?"

**Respuesta esperada:**
Una "barrera de accesibilidad" es cualquier obstáculo que impide a una persona usar un sistema. El cybersickness excluye a: personas con vértigo crónico, personas con migrañas vestibulares, adultos mayores con mayor sensibilidad vestibular, mujeres (estadísticamente más susceptibles), y literalmente cualquier persona que no puede tolerar la locomoción artificial. Si el sistema de navegación de la app causa náuseas a una persona y la persona tiene que parar a los 5 minutos, esa app no es accesible para ella — sin importar cuántas otras características de accesibilidad tenga. Por eso el cybersickness debe tratarse con el mismo seriedad que el daltonismo o la sordez en el diseño XR.

**Pregunta 3:**
> "Nombren 3 técnicas de accesibilidad XR que también mejoran la experiencia de usuarios sin discapacidad."

**Respuesta esperada (efecto bordillo):**
1. Subtítulos: los usan personas sordas Y personas en ambientes ruidosos Y personas que aprenden el idioma Y personas que simplemente prefieren leer. Netflix reporta que el 85% de los usuarios que activan subtítulos no son sordos. 2. Teleportación en lugar de locomoción: evita cybersickness para todos los primeros usuarios de VR, para personas sensibles al movimiento, y resulta más precisa y cómoda en muchos contextos. 3. Opciones de velocidad reducida: beneficia a usuarios con cognición lenta, a adultos mayores, Y a cualquier usuario que quiere explorar tranquilamente en lugar de correr.

---

### b) METACOGNICIÓN (3 min)

> "En silencio, piensen: ¿habían pensado antes en la accesibilidad cuando diseñaban sus proyectos? Si no lo habían hecho, ¿qué cambiaría si comenzaran a hacerlo desde la primera decisión de diseño en lugar de al final? ¿Qué usuario específico real han estado excluyendo sin saberlo?"

---

### c) TAREA / PUENTE (3 min)

**Tarea concreta:**

1. Implementar en el proyecto grupal al menos 2 de los 3 ajustes identificados en la auditoría individual
2. Subir a GitHub un archivo `ACCESIBILIDAD.md` con:
   - Auditoría completa del proyecto
   - Ajustes implementados (con capturas de antes/después)
   - Justificación de cada decisión de diseño

**Conexión con Semana 14:**
> "La semana 14 es la presentación intermedia del proyecto. Los criterios de evaluación incluyen accesibilidad — el tribunal va a preguntar explícitamente qué personas con discapacidad pueden usar su app y cómo. Si no tienen respuesta, van a perder puntos. La tarea de esta semana es la preparación directa para esa presentación."

---

## GUION VERBAL SUGERIDO {#guion}

**Al presentar el modelo social:**
> "El modelo médico dice: 'esa persona está rota'. El modelo social dice: 'ese diseño está roto'. Son exactamente opuestos. Y la diferencia no es filosófica — es práctica. Si yo creo que el problema es la persona, no voy a cambiar mi app. Si yo creo que el problema es mi diseño, voy a mejorarlo. El modelo social los hace mejores diseñadores."

**Al mostrar el código de subtítulos:**
> "Este código de 50 líneas puede incluir a 466 millones de personas sordas e hipoacúsicas en el mundo. No es un código heroico — es un código responsable. Y si alguna vez trabajan para una empresa que lanza apps en Europa, este código no es opcional: es legal."

**Al cerrar:**
> "La próxima vez que diseñen un sistema XR, el primer usuario que imaginen no debería ser un hombre de 25 años sin discapacidad con experiencia en tecnología. Ese es el usuario más fácil de satisfacer. El verdadero reto — y el verdadero diferenciador profesional — es diseñar para quien tiene más barreras. Si lo hacen bien para ellos, lo hacen bien para todos."

---

## CASOS REALES RECOMENDADOS {#casos}

1. **Microsoft HoloLens + ALS Association (2021):** Pacientes con ELA (esclerosis lateral amiotrófica) que pierden control motor usan HoloLens con control por mirada para comunicarse y operar dispositivos del hogar. El sistema de dwell-time es la interface principal.

2. **Oxford VR — tratamiento de fobia social (2022):** app de VR usada en el NHS (sistema de salud UK) para tratar fobia social severa. Incluye modo de sesión gradual, control de velocidad de exposición, y opción de "tiempo fuera" instantáneo. Publicado en Lancet Psychiatry.

3. **Floreo Technologies — autismo y VR (2023):** app de entrenamiento social para personas con autismo. Cada elemento sensorial es ajustable individualmente. Modo "calma" reduce todos los estímulos a un entorno minimalista. Aprobada como software médico en EEUU.

4. **Apple Vision Pro Accessibility (2024):** primer headset con VoiceOver en 3D (lector de pantalla espacial), Zoom (amplificación de objetos 3D), reducción de transparencias, y "reducción de movimiento" que elimina animaciones que causan cybersickness.

5. **AbleGamers + Meta (2023):** la organización AbleGamers colaboró con Meta para crear guías de accesibilidad para desarrolladores del Quest Store. Las guías incluyen checklist técnico específico y patrones de código recomendados.

---

## EVALUACIÓN FORMATIVA {#eval}

| Momento | Señal de comprensión | Señal de dificultad |
|---------|---------------------|---------------------|
| Rompe-hielo | Conecta la experiencia corporal con el diseño | Solo describe el ejercicio sin reflexión |
| Diagnóstico | Sabe que el 16% de la población tiene discapacidad | No conoce dato, confunde modelos |
| Transformación 3.2 | Explica el modelo social con ejemplo XR propio | Confunde modelos médico y social |
| Transformación 3.3 | Nombra solución para daltonismo en AR (backing panel) | Solo dice "cambiar los colores" |
| Práctica grupal | Tabla con 5 barreras + soluciones técnicas específicas | Solo menciona barreras genéricas |
| Ejercicio individual | Auditoría con ≥3 problemas concretos y soluciones | Marca todo como "cumplido" sin verificar |
| Cierre | Explica efecto bordillo con ejemplo de su proyecto | No encuentra ningún beneficio para usuarios sin discapacidad |

---

## REFERENCIAS APA 7 {#referencias}

Organización Mundial de la Salud. (2023). *World report on disability*. https://www.who.int/teams/noncommunicable-diseases/sensory-functions-disability-and-rehabilitation/world-report-on-disability

W3C. (2023). *XR Accessibility User Requirements (XAUR)*. https://www.w3.org/TR/xaur/

W3C. (2023). *Web Content Accessibility Guidelines (WCAG) 2.1*. https://www.w3.org/TR/WCAG21/

Microsoft. (2024). *Mixed Reality Toolkit 3 Accessibility documentation*. https://learn.microsoft.com/en-us/windows/mixed-reality/mrtk-unity/mrtk3-overview/accessibility/accessibility-overview

Unity Technologies. (2024). *Unity Accessibility package documentation*. https://docs.unity3d.com/Packages/com.unity.accessibility@1.0/manual/index.html

Rheingold, H., & Lerner, A. (2022). *Inclusive design for immersive environments: A practical guide to XR accessibility*. O'Reilly Media.

Beeston, J., Power, C., Petrie, H., & Swallow, D. (2019). Approaches to accessibility in virtual reality. *Proceedings of the 16th Web for All Conference (W4A 2019)*. https://doi.org/10.1145/3315002.3317563

Almallah, M., Cruickshank, L., & Evans, M. (2021). Inclusive design for virtual reality: A systematic review. *Journal of Usability Studies, 16*(4), 189–212.

*PSISP08075 | Universidad Autónoma del Perú | Ingeniería de Sistemas | 2026-1*
