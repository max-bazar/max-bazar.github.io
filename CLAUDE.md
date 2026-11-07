# CLAUDE.md — Max Bazar

> Primera lectura antes de cualquier tarea en este repo.

---

## 1. Qué es este proyecto

Sitio de la tienda Max Bazar: una sola página (`index.html`) con catálogo, carrito, pago con Mercado Pago, pedidos enviados a un Apps Script de Google y contacto por WhatsApp. Las imágenes están en `img/`.

## 2. Cómo se publica

- GitHub Pages desde `main`: **cada merge publica el sitio**. No hay build ni tests.
- Se trabaja en una rama por cambio y se abre un PR. El merge lo hace Maxi.
- Para probar en local: `python3 -m http.server 8000` y abrir `http://localhost:8000`.

## 3. Reglas duras

1. Nunca generar pedidos ni pagos reales al probar. Llamar al script de pedidos o a Mercado Pago pide confirmación (`.claude/guardas.json`).
2. No agregar claves, tokens ni datos de clientes al repo: el sitio es público, incluida la carpeta `.claude/`.
3. Revisar el sitio en celular (375 px de ancho) y en escritorio antes de pedir el merge.

---

---

## 4. Riesgo, revisión y subagentes

> Viene de `malbeldas/prompts` `base/`. Las guardas de `.claude/` bloquean lo prohibido; esta sección dice cuándo usar cada cosa.

**Al empezar cada issue, declarar en el plan el riesgo y el modo.**

| Riesgo | Qué es | Antes de pedir el merge |
|---|---|---|
| R0 | Textos, docs, estilos, tests | CI en verde |
| R1 | Lógica y pantallas comunes | CI en verde; `revisor-riesgo` si el PR pasa de 800 líneas |
| R2 | Toca un área sensible, aunque sea una línea | CI en verde + `revisor-riesgo` obligatorio |

- **Áreas sensibles de este proyecto:** carrito, checkout y pago con Mercado Pago, el envío de pedidos al Apps Script, precios y datos de contacto o medios de pago.
- **Modo:** por defecto se trabaja sin subagentes. Si el issue toca 2 capas o más y se estima en más de 800 líneas, o en más de 3.000, proponer partirlo antes de empezar. Las líneas generadas por script no cuentan.
- **Encargo al revisor:** issue, riesgo, `base <sha> · rama · head <sha>` y áreas tocadas. Una pasada completa; si hubo correcciones, otra solo sobre el diff. Sin pasadas de rutina.
- **Hallazgos [alta]:** se corrigen, o se decide con el humano, antes del merge.
- **Cupo del plan:** antes de lanzar un subagente, mirar el uso de la cuenta. Si el semanal va más de 10 puntos por encima de lo transcurrido de la semana, o el de 5 horas pasa del 70 %, solo se revisa R2. Por encima del 90 %, no se lanzan subagentes: se deja el trabajo prolijo y lo pendiente anotado en el issue. R2 nunca se saltea por cupo: el PR espera.
- **Descripción del PR:** una línea `Riesgo: R? · Revisor: <veredicto> o no aplica · Cupo semanal: <inicio> → <fin>`.
- **Si una guarda bloquea algo,** no se rodea: se reporta.

