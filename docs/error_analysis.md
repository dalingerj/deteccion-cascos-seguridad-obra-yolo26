# Análisis de Errores

---

## Falsos Positivos (FP) — El modelo predice una clase incorrecta

### FP-1: `blue_helmet` clasificado como `background` (6 casos)
- **Qué:** 6 instancias de `blue_helmet` fueron descartadas y clasificadas como fondo.
- **Por qué:** El azul oscuro en condiciones de sombra o lejanía reduce el contraste con fondos grises y metálicos típicos de obra. El modelo no tiene suficientes ejemplos de cascos azules en esas condiciones.

### FP-2: `white_helmet` y `yellow_helmet` clasificados como `background` (5 y 6 casos)
- **Qué:** Instancias de cascos blancos y amarillos no detectadas, absorbidas por la clase fondo.
- **Por qué:** Probable oclusión parcial o cascos muy pequeños en el frame (trabajadores a distancia). Las curvas muestran variabilidad en recall durante épocas intermedias, lo que sugiere dificultad con instancias de tamaño reducido.

### FP-3: `green_helmet` clasificado como `background` (1 caso)
- **Qué:** Un casco verde no detectado, absorbido por fondo.
- **Por qué:** `green_helmet` es la clase con menor representación en el dataset. Con pocas instancias de entrenamiento, el modelo tiene menor capacidad de generalización para esta clase.

---

## Falsos Negativos (FN) — El modelo no detecta un casco presente

### FN-1: Cascos no detectados en escenas con múltiples personas
- **Qué:** En escenas con grupos de trabajadores, algunas detecciones son parciales (se detecta 1 de 3 cascos visibles).
- **Por qué:** Oclusión entre personas y solapamiento de bounding boxes reduce la confianza del modelo por debajo del umbral de 0.25.

### FN-2: `green_helmet` con recall bajo
- **Qué:** Solo 4 detecciones correctas de `green_helmet` en validación.
- **Por qué:** Dataset desbalanceado — `green_helmet` tiene significativamente menos instancias que `white_helmet` (18) o `yellow_helmet` (16).

### FN-3: Cascos vistos desde atrás o en ángulo bajo
- **Qué:** Casos donde el casco es visible pero desde atrás generan confianza baja (ej: `red_helmet 0.6`).
- **Por qué:** El dataset probablemente tiene mayoría de imágenes frontales o de 3/4. La variación de ángulo no está suficientemente cubierta.

---

## 3 Mejoras Prioritarias del Dataset

### Mejora 1 — Balancear las clases
- **Problema vinculado:** FP-3, FN-2
- **Acción:** Llevar todas las clases a un mínimo de 15–20 instancias de validación. Priorizar `green_helmet` y `blue_helmet` con nuevas imágenes o data augmentation con hue shift controlado.

### Mejora 2 — Incorporar imágenes con oclusión y grupos
- **Problema vinculado:** FP-2, FN-1
- **Acción:** Añadir imágenes panorámicas de obra con múltiples trabajadores en cuadro, incluyendo oclusiones parciales naturales entre personas.

### Mejora 3 — Diversificar ángulos de captura
- **Problema vinculado:** FN-3
- **Acción:** Incluir imágenes con cascos vistos desde atrás, desde altura (dron) y en ángulo picado. Esto mejora la robustez ante cámaras de seguridad con montaje elevado, caso de uso frecuente en obras reales.
