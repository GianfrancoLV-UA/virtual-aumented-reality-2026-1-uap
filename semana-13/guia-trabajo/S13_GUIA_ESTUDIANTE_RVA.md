# S13 — GUÍA DE TRABAJO DEL ESTUDIANTE
## Curso: Realidad Virtual y Aumentada | PSISP08075
### Semana 13 — Accesibilidad en RA y RV

---

> **Instrucciones generales**
> - Esta guía tiene 4 secciones (A, B, C, D) de complejidad creciente.
> - No hay respuestas en este documento — las encontrarás por tu propio análisis.
> - En la sección A y B: solo una respuesta es correcta.
> - En la sección C y D: se valora la profundidad del análisis y la creatividad.
> - Tiempo estimado: 90–120 minutos.

---

## SECCIÓN A — OPCIÓN MÚLTIPLE (25 puntos, 2.5 pts c/u)

**Instrucción:** Marca con una X la única respuesta correcta para cada pregunta.

---

**A1.** Según el modelo social de la discapacidad, cuando un usuario en silla de ruedas no puede usar una app de VR que requiere ponerse de pie para alcanzar objetos, el problema principal es:

- [ ] a) La condición médica del usuario que le impide ponerse de pie
- [ ] b) El diseño de la app que no consideró usuarios con movilidad reducida
- [ ] c) La tecnología VR que todavía no está madura para casos especiales
- [ ] d) El usuario, quien debería usar una versión diferente de la app para discapacitados

---

**A2.** ¿Cuál es el ratio de contraste mínimo que exige WCAG 2.1 nivel AA para texto normal sobre fondo?

- [ ] a) 2:1
- [ ] b) 3:1
- [ ] c) 4.5:1
- [ ] d) 7:1

---

**A3.** Un usuario con **daltonismo rojo-verde (deuteranopia)** usa tu app AR de medicina donde el color rojo indica tejido dañado y verde indica tejido sano. ¿Cuál es la solución de accesibilidad más completa?

- [ ] a) Eliminar todos los colores rojo y verde de la app y usar solo escala de grises
- [ ] b) Agregar un modo especial "para daltónicos" con colores diferentes
- [ ] c) Mantener los colores pero añadir forma, icono de advertencia y texto overlay como canales adicionales de información
- [ ] d) Informar al usuario que la app no es compatible con daltonismo en los términos de servicio

---

**A4.** La técnica "Dwell Time" en VR/AR permite:

- [ ] a) Ajustar el tiempo de renderizado de frames para mejorar rendimiento
- [ ] b) Seleccionar objetos simplemente mirándolos durante un tiempo configurado, sin usar las manos
- [ ] c) Medir cuánto tiempo el usuario pasa dentro de una sesión VR
- [ ] d) Controlar la velocidad de locomoción para reducir cybersickness

---

**A5.** ¿Por qué el texto AR sobre fondo transparente es particularmente problemático para personas con baja visión?

- [ ] a) Porque el rendering de texto transparente consume más GPU
- [ ] b) Porque el texto flotante parece falso y rompe la ilusión de realidad
- [ ] c) Porque el fondo del mundo real es variable e impredecible, haciendo imposible garantizar contraste suficiente
- [ ] d) Porque el texto AR requiere un shader especial incompatible con la mayoría de dispositivos

---

**A6.** El **cybersickness** se produce principalmente por:

- [ ] a) La calidad baja de los gráficos en entornos VR económicos
- [ ] b) Una discordancia entre la información visual (movimiento en VR) y la información vestibular (el cuerpo no se mueve)
- [ ] c) La duración excesiva de la sesión VR sin descanso
- [ ] d) El peso del headset que causa fatiga en el cuello

---

**A7.** ¿Qué es el documento **XAUR** (XR Accessibility User Requirements)?

- [ ] a) Un SDK de Unity para implementar accesibilidad en proyectos XR
- [ ] b) La extensión de WCAG publicada por el W3C para definir requisitos de accesibilidad específicos para XR
- [ ] c) El estándar legal obligatorio de accesibilidad XR en la Unión Europea
- [ ] d) Una herramienta de diagnóstico de accesibilidad para headsets Meta Quest

---

**A8.** En el script `SubtitulosXR.cs` visto en clase, el método se coloca en `LateUpdate()` en lugar de `Update()` porque:

- [ ] a) `LateUpdate()` es más eficiente en términos de memoria para cálculos de UI
- [ ] b) `LateUpdate()` se ejecuta después de que la cámara se ha movido, garantizando que los subtítulos se posicionen correctamente respecto a la posición final de la cámara en ese frame
- [ ] c) `LateUpdate()` es el único ciclo de vida que permite modificar transformaciones en VR
- [ ] d) `Update()` no puede acceder a la posición de la cámara, solo `LateUpdate()` puede

---

**A9.** El "efecto bordillo" (curb cut effect) en diseño accesible se refiere a:

- [ ] a) La necesidad de añadir rampas en todas las entradas de edificios
- [ ] b) El principio de que las soluciones diseñadas para personas con discapacidad terminan beneficiando a todos los usuarios
- [ ] c) La técnica de diseño que coloca todos los elementos de UI cerca del borde inferior de la pantalla
- [ ] d) El problema de la fatiga de brazo cuando los menús están muy separados en VR

---

**A10.** ¿Cuál es la diferencia clave entre **locomoción libre** y **teleportación** en VR desde el punto de vista de la accesibilidad?

- [ ] a) La teleportación es más difícil de implementar y solo se usa en apps avanzadas
- [ ] b) La locomoción libre permite moverse más rápido y es preferida por usuarios profesionales
- [ ] c) La locomoción libre con joystick puede causar cybersickness ya que el cuerpo no se mueve físicamente, mientras la teleportación elimina esa discordancia
- [ ] d) No hay diferencia significativa en accesibilidad, solo en la sensación de inmersión

---

## SECCIÓN B — COMPLETAR Y RELACIONAR (22 puntos)

### B1 — Completar espacios en blanco (12 puntos, 2 pts c/u)

Completa correctamente cada espacio:

1. WCAG son las siglas de **______________________________** y sus cuatro principios (POUR) son: Perceptible, **______________________________**, Comprensible y Robusto.

2. El componente de Unity que permite asignar una etiqueta accesible y descripción a cualquier GameObject para que el lector de pantalla del sistema operativo los pueda leer se llama **______________________________**.

3. El **______________________________** es el conjunto de síntomas de náusea, desorientación y malestar causado por la discordancia entre la información visual del entorno VR y las señales del sistema vestibular.

4. Para que el texto en AR sea legible independientemente del fondo del mundo real, se debe añadir un **______________________________** semiopaco detrás del texto.

5. Según WCAG 2.1, las imágenes o elementos que contienen información no deben usar **______________________________** como único medio de transmitir esa información — deben incluir también forma, patrón o texto.

6. La organización que publicó el documento XAUR (XR Accessibility User Requirements) es el **______________________________**.

---

### B2 — Relacionar columnas (10 puntos, 1 pt c/u)

Conecta cada barrera de accesibilidad (columna izquierda) con su solución más apropiada en XR (columna derecha):

| # | Barrera de accesibilidad | Letra | Solución en XR |
|---|--------------------------|-------|----------------|
| 1 | Usuario sordo no puede escuchar narración de audio en VR | | A. Backing panel semiopaco + texto outline |
| 2 | Usuario con daltonismo no distingue zonas de peligro codificadas en rojo | | B. Dwell time (selección por mirada con tiempo configurable) |
| 3 | Texto AR ilegible sobre fondos claros del mundo real | | C. Subtítulos 3D anclados a la cámara (head-locked) |
| 4 | Usuario con Parkinson no puede presionar botones pequeños del controller | | D. Iconos de forma + texto "PELIGRO" redundante al color |
| 5 | Primera vez en VR — usuario adulto mayor siente náuseas con joystick | | E. Modo teleportación + vignette dinámico + velocidad ajustable |
| 6 | Usuario con autismo siente sobrecarga sensorial con muchos estímulos | | F. Botones más grandes + zona de toque ampliada + modo hold |
| 7 | Usuario en silla de ruedas no puede alcanzar objetos colocados muy arriba en VR | | G. Modo calma: reducir objetos, sonidos y velocidad |
| 8 | App sin modo pausa: usuario con epilepsia expuesto a flashes continuos | | H. Reposicionar UI dentro del rango de movimiento sentado |
| 9 | App de entrenamiento VR usa solo audio para dar feedback de errores | | I. Semáforos, iconos y vibración como canales adicionales |
| 10 | Usuario ciego quiere explorar objetos 3D en un museo VR | | J. Máximo flash rate configurado + botón de pausa siempre visible |
| | | | K. Audio descriptivo espacial + hápticos de confirmación |

---

## SECCIÓN C — ANÁLISIS Y DIAGNÓSTICO (28 puntos)

### C1 — Diagnóstico de código con problemas de accesibilidad (12 puntos)

El siguiente script de Unity fue escrito sin considerar accesibilidad. Identifica **al menos 4 problemas concretos de accesibilidad** y para cada uno propón la solución correcta.

```csharp
using UnityEngine;
using UnityEngine.UI;

public class MenuPrincipalVR : MonoBehaviour
{
    public Button botonIniciar;
    public Button botonOpciones;
    public Button botonSalir;
    public Image imagenEstado;  // Rojo = error, Verde = OK
    public AudioSource alarma;  // Sonido de alerta de error

    void Start()
    {
        // Colores de estado
        imagenEstado.color = Color.green;

        // Tamaño fijo de botones
        botonIniciar.GetComponent<RectTransform>().sizeDelta = new Vector2(80, 25);
        botonOpciones.GetComponent<RectTransform>().sizeDelta = new Vector2(80, 25);
        botonSalir.GetComponent<RectTransform>().sizeDelta = new Vector2(80, 25);

        // Timeout automático sin aviso
        Invoke("CerrarSesion", 60f);
    }

    void Update()
    {
        // Animación de parpadeo del estado
        float velocidadParpadeo = 8f;  // 8 ciclos por segundo
        float alpha = Mathf.Abs(Mathf.Sin(Time.time * velocidadParpadeo * Mathf.PI));
        imagenEstado.color = new Color(imagenEstado.color.r,
                                        imagenEstado.color.g,
                                        imagenEstado.color.b, alpha);
    }

    public void MostrarError()
    {
        imagenEstado.color = Color.red;
        alarma.Play();
        // No hay feedback de texto — solo color y sonido
    }

    void CerrarSesion()
    {
        Application.Quit();
    }
}
```

Para cada problema, usa esta tabla:

| # | Línea(s) | Problema de accesibilidad | Tipo de discapacidad afectada | Solución correcta |
|---|----------|--------------------------|-------------------------------|-------------------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

---

### C2 — Comparación: Audio Narration vs Spatial Audio Descriptions (8 puntos)

Explica la diferencia entre estos dos enfoques para hacer una app VR accesible a usuarios ciegos:

**Enfoque A:** La app tiene una narración lineal de audio que describe todo el contenido de la escena al inicio de cada nivel — el usuario escucha una descripción completa en 2 minutos y luego navega libremente.

**Enfoque B:** La app usa "audio descriptions espaciales" — cuando el usuario gira la cabeza o se aproxima a un objeto, el sistema dice en voz alta el nombre, función y estado de ese objeto específico.

Responde:
1. ¿Cuál enfoque representa mejor el modelo social de la discapacidad? Justifica.
2. ¿Qué limitaciones tiene el Enfoque A que el Enfoque B no tiene?
3. ¿En qué tipo de app VR el Enfoque A sería más apropiado que el B?
4. ¿Cómo implementarías el Enfoque B en Unity a nivel técnico (qué componente y evento usarías)?

---

### C3 — Caso: App de rehabilitación física en VR (8 puntos)

Una empresa de Lima está desarrollando una app de **rehabilitación física en VR** para pacientes post-operados en hospitales peruanos. La app pide a los pacientes hacer movimientos específicos de brazos para recuperar rango de movimiento (cirugía de hombro, codo, muñeca). El headset es un Meta Quest 3.

El equipo identificó estos usuarios objetivo:
- Paciente A: mujer de 65 años, primera vez con VR, operada del hombro derecho
- Paciente B: hombre de 45 años, usa VR ocasionalmente, con parálisis parcial de mano derecha por accidente
- Paciente C: joven de 22 años, experiencia en videojuegos, sordo desde nacimiento
- Paciente D: hombre de 55 años, con daltonismo rojo-verde, operado de ambos codos

Para cada paciente:
1. Identifica las 2 principales barreras de accesibilidad que encontraría en una app diseñada sin accesibilidad
2. Propón 1 solución concreta de diseño XR para cada barrera

**Formato de respuesta:**

| Paciente | Barrera 1 | Solución 1 | Barrera 2 | Solución 2 |
|----------|-----------|-----------|-----------|-----------|
| A (65 años, cirugía hombro) | | | | |
| B (parálisis mano derecha) | | | | |
| C (sordo, 22 años) | | | | |
| D (daltonismo, codos) | | | | |

---

## SECCIÓN D — CASO AVANZADO (25 puntos)

### Caso: Sistema XR de Educación Inclusiva para Zonas Rurales del Perú

El **Programa Nacional de Innovación Educativa** contrata a tu equipo para desarrollar un sistema XR educativo para colegios de zonas rurales de Ayacucho y Huancavelica. Las características del contexto:

- Estudiantes de 12-17 años con diversidad de capacidades
- Algunos colegios tienen estudiantes con discapacidad visual, auditiva o cognitiva
- Conectividad limitada (solo WiFi, sin 4G estable)
- Presupuesto limitado → headsets económicos (no Meta Quest Pro — sino Quest Go o cardboard con Android)
- El contenido educativo es ciencias naturales: ciclo del agua, fotosíntesis, ecosistemas
- El sistema debe ser usado por profesores sin formación técnica avanzada

**Parte 1 — Análisis de requerimientos de accesibilidad (8 puntos)**

Diseña un análisis de los requisitos de accesibilidad para este sistema. Incluye:
- ¿Qué tipos de discapacidad debes considerar? ¿Por qué?
- ¿Qué restricciones del contexto (rural, económico, sin expertos técnicos) afectan las soluciones de accesibilidad disponibles?
- ¿Qué contenidos del currículum (ciclo del agua, fotosíntesis) plantean desafíos específicos de accesibilidad?

**Parte 2 — Propuesta de diseño inclusivo (10 puntos)**

Diseña un sistema XR accesible para este contexto. Tu diseño debe incluir:
- Mínimo 5 características de accesibilidad concretas (no genéricas: "agregar subtítulos" → especifica cómo, en qué idiomas, en qué formato)
- Cómo el sistema se adapta a diferentes niveles de capacidad sin necesitar configuración técnica compleja
- Una característica creativa que no existe en las apps XR actuales y que sería especialmente útil para este contexto peruano específico

**Parte 3 — Validación (7 puntos)**

Diseña un plan de validación de accesibilidad para el sistema. Responde:
- ¿Cómo probarías la accesibilidad del sistema antes del lanzamiento?
- ¿Qué personas específicas incluirías en el proceso de prueba?
- ¿Qué métricas usarías para determinar si el sistema es "accesible"?
- ¿Cómo incorporarías feedback de personas con discapacidad al proceso de diseño (no solo de prueba)?

---

## CRITERIOS DE EVALUACIÓN

| Sección | Puntos | Criterio |
|---------|--------|---------|
| A — Opción Múltiple | 25 pts | Respuesta correcta única por pregunta |
| B1 — Espacios en blanco | 12 pts | Término técnico exacto en cada espacio |
| B2 — Relacionar columnas | 10 pts | Correspondencia correcta |
| C1 — Diagnóstico de código | 12 pts | 4 problemas identificados con solución correcta |
| C2 — Comparación enfoques | 8 pts | Análisis profundo de diferencias y casos |
| C3 — Caso rehabilitación | 8 pts | Barreras y soluciones específicas por perfil |
| D — Caso avanzado | 25 pts | Análisis contextualizado, creatividad, validación |
| **TOTAL** | **100 pts** | |

---

*PSISP08075 | Universidad Autónoma del Perú | Ingeniería de Sistemas | Semana 13 | 2026-1*
