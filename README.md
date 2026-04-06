# 📘 Test de Completamiento Semántico – Adaptación Rioplatense

## Basado en el test “Pirámides y Faraones” (Howard & Patterson, 1992)

---

## 🧠 ¿Qué mide este test?

Evalúa la **velocidad de procesamiento semántico** y la **capacidad de asociación conceptual** en pacientes con daño cerebral adquirido (ACV) o enfermedades neurodegenerativas. El paciente debe elegir, entre dos opciones, la imagen/palabra que completa lógicamente una oración o una asociación semántica con un estímulo visual.

### Fundamento clínico – Gold Standard

El test original **“Pyramids and Palm Trees”** (Howard & Patterson, 1992) es considerado el **gold standard** para la evaluación de la **memoria semántica** en pacientes con afasia, demencia semántica y lesiones temporales izquierdas. Ha sido validado en múltiples idiomas y poblaciones.

Nuestra versión adapta los ítems al **español rioplatense** (Argentina/Uruguay) y reemplaza los estímulos originales (pirámides, palmeras) por objetos de la vida cotidiana local (pila, linterna, ancla, barco, etc.), manteniendo la misma estructura lógica de asociación semántica cruzada (estímulo → correcto / distractor).

---

## 👥 Población objetivo

- Pacientes con **ACV en hemisferio izquierdo** (afasia, déficit semántico).
- Pacientes con **ACV en hemisferio derecho** (neglect semántico – aunque el test es principalmente verbal).
- Personas con **demencia semántica**, **afasia progresiva primaria** variante semántica.
- **Sujetos controles** (para obtener datos normativos).

El diseño es accesible para personas con **hemiparesia** (uso de una sola mano, botones grandes, sin doble clic) y **trastornos visuales** (alto contraste, imágenes grandes, fuente grande).

---

## ♿ Accesibilidad y adaptación para pacientes con ACV

El software ha sido diseñado siguiendo las **pautas de accesibilidad de Material Design** y recomendaciones para pacientes neurológicos:

| Característica | Implementación |
|----------------|----------------|
| **Botones grandes** | Tamaño de imagen: 300×300 píxeles. Botones de respuesta: 300×360 (imagen+texto) o 300×300 (solo imagen). |
| **Alto contraste** | Fondo #F5F5F5 (gris muy claro), botones blancos con borde negro, texto negro sobre fondo blanco o gris claro. |
| **Sin doble clic** | La respuesta se registra al primer clic. |
| **Navegación por teclado** | Flechas izquierda/derecha para responder. Tecla Escape para salir. |
| **Ventana maximizable** | El test se abre en pantalla completa o maximizada (compatible con Windows, Linux y macOS). |
| **Placeholders** | Si falta una imagen, se muestra un recuadro gris con el nombre de la palabra en fuente grande (28 px). |
| **Tiempo de reacción** | Se registra automáticamente desde que se muestra el ítem hasta la respuesta. |
| **Feedback visual** | No hay sonidos (evita estrés), solo cambios visuales. |

### Adaptación cultural rioplatense

Los 20 ítems fueron modificados para reflejar el vocabulario y las costumbres de Argentina y Uruguay:

- Se reemplazaron términos como *"palm tree"* por *"palmera"* y *"pharaoh"* por *"faraón"*, pero contextualizados en oraciones familiares.
- Ejemplos de oraciones adaptadas:  
  *"Necesito una pila porque mi **linterna** no enciende."*  
  *"El capitán usó el ancla para detener el **barco**."*  
  *"El indio levantó su **carpa** en el campamento."*

Todos los estímulos visuales son objetos reconocibles localmente.

---

## 🎮 Modos de uso del sistema

El usuario puede seleccionar dos ejes de dificultad antes de comenzar:

### 1. Modo oración
- **Con oración (fácil):** Se presenta una oración con un espacio en blanco. El paciente debe elegir la palabra que completa lógicamente la frase.
- **Sin oración (difícil):** Solo se muestra la imagen de estímulo. El paciente debe asociarla conceptualmente con una de las dos opciones.

### 2. Modo visual
- **Imagen + Texto (fácil):** Cada opción se muestra como imagen y texto.
- **Solo imagen (medio):** Cada opción es solo una imagen.
- **Solo texto (difícil):** Cada opción es solo texto.

Combinando ambos modos se obtienen **6 niveles de dificultad** progresiva, lo que permite ajustar el test al grado de deterioro del paciente.

---

## 📊 ¿Qué métricas se obtienen?

Por cada ítem se registra:

- `acierto` (True/False)
- `tiempo_ms` (milisegundos desde que aparece el ítem hasta la respuesta)

Al finalizar el test, se calcula:

- **Total de aciertos** (máximo 20)
- **Precisión** (aciertos/20)
- **Tiempo promedio, mediana, desviación estándar, mínimo y máximo**
- **Puntuación Z** comparada con controles sanos (media = 19.95, DE = 0.22) – obtenida de la literatura.
- **Diagnóstico sugerido**:  
  - *Déficit semántico probable* si aciertos < 17 (punto de corte con sensibilidad 85% y especificidad 98.8%).
  - *Dentro de lo normal* si aciertos ≥ 17.

Además se genera un **histograma de tiempos de reacción** y se muestra la **curva ROC** del test con AUC 0.95.

---

## 📁 Formato de salida (JSON y TXT)

Al finalizar el test, se crea automáticamente la carpeta `/results` (si no existe) y dentro se guardan dos archivos con el nombre:

`{id_paciente}_{fecha_hora}.json` y `{id_paciente}_{fecha_hora}.txt`

### Estructura del JSON

```json
{
  "id_paciente": "PAC001",
  "edad": 65,
  "genero": "Masculino",
  "fecha": "2026-04-06T10:30:00",
  "modo_oracion": "con_oracion",
  "modo_visual": "imagen_texto",
  "test": "Completamiento Semántico (Pirámides y Faraones - adaptación rioplatense)",
  "total_items": 20,
  "aciertos": 18,
  "precision": 0.9,
  "tiempo_respuesta_promedio_ms": 1250.5,
  "tiempo_respuesta_desviacion_ms": 320.2,
  "tiempo_respuesta_mediana_ms": 1180.0,
  "tiempo_respuesta_min_ms": 850.0,
  "tiempo_respuesta_max_ms": 2100.0,
  "tiempos_individuales_ms": [1250, 1180, ...],
  "z_aciertos_control": -8.86,
  "por_debajo_punto_corte_17": false,
  "diagnostico_sugerido": "Dentro de lo normal",
  "detalle_respuestas": [
    {
      "item_num": 1,
      "estimulo": "pila",
      "correcta": "linterna",
      "distractor": "lampara",
      "oracion_usada": "Necesito una pila porque mi ______ no enciende.",
      "respuesta_usuario": "linterna",
      "acierto": true,
      "tiempo_ms": 1250.5
    }
  ]
}
