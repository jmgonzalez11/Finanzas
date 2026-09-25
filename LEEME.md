# Finanzas: instalación

La app tiene dos partes:

- **Backend (Google Apps Script):** `Code.gs` y `appsscript.json`. Corre dentro de tu cuenta Google, lee los correos de los bancos y guarda todo en una hoja de cálculo tuya.
- **App (web instalable, funciona sin internet):** `index.html`, `sw.js`, `manifest.json`, `icon-192.png` e `icon-512.png`. Tus datos quedan guardados en cada dispositivo y se sincronizan con el backend solo cuando tocas **Sincronizar**.

Tiempo estimado: unos 30 minutos la primera vez.

---

## Cómo aplicar una actualización

Cada versión nueva trae los archivos `index.html`, `sw.js` y `version.json`. Si también cambia `Code.gs`, te lo diré.

1. En el Mac, entra a tu repositorio en github.com → **Add file → Upload files**.
2. Arrastra **los tres archivos juntos** y presiona **Commit changes**.
3. Espera 1 o 2 minutos a que GitHub Pages publique.
4. En la app (iPhone o Mac): **Ajustes → Actualizaciones → Buscar actualización**. Si hay una versión nueva, se instala y la app se recarga sola.

La app también revisa sola al abrirse (como máximo una vez por hora) y muestra el aviso azul «Hay una versión nueva».

**Tus datos no se pierden:** la actualización borra solo la copia guardada de la página, no tus movimientos ni ajustes.

**Si el botón dice que ya tienes la última versión, pero te envié una más nueva:**
- lo más probable es que `version.json` no se haya subido,
- o que GitHub aún no termine de publicar.

**Si alguna vez `Code.gs` cambia:** pégalo en Apps Script y ve a **Implementar → Gestionar implementaciones → Editar → Versión: nueva**.

---

## Novedades de la versión 11

- **Lo facturado del mes en el Resumen.** Donde antes estaba el flujo de caja, ahora aparece lo facturado en el mes, según los estados de cuenta cuyo período termina en ese mes:
  - **Nacional:** el total a pagar que informa el banco, con la fecha límite. Si hay saldo a favor o pendiente del período anterior, se indica aparte, junto a las compras y cargos del período.
  - **Internacional:** las compras en dólares, su equivalente aproximado en pesos al dólar de hoy y lo que queda por pagar en dólares.
- **Ingresos y egresos, nacionales e internacionales**, justo debajo. Los egresos internacionales se muestran en dólares y en pesos.
- **Flujo del mes** (ingresos − egresos) en una línea bajo esa tabla.
- **Meses sin estado de cuenta:** si aún no subes el estado de cuenta del mes, el Resumen muestra el flujo de caja como antes.

**Diferencia entre ambas cifras:** lo facturado corresponde al período de la tarjeta (por ejemplo, 22/08 al 22/09), mientras que los ingresos y egresos corresponden al mes calendario. Por eso pueden diferir.

## Novedades de la versión 10

Todo funciona dentro de la app, con tus documentos. No necesita acceso a tus cuentas.

- **Deshacer cargas:** Resumen → **Historial de cargas**. Muestra las últimas 12 cargas de documentos (estado de cuenta, no facturados o cartola) con su período y cantidad de movimientos. «Deshacer» deja todo como estaba antes de esa carga. El historial queda guardado en cada dispositivo.
- **Comprobar contra el banco:** al subir un estado de cuenta, la app compara lo que leyó con los totales que informa el banco:
  - compras en una cuota,
  - cuotas del mes,
  - comisiones, impuestos y abonos,
  - pagos,
  - compras internacionales.

  Dice «Cuadra» o muestra la diferencia. En Deudas también verás el total a pagar según el banco.
- **Abonos y reversas del estado de cuenta:** se leen y se registran como reembolsos. Por ejemplo, una reversa de Mercado Libre o un impuesto anulado.
- **Categorizar gastos:** Movimientos → **Categorizar**, o desde Meses pasados.
  - Lista los comercios sin categoría, de mayor a menor gasto.
  - Al elegir una categoría, se aplica a todos sus cobros, pasados y futuros.
  - «Aplicar sugeridas» confirma de una vez las sugerencias obvias.
- **Subetiquetas:**
  - Comida: delivery; café y panadería; almuerzos y colaciones; restaurantes y bares.
  - Transporte: apps; bencina; estacionamiento; peajes y TAG; transporte público; vuelos y viajes.

  Se ven en cada movimiento y en el detalle de Meses pasados.
- **Tendencia de 6 meses:** al inicio de Meses pasados, una tabla de gasto por etiqueta con ▲ o ▼ cuando algo cambia más de 10% frente al mes anterior.
- **Cierre de mes:** al abrir la app en un mes nuevo, aparece el cierre del mes anterior. Muestra el resultado, dónde se fue el dinero comparado con lo habitual y un presupuesto propuesto para el mes que empieza (editable, se guarda con un toque). También puedes abrirlo desde cada mes en Meses pasados.
- **Alertas:** en el Resumen. Avisan de:
  - cobros inusualmente altos en un comercio,
  - posibles cobros repetidos (mismo comercio, monto y día),
  - cargos nuevos de la tarjeta frente al estado de cuenta anterior,
  - suscripciones nuevas,
  - alzas de precio.

  Cada alerta se puede descartar.

**Para actualizar:** sube `index.html`, `sw.js` y `version.json`, y en la app ve a Ajustes → **Buscar actualización**. `Code.gs` no cambió.

## Novedades de la versión 9

**Cargas sin duplicados («carga basal»).** Cada documento que subes pasa a ser la base de su período:
- **Estado de cuenta de tarjeta (PDF):** reemplaza todo lo cargado antes desde documentos de esa tarjeta en el período facturado (por ejemplo, del 24/07 al 21/08). Además, sus compras de ese período pasan a Movimientos, y sus pagos quedan como «pago de tarjeta».
- **No facturados:** reemplazan lo cargado antes para esa tarjeta desde el día siguiente al último período facturado hasta la fecha del documento.
- **Cartola de cuenta (PDF, Excel o CSV):** reemplaza lo cargado antes desde cartolas de esa cuenta entre sus fechas.

Subir el mismo documento dos veces, o uno más nuevo que se superpone, ya no duplica nada. Tus correcciones de nombre, categoría, cuotas y tipo se mantienen al recargar. Los correos que coinciden con un documento quedan ocultos detrás del documento.

**Importar desde la página principal:** Resumen → **«Importar cartola o estado de cuenta»**. La app reconoce sola si es un estado de cuenta, no facturados o una cartola en PDF. Si es Excel o CSV, te pregunta qué es.

**Transferencias entre tus cuentas:** ya no se cuentan como gasto.
- Se reconocen por el texto (traspaso, cuenta propia, entre cuentas, mismo titular) o por tus nombres en Ajustes.
- También se reconocen al emparejarlas: si sale un monto de una cuenta y entra el mismo monto en otra, con ±2 días de diferencia, ambas quedan como «entre mis cuentas».
- Los pagos de tarjeta desde la cuenta tampoco cuentan como gasto.
- Si una transferencia quedó mal, edítala, elige «Entre mis cuentas» y marca «usar este tipo en futuros movimientos».

**Meses pasados:** Resumen → **Meses pasados** (en el Mac, también en la barra lateral). Para cada mes muestra:
- ingresos por etiqueta,
- gastos únicos por etiqueta (Comida, Transporte, Compras, etc.),
- suscripciones por etiqueta (Streaming, Productividad, IA, Lectura),
- compras en cuotas,
- pagos de tarjetas y cuentas,
- movimientos entre tus cuentas,
- el monto final.

**Etiquetas nuevas:** Streaming (Netflix, Spotify, Prime Video, YouTube), Productividad (Microsoft 365, Dropbox, iCloud, TextExpander, Fantastical), IA (ChatGPT, Claude, Superwhisper) y Lectura (Audible, Storytel, Patreon).

**Para actualizar:** sube `index.html`, `sw.js` y `version.json`, y en la app ve a Ajustes → **Buscar actualización**. `Code.gs` no cambió.

## Novedades de la versión 8

- **Diseño oscuro con fondo negro.** Está en Ajustes → Diseño, con tres opciones: Claro, Oscuro o Según el sistema. «Según el sistema» cambia solo cuando tu iPhone o Mac pasa a modo oscuro.
- Los colores de ingresos, egresos, etiquetas y gráficos están ajustados para leerse bien sobre negro.
- Cada dispositivo recuerda su propio diseño.

**Para actualizar:** sube `index.html`, `sw.js` y `version.json` a GitHub. Luego, en la app, ve a Ajustes → **Buscar actualización**.

## Novedades de la versión 6

**Cómo actualizar:**
1. Sube `index.html` y `sw.js` a GitHub.
2. En Apps Script, reemplaza `Code.gs` (ahora reconoce «en N cuotas» en los correos).
3. Ve a **Implementar → Gestionar implementaciones → Editar → Versión: nueva**.

No hace falta volver a ejecutar `configurar`.

**Qué hay de nuevo:**

- **¿En cuotas?** Todo gasto tiene la pregunta Sí/No. Si marcas Sí, indicas:
  - el número de cuotas,
  - si tiene interés (y la tasa mensual),
  - la tarjeta.

  El valor de la cuota y la fecha de la primera cuota se calculan solos, según el corte de tu tarjeta. La compra aparece en Deudas. Cuando esa misma compra llega en un estado de cuenta o en los no facturados (mismo monto, ±4 días), manda el documento y no se cuenta dos veces.
- **Etiquetas de categoría** (Transporte, Comida, etc.) en cada ingreso y egreso, y una etiqueta con el número de cuotas.
- **Suscripciones a mano:** en la pestaña Suscripciones puedes:
  - agregar una que falte,
  - quitar una detectada por error. Sus cobros siguen como gastos normales.

  Si agregas una suscripción, indica cómo aparece en el banco para que los cobros reales se junten con ella.
- **Análisis** ahora tiene cuatro secciones:
  - **Resumen del mes:** cada categoría con su monto, su % del total y si está similar, levemente mayor/menor o bastante mayor/menor que lo habitual. En el mes en curso se compara con lo habitual a la misma altura del mes. Este resumen también se incluye en el texto para Claude.
  - **Recomendaciones:** plan para el mes siguiente (ingresos esperados, cuotas, pagos fijos, suscripciones, gasto habitual y margen) y recomendaciones concretas, con opción de pedirle a Claude un plan detallado.
  - **Consulta de compra:** escribes qué quieres comprar, el precio y cómo lo pagarías (contado o cuotas, con o sin interés). La app responde si se ve manejable, posible con cuidado o no recomendable ahora, y la mejor forma de hacerlo. Además arma la consulta para Claude. También se abre desde el Resumen con **«¿Me conviene una compra?»**.
  - **Honorarios.**

  En la consulta de compra, los umbrales son: cuotas y créditos bajo 30% de tus ingresos, y cuota bajo la mitad de tu margen mensual. Es un cálculo con tus datos, no una asesoría financiera.

## Novedades de la versión 5 (requiere actualizar también Code.gs)

**Cómo actualizar:**
1. Sube `index.html` y `sw.js` a GitHub, como siempre.
2. En Apps Script, reemplaza el contenido de `Code.gs` por el nuevo.
3. Ejecuta una vez `configurar`. Google pedirá permiso para **Calendar**, que usan los avisos de vencimientos.
4. Ve a **Implementar → Gestionar implementaciones → Editar → Versión: nueva**. La dirección `/exec` no cambia.

**Qué hay de nuevo:**

- **Movimientos no facturados.** Sube el PDF «Saldo y movimientos no facturados» (nacional o internacional) desde Movimientos o Deudas.
  - Cada movimiento se cruza con lo ya registrado: mismo monto, ±3 días.
  - Lo que ya estaba no se duplica; lo que falta se agrega.
  - Los pagos a la tarjeta se ignoran, y las anulaciones o reversas se compensan con su cargo.
  - Si vuelves a subir el mismo PDF (o uno más nuevo), solo se agrega lo nuevo.
  - Las compras del período también alimentan Deudas para estimar el próximo pago, hasta que subas el estado de cuenta facturado.
- **Egresos nacionales e internacionales**, separados en Movimientos y en el Resumen.
- **Movimientos fijos mensuales** (Movimientos → «Movimientos fijos»). Sirven para transferencias a tu familia, la cuota de un crédito o un sueldo fijo.
  - Indicas la fecha del primer pago y, si termina, la del último.
  - Cada mes se registra solo en su fecha. Si después llega el correo o la cartola del mismo pago, no se duplica.
  - Si marcas «Es el pago de una deuda», aparece en Deudas con las cuotas pagadas.
- **Proyección de fin de mes** en el Resumen. Suma lo que falta del mes: ingresos y pagos fijos, suscripciones por renovarse, cuotas de créditos y el gasto variable estimado.
- **Presupuesto por categoría** en el Resumen, con avisos al 80% y al 100%.
- **Costo de la tarjeta** en Deudas:
  - intereses de las compras en cuotas,
  - comisiones, seguros e impuestos,
  - estimado anual,
  - qué compras conviene prepagar primero (las de mayor tasa).
  - Para ver intereses y tasas, vuelve a subir el estado de cuenta.
- **Honorarios y Operación Renta** en Análisis: total bruto, retenciones y detalle por pagador, con descarga en CSV. Al registrar una boleta ahora puedes indicar el pagador.
- **Avisos en Google Calendar** (Ajustes). Crea un calendario «Finanzas» con los pagos de los próximos 60 días (tarjetas, cuotas, suscripciones y movimientos fijos). Cada evento avisa 3 días y 1 día antes, y se actualiza al sincronizar.
- **Muestras para ajustar el lector de correos.** En Apps Script, ejecuta `exportarMuestras`. Crea la hoja «muestras» con hasta 6 correos recientes por banco, con nombres, correos, RUT y números de cuenta o tarjeta tapados, junto con lo que entendió el lector.
  - Revisa la hoja antes de compartirla y borra cualquier dato personal que haya quedado.
  - Compárteme esa hoja para ajustar el lector a tus bancos.

---

## 1. Backend en Apps Script

1. Entra a [script.google.com](https://script.google.com) con la cuenta de Gmail donde llegan los vouchers y crea un **Proyecto nuevo**. Ponle de nombre «Finanzas».
2. Borra el contenido de `Código.gs` y pega el contenido completo de `Code.gs`.
3. Ve a **Configuración del proyecto** (ícono de engranaje), activa **Mostrar el archivo de manifiesto "appsscript.json"** y reemplaza ese archivo por el `appsscript.json` incluido. Esto fija la zona horaria en Santiago.
4. Vuelve al editor, elige la función `configurar` y presiona **Ejecutar**. Google pedirá permisos para:
   - leer Gmail (solo se leen los remitentes de los bancos que actives y los correos con la etiqueta «Finanzas»),
   - crear la hoja de cálculo,
   - consultar mindicador.cl (dólar y UF).

   Como es un script tuyo, Google mostrará «Google no verificó esta app»: entra a **Configuración avanzada → Ir a Finanzas**.
5. Abre **Ejecuciones** (o el registro) y copia el **TOKEN** que aparece. Trátalo como una contraseña.
6. **Implementar → Nueva implementación → Tipo: Aplicación web**
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier usuario**

   Copia la dirección que termina en `/exec`.

> «Cualquier usuario» es necesario para que la app se conecte sin iniciar sesión en Google en cada dispositivo. Sin el token, el script no entrega ni recibe datos. Si crees que el token se filtró, ejecuta `rotarToken` y pega el nuevo en la app.

Cuando cambies `Code.gs` más adelante, usa **Implementar → Gestionar implementaciones → Editar → Versión: nueva** para que la dirección `/exec` siga siendo la misma.

## 2. Publicar la app

La app necesita estar en una dirección `https` para funcionar sin internet y poder instalarse. La opción más simple y gratuita es GitHub Pages:

1. Crea un repositorio en GitHub (por ejemplo `finanzas`).
2. Sube `index.html`, `sw.js`, `manifest.json`, `icon-192.png` e `icon-512.png`. **No subas** `Code.gs` ni ningún respaldo `.json` con tus datos.
3. **Settings → Pages → Branch: main / root → Save.** En un minuto tendrás una dirección como `https://tuusuario.github.io/finanzas/`.

El código de la app no contiene datos ni el token: esos quedan solo en tus dispositivos. Por eso el repositorio puede ser público. Alternativa: Netlify Drop, arrastrando la carpeta.

## 3. Instalar en el iPhone y en el Mac

**iPhone o iPad:** abre la dirección en Safari → Compartir → **Agregar a pantalla de inicio**.

**Mac (macOS Sonoma 14 o posterior):** abre la dirección en Safari → **Archivo → Agregar al Dock**.
- Queda como una app propia: tiene ícono en el Dock y en Launchpad, abre en su propia ventana y funciona sin internet.
- En pantallas grandes cambia a diseño de escritorio: barra lateral, ingresos y egresos lado a lado, y resumen en dos columnas.
- También puedes instalarla desde Chrome con el ícono de instalar de la barra de direcciones.

**Conectar el primer dispositivo:** Ajustes → pega la dirección `/exec` y el token → **Probar conexión** → marca tus bancos → **Sincronizar**.

**Conectar los demás dispositivos:**
1. En el dispositivo ya configurado, toca **Copiar código para otro dispositivo**.
2. En el nuevo, pégalo en **¿Ya lo configuraste en otro dispositivo?**
3. Los bancos, tus nombres, los nombres de tarjetas y las reglas se copian solos.

Hay un solo archivo `index.html` para el iPhone y el Mac. Al subir la versión nueva a GitHub, ambas apps se actualizan solas la próxima vez que las abras.

**Cómo se mantienen iguales el Mac y el iPhone:** los dos sincronizan contra la misma hoja de Google.
- La app sincroniza sola al abrirla, al recuperar internet y cada 15 minutos mientras está abierta.
- Lo que editas se sube unos segundos después.
- Sin internet, todo sigue funcionando y se sube cuando vuelve la conexión.

**Atajos en el Mac:**

| Atajo | Acción |
|---|---|
| ⌘R | Sincronizar |
| ⌘N | Nuevo movimiento |
| ⌘1 a ⌘6 | Cambiar de sección (⌘4 es Deudas) |
| ⌘← y ⌘→ | Cambiar de mes |

> ¿Por qué no una app nativa de Mac? Sería otra app que mantener aparte y no agregaría funciones: la versión instalada desde Safari ya funciona sin internet, tiene su propio ícono y se actualiza sola cuando actualizas los archivos en GitHub.

La primera sincronización revisa los últimos 90 días (lo puedes cambiar en Ajustes). Si hay muchos correos puede quedar a medias; la app te avisa y basta con sincronizar otra vez. No se duplica nada.

## 4. Correos de Outlook

Apps Script solo lee Gmail. Para que los vouchers que llegan a Outlook entren a la app:

1. En Outlook: **Configuración → Correo → Reglas → Agregar regla**.
2. Condición: el remitente contiene `bancochile.cl`, `santander.cl`, `bancoestado.cl` (y los de tus otros bancos).
3. Acción: **Redirigir a** tu Gmail. Usa «Redirigir», no «Reenviar»: así el correo conserva el remitente original del banco y la app lo reconoce.

Si la cuenta de Outlook es institucional, es posible que la organización bloquee la redirección a correos externos. En ese caso, usa la importación de cartola para esos movimientos.

Opcional: en Gmail, crea la etiqueta **Finanzas** y aplícala con un filtro a cualquier otro remitente que quieras incluir.

## 5. Cartola

Descarga la cartola en Excel o CSV desde el sitio de tu banco. En **Ajustes → Importar cartola**, elige el banco y el archivo. La primera vez confirmas qué columna es la fecha, la descripción, los cargos y los abonos; la app lo recuerda para las siguientes.

La app no duplica movimientos:

- Los que ya llegaron por correo se ocultan como duplicados (mismo monto, sentido y fecha ±3 días; ±6 días para ingresos).
- Volver a importar la misma cartola no agrega nada.

## 6. Deudas

La pestaña **Deudas** junta dos cosas: las compras en cuotas de tus tarjetas y los créditos que ingreses a mano (consumo, hipotecario en UF, préstamos).

Para cada deuda muestra:
- **cuántas cuotas van pagadas** y cuántas faltan, con una barra de avance,
- cuánto queda por pagar,
- el valor de la cuota,
- el mes en que terminas.

Arriba verás la **deuda total**, el **próximo pago** y los **pagos de los próximos 6 meses**.

**Cómo se estiman las cuotas pagadas (por fechas):**
- En el estado de cuenta, una compra «05/06» significa que ese mes se cobra la cuota 5.
- Se cuentan 4 cuotas pagadas antes del estado de cuenta.
- Cuando pasa la fecha de «Pagar hasta», se cuenta la quinta.
- Cada mes siguiente, al pasar la misma fecha, se suma una más.
- Las compras «00/03» (primera cuota el mes siguiente) parten un mes después.

**Créditos ingresados a mano:** indicas el total de cuotas, las ya pagadas y el día de pago. La app suma una cuota pagada cada vez que pasa ese día.
- Si ingresas el **monto total**, el valor de la cuota se calcula solo (monto dividido por cuotas, sin intereses). Puedes cambiarlo.
- Un solo pago se registra como 1 cuota.

**Corregir una deuda:** toca cualquier compra en la lista de deudas. Puedes cambiar:
- el nombre,
- el monto,
- si tiene cuotas o no,
- cuántas cuotas tiene y cuántas llevas pagadas,
- el valor de la cuota.

Si no escribes el valor de la cuota, se calcula como el monto dividido por las cuotas, sin intereses. Mientras editas, un resumen muestra cuántas cuotas quedan, cuánto falta y cuándo terminas.

Las compras que el banco cobró sin cuotas aparecen en **«Compras sin cuotas del último estado de cuenta»**. Tócalas para pasarlas a cuotas.

**Quitar de deudas** saca un cargo de la lista. Se puede volver a marcar en **Revisar cargos**.

**Cerrar sin guardar:** todas las ventanas tienen una **×** arriba y un botón **Cancelar**. También se cierran tocando fuera de ellas o, en el Mac, con la tecla Esc.

La estimación supone que pagas cada estado de cuenta a tiempo. Sube el estado de cuenta nuevo cada mes: se usa el más reciente de cada tarjeta y corrige cualquier diferencia.

**Subir un estado de cuenta:** Deudas → **Subir estado de cuenta**. Acepta PDF, Excel o CSV.
- **PDF con clave:** la app la pide en el momento y no la guarda.
- Lee el **estado nacional** (en pesos) y el **internacional** (en dólares) del mismo PDF.
- Antes de guardar revisas los cargos, la fecha de pago y la tarjeta.
- **Las suscripciones se excluyen**, porque ya aparecen en su pestaña. Puedes corregirlo cargo por cargo.

Estas cifras son una proyección y **no suman al flujo**: cada compra ya se registró cuando la hiciste. Tampoco se descuentan los saldos a favor del período anterior.

**Probado con un estado de cuenta real de Banco de Chile:**
- Los totales de compras en cuotas, cargos del mes y compras en dólares coinciden exactamente con los del documento.
- La proyección de los próximos 4 meses difiere de la tabla «Vencimiento próximos 4 meses» del banco en menos de $25 por mes. La diferencia se debe al redondeo de la última cuota.

## 7. Datos de tarjeta

**La app no guarda números de tarjeta ni de cuenta.**
- Cada tarjeta aparece solo como «Tarjeta 1 Banco de Chile», «Tarjeta 2 Banco de Chile», etc. Puedes cambiarles el nombre en Ajustes o en la pestaña Tarjetas.
- Los números enmascarados (****1234, «terminada en 1234») se eliminan de los asuntos de correo y de las descripciones, tanto en la app como en la hoja de Google.
- De los estados de cuenta solo se guardan fechas, comercios, montos y cuotas. El nombre del titular, el correo, el número de tarjeta y la clave del PDF nunca se leen ni se guardan.

**Si ya habías instalado la versión anterior:**
1. Pega el `Code.gs` nuevo.
2. Crea una nueva versión de la implementación.
3. Ejecuta una vez `limpiarDatosTarjeta` para borrar los dígitos guardados antes.

La app también los elimina de cada dispositivo al abrirse.

## 8. Cómo cuenta el dinero

- **Suman al flujo:** ingresos, transferencias recibidas, gastos, transferencias enviadas, y descuentos o retenciones.
- **No suman al flujo:**
  - Transferencias entre tus cuentas. Se reconocen con tus nombres y RUT en Ajustes.
  - Pagos de tarjeta de crédito, porque cada compra ya se contó.
  - Duplicados.
- **Sueldo:** si ingresas el líquido y el bruto, el ingreso es el bruto y la diferencia aparece como «Descuentos legales del sueldo» en egresos. El flujo neto queda igual al líquido.
- **Boleta de honorarios:** marca la casilla y registra el bruto. La retención se calcula según el año: 15,25% en 2026, 16% en 2027 y 17% desde 2028.
- **Si ya registraste el sueldo a mano** y después llega por correo la transferencia del mismo monto líquido, la transferencia se oculta como duplicado.

## 9. Si un correo no se reconoce

Cada banco usa plantillas distintas y las cambia de vez en cuando. En **Ajustes → Correos no reconocidos** verás los que no se pudieron leer.

En Apps Script, la función `probarLector` muestra en el registro qué entiende de tus últimos correos bancarios, sin guardar nada. Con dos o tres ejemplos reales por banco (puedes borrar montos y nombres) se ajustan los patrones de `parseEmail` en `Code.gs`.

## Archivos

| Archivo | Dónde va |
|---|---|
| `Code.gs`, `appsscript.json` | Proyecto de Apps Script |
| `index.html`, `sw.js`, `version.json`, `manifest.json`, `icon-192.png`, `icon-512.png` | GitHub Pages u otro hosting `https` |
