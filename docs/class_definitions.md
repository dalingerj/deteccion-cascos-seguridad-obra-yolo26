# Definición de Clases y Reglas de Etiquetado

## Contexto del Problema

En el sector de la construcción (AECO), el color del casco de seguridad es un estándar internacional
que identifica el rol del portador dentro de la obra. Este sistema permite al modelo de visión
artificial inferir la composición de roles presentes en una escena.

---

## Clases del Modelo

### `white_helmet` — Casco Blanco
- **Rol:** Ingeniero de obra, Director de proyecto, Visita técnica o ejecutiva
- **Contexto típico:** Persona que supervisa, revisa planos o acompaña recorridos de obra
- **Notas de etiquetado:** Color blanco puro o blanco con detalles reflectivos

### `yellow_helmet` — Casco Amarillo
- **Rol:** Operario general, Trabajador de construcción
- **Contexto típico:** Personal en tareas de albañilería, movimiento de materiales, encofrado
- **Notas de etiquetado:** Amarillo intenso; no confundir con naranja o dorado

### `green_helmet` — Casco Verde
- **Rol:** Inspector de seguridad, Técnico HSE (Health, Safety & Environment)
- **Contexto típico:** Personal realizando inspecciones, verificando EPP, tomando medidas
- **Notas de etiquetado:** Verde medio o verde lima; distinguir de fondos con vegetación

### `blue_helmet` — Casco Azul
- **Rol:** Supervisor, Capataz, Jefe de cuadrilla
- **Contexto típico:** Personal coordinando grupos de trabajo, dando instrucciones
- **Notas de etiquetado:** Azul medio o azul oscuro; no confundir con azul marino (negro)

### `red_helmet` — Casco Rojo
- **Rol:** Electricista, Personal en zona de peligro especial, Contratista especializado
- **Contexto típico:** Trabajos eléctricos, zonas restringidas, instalaciones especiales
- **Notas de etiquetado:** Rojo brillante; distinguir de cascos naranjas o vino

---

## Reglas Generales de Etiquetado

1. **Bounding box ajustado:** Encuadrar el casco completo con margen mínimo (~5px). Evitar incluir cuello, cara o fondo innecesario.
2. **Visibilidad mínima:** Etiquetar solo cascos con al menos 30% de la superficie visible.
3. **Color dominante:** Etiquetar según el color mayoritario visible, ignorando sombras locales.
4. **Superposición:** En cascos que se solapan, etiquetar cada uno por separado si se puede distinguir su clase.
5. **Imágenes ambiguas:** Si el color no puede determinarse con certeza, omitir esa instancia.
6. **Reflejo de luz:** No reclasificar un casco por reflejos especulares que alteren el color percibido.

---

## Distribución de Clases (Dataset)

> Completar con datos reales del dataset exportado desde Roboflow

| Clase | Instancias (train) | Instancias (val) |
|---|---|---|
| white_helmet | — | — |
| yellow_helmet | — | — |
| green_helmet | — | — |
| blue_helmet | — | — |
| red_helmet | — | — |
| **Total** | — | — |
