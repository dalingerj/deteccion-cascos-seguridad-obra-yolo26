# Checklist de Gobernanza y Licencias

**Proyecto:** Deteccion de Cascos de Seguridad en Obra — Detección de Roles en Obra por Color de Casco  
**Autor:** Jonathan Dalinger
**Fecha:** Marzo 2026  
**Versión:** 1.0

---

## 1. Privacidad y Consentimiento

| Ítem | Estado | Notas |
|---|---|---|
| Las imágenes del dataset son de fuentes públicas con licencia libre | ✅ | Unsplash License |
| No se incluyen imágenes con personas identificables sin consentimiento | ✅ | Imágenes de stock genéricas |
| Los rostros presentes en las imágenes no son el objeto de detección | ✅ | El modelo detecta cascos, no personas |
| El dataset no contiene datos personales (nombre, DNI, biometría) | ✅ | Solo imágenes visuales de cascos |
| El modelo no puede usarse para identificar individuos específicos | ✅ | Clasificación por color, no por identidad |

---

## 2. Minimización de Datos

| Ítem | Estado | Notas |
|---|---|---|
| Solo se recopilan imágenes necesarias para el objetivo de detección de cascos | ✅ | ~150 imágenes totales, suficiente para el problema |
| No se almacenan metadatos de geolocalización ni información EXIF sensible | ✅ | Imágenes descargadas sin EXIF de identificación |
| El dataset no se comparte públicamente sin revisión de privacidad | ⚠️ | Dataset en Roboflow con acceso controlado |

---

## 3. Declaración de Limitaciones — Cuándo NO usar este modelo

Este modelo **no debe utilizarse** en los siguientes contextos:

1. **Toma de decisiones de seguridad en tiempo real sin supervisión humana:** El modelo puede generar falsos negativos (no detectar un casco presente). Usarlo como único control de acceso o seguridad sin revisión humana representa un riesgo inaceptable.

2. **Condiciones de iluminación extrema:** El modelo fue entrenado principalmente con imágenes diurnas, con saturacion, tono, brillo y contraste constante. No se recomienda su implementacion bajo condiciones de iluminacion atipicas.

3. **Obras con convenciones de color no estándar:** El esquema de colores asumido (blanco=ingeniería, amarillo=operario, etc.) puede variar según país, empresa o normativa local. El modelo no es transferible sin re-etiquetado.

4. **Identificación de individuos:** El modelo detecta clases de casco, no identidades. No debe integrarse en sistemas de reconocimiento facial o seguimiento de personas.

5. **Imágenes de baja resolución o muy lejanas:** Cascos con menos de 20×20px en la imagen tienen alta probabilidad de no ser detectados.

---

## 4. Nota de Riesgos — FP vs FN

| Tipo de error | Consecuencia potencial | Severidad |
|---|---|---|
| **Falso Negativo (FN)** — No detectar un casco | No se registra la presencia de un rol. Ej: no se detecta que un inspector HSE abandonó la zona. | 🔴 Alta |
| **Falso Positivo (FP)** — Detectar una clase incorrecta | Se asigna un rol incorrecto. Ej: un operario es identificado como supervisor. | 🟡 Media |

---

## 5. Declaración de Licencia

### Licencia del Código
Este repositorio se distribuye bajo licencia **MIT**.

```
MIT License — Copyright (c) 2026 Jonathan Dalinger
Se permite el uso, copia, modificación y distribución con o sin fines comerciales,
siempre que se mantenga el aviso de copyright original.
```

### Derechos del Dataset
| Componente | Origen | Licencia |
|---|---|---|
| Imágenes base | [Unsplash](https://unsplash.com) | [Unsplash License](https://unsplash.com/license) — uso libre incluyendo fines educativos |
| Anotaciones (bounding boxes) | Elaboración propia | MIT (incluidas en este repositorio) |
| Modelo pre-entrenado base | Ultralytics YOLO26 | [AGPL-3.0](https://github.com/ultralytics/ultralytics/blob/main/LICENSE) |

---

## 6. Contacto y Responsabilidad

Este modelo fue desarrollado con fines **exclusivamente académicos** en el marco de la Maestría en Inteligencia Artificial Aplicada a la Arquitectura y Construcción (Zigurat, 2026). No se garantiza su uso en entornos productivos sin validación adicional.

**Responsable del proyecto:** Jonathan Dalinger

**Institución:** Zigurat Institute of Technology 

**Año:** 2026
