# S13 — LABORATORIO EN CLASE
## Curso: Realidad Virtual y Aumentada | PSISP08075
### Semana 13 — Auditoría Express de Accesibilidad XR

---

> **Laboratorio en clase — autónomo y autoexplicativo**
> **Tiempo:** 35–40 minutos
> **Modalidad:** Individual
> **Objetivo:** Realizar una auditoría de accesibilidad de tu proyecto XR e implementar 2 ajustes concretos
> **Entrega:** Archivo `ACCESIBILIDAD_EXPRESS.md` + commit antes de salir de clase

---

## ANTES DE EMPEZAR (2 min)

```
☐ Unity 2022.3.x abierto con tu proyecto AR/VR (cualquier lab anterior)
☐ Tu proyecto puede ejecutarse en Play sin errores críticos
☐ Tienes acceso a tu repositorio de GitHub para hacer commit al final
```

---

## PASO 1 — AUDITORÍA VISUAL RÁPIDA (8 min)

Haz clic en **▶ Play** y observa tu proyecto en funcionamiento. Sin tocar código, solo observar.

### 1.1 — Lista de verificación visual

Marca cada ítem: **✓ Cumple** / **✗ No cumple** / **? No sé**

```
ACCESIBILIDAD VISUAL
═══════════════════════════════════════════════════════════
[ ] Los objetos importantes tienen más de un indicador (no solo color)
    Ejemplo: si algo es peligroso, ¿hay también texto, ícono o forma?

[ ] El texto en pantalla tiene un fondo propio (no flotante sobre AR)
    Ejemplo: ¿hay un panel oscuro detrás del texto en tu Canvas?

[ ] El texto es lo suficientemente grande para leer a brazo extendido
    Referencia: mínimo 16 unidades de font size en Canvas (Screen Space)

[ ] No hay nada parpadeando más de 3 veces por segundo
    Cómo verificar: contar mentalmente los flashes durante 1 segundo

ACCESIBILIDAD AUDITIVA
═══════════════════════════════════════════════════════════
[ ] Si hay audio informativo (narración, alertas de sonido): hay equivalente visual
    Ejemplo: si un sonido indica "error" → ¿hay también texto o ícono de error?

[ ] Si no hay audio: no hay información perdida para usuarios sordos
    (Si no tienes audio en el proyecto: marcar como "Cumple")

ACCESIBILIDAD MOTRIZ
═══════════════════════════════════════════════════════════
[ ] Los botones del Canvas tienen tamaño razonable (mínimo 80×40 unidades)
    Cómo verificar: seleccionar el botón en Hierarchy → Inspector → Rect Transform → Width y Height

[ ] No hay timeout automático que cierre la app sin aviso al usuario
    Cómo verificar: buscar "Invoke" + "Quit" o "SceneManager.LoadScene" en tus scripts

ACCESIBILIDAD COGNITIVA
═══════════════════════════════════════════════════════════
[ ] Hay un botón o forma de "pausar" la experiencia
[ ] Las instrucciones en pantalla son cortas (máx. 10 palabras por frase)

CYBERSICKNESS (si tu proyecto tiene movimiento con joystick/WASD)
═══════════════════════════════════════════════════════════
[ ] Si hay locomoción artificial: la velocidad de movimiento es ajustable
[ ] Si hay locomoción artificial: existe modo teleportación o alternativa
    (Si no tienes locomoción: marcar "No aplica")
═══════════════════════════════════════════════════════════
```

**Después de Play → parar (▶).**

### 1.2 — Registrar resultados

Cuenta tus marcas:
```
Total "Cumple":     _____ / 12 criterios aplicables
Total "No cumple":  _____
Total "No sé":      _____

Los 3 problemas más graves que identifiqué:
1. ________________________________________________
2. ________________________________________________
3. ________________________________________________
```

---

## PASO 2 — IMPLEMENTAR AJUSTE #1: BACKING PANEL PARA TEXTO (12 min)

Este ajuste soluciona el problema más común en proyectos AR: texto ilegible sobre fondos variables.

### 2.1 — Verificar si ya tienes Canvas con texto

1. En la **Hierarchy**, busca un `Canvas` o elemento `Text/TextMeshPro`
2. Si no tienes texto en tu proyecto: crea un Canvas básico ahora:
   ```
   Hierarchy → clic derecho → UI → Canvas
   Luego: clic derecho en Canvas → UI → Text - TextMeshPro
   Texto del elemento: "Toca para colocar objeto"
   ```

### 2.2 — Agregar el Backing Panel

**Opción A: Canvas en Screen Space (más común en labs anteriores)**

1. En la **Hierarchy**, expande tu `Canvas`
2. Clic derecho en el `Canvas` → **UI → Image** — llámalo `PanelFondo`
3. En Inspector del `PanelFondo`:
   - **Color**: negro con alpha 70% → haz clic en Color → selecciona negro `(0, 0, 0)` → Alpha: **178** (equivale al 70%)
4. En la jerarquía UI, asegúrate de que `PanelFondo` aparezca **ANTES** que el texto (el texto debe estar "encima"):
   ```
   Canvas
   ├── PanelFondo    ← aquí (renderiza primero = aparece atrás)
   └── Texto         ← aquí (renderiza después = aparece encima)
   ```
5. Ajustar el tamaño del `PanelFondo` para que cubra el texto:
   - Rect Transform del PanelFondo: hacer que sea del mismo tamaño que el área de texto o ligeramente más grande

**Opción B: Canvas en World Space (para objetos AR en el mundo 3D)**

1. Selecciona el Canvas → en el Inspector → `Canvas` component → **Render Mode: World Space**
2. Agregar `Image` como hermano del texto → posicionar ligeramente detrás (Z del Image: 0.001 más que el texto)
3. Color negro semitransparente como en Opción A

### 2.3 — Cambiar el color del texto a blanco

1. Seleccionar el componente `TextMeshPro` (o `Text`)
2. Inspector → **Color** → seleccionar blanco `(255, 255, 255)` con Alpha 255

### 2.4 — Verificar el contraste

1. Presionar ▶ Play
2. Observar el texto sobre el fondo oscuro del panel
3. Preguntar: ¿se lee claramente sin importar qué fondo del mundo real haya detrás?

**Anotar:**
```
¿El texto era legible antes? (Sí / No / A veces)  : _______
¿El texto es legible ahora?                        : _______
¿El panel oscuro cubre todo el texto?              : _______
```

---

## PASO 3 — IMPLEMENTAR AJUSTE #2: BOTÓN ACCESIBLE CON FEEDBACK (12 min)

Este ajuste mejora la interacción táctil/VR para usuarios con movilidad reducida o precisión limitada.

### 3.1 — Crear el script AccesibilidadBoton.cs

En el panel **Project** → carpeta `Scripts` → clic derecho → **Create → C# Script** → nombre: `AccesibilidadBoton`

Abre el script y reemplaza todo el contenido con:

```csharp
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.EventSystems;
using TMPro;

/// <summary>
/// Mejora de accesibilidad para botones:
/// - Retroalimentación visual clara al hover y al presionar
/// - Retroalimentación háptica (vibración) al presionar
/// - Etiqueta accesible para lectores de pantalla
/// </summary>
[RequireComponent(typeof(Button))]
public class AccesibilidadBoton : MonoBehaviour, IPointerEnterHandler, IPointerExitHandler
{
    [Header("Colores de accesibilidad")]
    public Color colorNormal    = new Color(0.2f, 0.4f, 0.8f, 1f); // azul
    public Color colorHover     = new Color(0.3f, 0.6f, 1.0f, 1f); // azul claro
    public Color colorPresionado = new Color(0.1f, 0.2f, 0.5f, 1f); // azul oscuro

    [Header("Etiqueta accesible (para lector de pantalla)")]
    [Tooltip("Descripción del botón para usuarios con tecnología asistiva")]
    public string etiquetaAccesible = "Botón de acción principal";

    private Image imagenBoton;
    private Button boton;

    void Start()
    {
        boton       = GetComponent<Button>();
        imagenBoton = GetComponent<Image>();

        // Aplicar color inicial
        if (imagenBoton != null)
            imagenBoton.color = colorNormal;

        // Registrar acción al presionar para agregar feedback háptico
        boton.onClick.AddListener(AlPresionar);

        // Asegurar tamaño mínimo accesible (44×44 unidades Unity ≈ equivalente 44px)
        RectTransform rt = GetComponent<RectTransform>();
        if (rt.sizeDelta.x < 120f || rt.sizeDelta.y < 44f)
        {
            rt.sizeDelta = new Vector2(
                Mathf.Max(rt.sizeDelta.x, 120f),
                Mathf.Max(rt.sizeDelta.y, 44f)
            );
            Debug.Log($"[Accesibilidad] Botón '{gameObject.name}' redimensionado a tamaño mínimo accesible.");
        }
    }

    // Llamado cuando el cursor/gaze entra en el botón
    public void OnPointerEnter(PointerEventData eventData)
    {
        if (imagenBoton != null)
            imagenBoton.color = colorHover;
    }

    // Llamado cuando el cursor/gaze sale del botón
    public void OnPointerExit(PointerEventData eventData)
    {
        if (imagenBoton != null)
            imagenBoton.color = colorNormal;
    }

    void AlPresionar()
    {
        // Feedback visual de "presionado"
        if (imagenBoton != null)
            imagenBoton.color = colorPresionado;

        // Feedback háptico (funciona en dispositivos móviles Android)
        #if UNITY_ANDROID || UNITY_IOS
        Handheld.Vibrate();
        #endif

        // Volver al color hover después de 0.1 segundos
        Invoke(nameof(RestaurarColorHover), 0.1f);

        Debug.Log($"[Accesibilidad] Botón activado: {etiquetaAccesible}");
    }

    void RestaurarColorHover() => imagenBoton.color = colorHover;
}
```

### 3.2 — Agregar el script a un botón

1. En la **Hierarchy**, selecciona cualquier botón de tu proyecto
   - Si no tienes un botón: `Hierarchy → clic derecho → UI → Button - TextMeshPro`
2. En el **Inspector** del botón → `Add Component` → busca `AccesibilidadBoton` → seleccionarlo
3. Llenar el campo **Etiqueta Accesible** con la descripción del botón, ejemplo: `"Botón para colocar objeto AR en la escena"`

### 3.3 — Verificar el ajuste

1. ▶ Play
2. Pasar el cursor por encima del botón → debe cambiar a azul claro
3. Hacer clic → debe oscurecerse brevemente y mostrar log en Console
4. Abrir **Window → Analysis → Console**: verificar que aparece el mensaje `[Accesibilidad] Botón activado: ...`

```
¿El botón cambia de color al hover?          : Sí / No
¿El botón tiene feedback visual al click?    : Sí / No
¿Aparece el mensaje en Console?              : Sí / No
¿El tamaño del botón fue ajustado?           : Sí / No / Ya era accesible
```

---

## PASO 4 — CREAR REPORTE Y COMMIT (5 min)

### 4.1 — Crear el archivo de reporte

En la raíz del proyecto (misma carpeta que `Assets/`), crea un archivo llamado `ACCESIBILIDAD_EXPRESS.md`:

```markdown
# Reporte de Accesibilidad Express — Semana 13
**Nombre:** [Tu nombre completo]
**Código:** [Tu código de estudiante]
**Proyecto:** [Nombre del proyecto Unity auditado]
**Fecha:** [fecha de hoy]

## Auditoría Initial (12 criterios)

| Criterio | Estado | Observación |
|----------|--------|-------------|
| Objetos con indicador múltiple (no solo color) | ✓/✗/? | |
| Texto con backing panel | ✓/✗/? | |
| Texto tamaño legible | ✓/✗/? | |
| Sin parpadeo > 3Hz | ✓/✗/? | |
| Audio con equivalente visual | ✓/✗/? | |
| Sin información perdida para sordos | ✓/✗/? | |
| Botones tamaño mínimo | ✓/✗/? | |
| Sin timeout automático sin aviso | ✓/✗/? | |
| Botón de pausa | ✓/✗/? | |
| Instrucciones cortas | ✓/✗/? | |
| Velocidad de movimiento ajustable | ✓/✗/N/A | |
| Modo alternativo de locomoción | ✓/✗/N/A | |

**Total cumple:** ___ / ___ aplicables

## Ajustes Implementados

### Ajuste 1 — Backing Panel para texto
- **Problema antes:** [descripción]
- **Solución aplicada:** [descripción]
- **Resultado:** [descripción]

### Ajuste 2 — Botón accesible con feedback
- **Problema antes:** [descripción]
- **Solución aplicada:** AccesibilidadBoton.cs en [nombre del botón]
- **Resultado:** [descripción]

## Los 3 ajustes de accesibilidad más importantes para mi proyecto

1. [Ajuste 1 — ¿qué y por qué?]
2. [Ajuste 2 — ¿qué y por qué?]
3. [Ajuste 3 — ¿qué y por qué?]

## Reflexión
¿Qué tipo de usuario estabas excluyendo sin saberlo antes de esta auditoría?
[3-5 líneas]
```

### 4.2 — Commit

```bash
git add ACCESIBILIDAD_EXPRESS.md Assets/Scripts/AccesibilidadBoton.cs
git commit -m "feat(s13): auditoría de accesibilidad + backing panel + botón accesible"
git push
```

---

## CHECKLIST DE ENTREGA

```
☐ Auditoría de 12 criterios completada con observaciones
☐ Backing panel implementado y texto legible con fondo oscuro
☐ AccesibilidadBoton.cs creado y aplicado a al menos 1 botón
☐ Feedback visual (hover + click) verificado en Play
☐ ACCESIBILIDAD_EXPRESS.md con todas las secciones completadas
☐ Commit y push realizados (verificar en GitHub que aparece)
```

---

## SOLUCIÓN DE PROBLEMAS RÁPIDA

| Síntoma | Causa | Solución |
|---------|-------|----------|
| PanelFondo tapa el texto (texto invisible) | El Panel está "encima" del texto en la jerarquía | En Hierarchy: arrastrar el PanelFondo para que esté ANTES del texto |
| AccesibilidadBoton no aparece en Add Component | Error de compilación en el script | Revisar Console: si hay error rojo, leerlo y corregirlo |
| El botón no cambia de color | El botón no tiene componente `Image` | Seleccionar el botón → Add Component → Image → luego volver a verificar |
| Handheld.Vibrate() da error | Plataforma de compilación no es Android/iOS | El #if UNITY_ANDROID protege esa línea — si da error, revisar los #if |
| El mensaje de commit falla | No hay cambios staged | `git status` para verificar qué archivos nuevos hay, luego `git add .` |

---

## ROL DEL DOCENTE

**Mientras circula, verificar:**
- ¿El estudiante realmente llenó la auditoría o la completó sin verificar?
- ¿El PanelFondo está en el orden correcto de la jerarquía UI?
- ¿El script AccesibilidadBoton.cs compiló sin errores?

**Preguntas de andamiaje:**
- "¿El texto se puede leer sobre un fondo blanco? ¿Sobre un fondo muy oscuro? Si la respuesta varía, necesitas el panel."
- "¿Cuál fue el problema de accesibilidad que más te sorprendió encontrar en tu propio proyecto?"
- "Nombra un usuario real que no podría usar tu proyecto tal como está ahora."

**Cierre del lab (3 min):**
> "Levanten la mano si encontraron al menos 3 criterios 'No cumple'. ¿Alguien encontró 5 o más? No es un fracaso — es el punto del ejercicio. El 99% de los proyectos XR tienen problemas de accesibilidad porque se diseñan pensando en el usuario 'promedio'. La habilidad de hacer esta auditoría y saber qué hacer al respecto es exactamente lo que diferencia a un desarrollador XR inclusivo de uno que solo cumple el mínimo."

---

*PSISP08075 | Universidad Autónoma del Perú | Ingeniería de Sistemas | Semana 13 | 2026-1*
