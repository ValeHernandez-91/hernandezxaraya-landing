# Puesta en marcha — hernandezxaraya.cl

Guía paso a paso para dejar el sitio 100% funcional. Todo es **gratis**.
Dominio: `hernandezxaraya.cl` (registrado en NIC Chile). Correo principal: `hola@hernandezxaraya.cl`.

Orden recomendado: **1 → 2 → 3 → 4 → 5**. Las fases 6 y 7 son opcionales.

---

## Resumen de lo que ya quedó listo en el código

- ✅ Formulario de contacto real (nombre, email, tipo de proyecto, mensaje) con envío AJAX y mensajes de éxito/error.
- ✅ Los botones **"Cotizar Esencial / Producto / Evolución"** pre-seleccionan el plan en el formulario.
- ✅ Todos los emails apuntan a `hola@hernandezxaraya.cl`.
- ✅ WhatsApp con mensaje pre-escrito.
- ✅ Botón **"Reservar una reunión"** (apunta a Cal.com).

Lo único que falta es **conectar las cuentas externas** (abajo). Hay 2 valores que debes reemplazar en el código:

1. `REEMPLAZAR_CON_TU_ACCESS_KEY` en `index.html` → tu Access Key de Web3Forms (Fase 4).
2. `https://cal.com/hernandezxaraya` en `index.html` → tu link real de Cal.com (Fase 6), si tu usuario es distinto.

---

## Fase 1 — Cloudflare + apuntar el dominio (DNS)

> Cloudflare nos da, gratis y en un solo lugar: hosting (Pages), correo (Email Routing) y DNS.

1. Crea una cuenta en **https://dash.cloudflare.com/sign-up** (gratis).
2. **Add a site** → escribe `hernandezxaraya.cl` → elige el plan **Free**.
3. Cloudflare escaneará los DNS actuales y te mostrará **2 nameservers** del tipo:
   ```
   xxxx.ns.cloudflare.com
   yyyy.ns.cloudflare.com
   ```
4. Entra a **NIC Chile** → https://www.nic.cl → inicia sesión → **Mis dominios** → `hernandezxaraya.cl` → **Editar / Cambiar servidores de nombre (DNS)**.
5. Borra los servidores actuales y pon los **2 de Cloudflare**. Guarda.
6. Vuelve a Cloudflare y pulsa **Check nameservers / Done**.

⏳ La delegación puede tardar de minutos a ~24 h. Cloudflare te avisa por email cuando el dominio quede **Active**. No sigas con las fases 2 y 3 hasta que esté activo.

---

## Fase 2 — Correo corporativo gratis (recibir)

> Con **Email Routing** recibes los correos de `@hernandezxaraya.cl` en tu Gmail actual. Gratis e ilimitado.

1. En Cloudflare → tu dominio → menú **Email** → **Email Routing** → **Get started / Enable**.
2. Cloudflare agrega solo los registros **MX** y **SPF** necesarios (acepta).
3. **Destination addresses** → agrega tu Gmail personal y **confírmalo** (te llega un correo de verificación).
4. **Routing rules** → **Create address**:
   - `hola@hernandezxaraya.cl` → tu Gmail.
   - (Opcional) `valentina@hernandezxaraya.cl` y `jonathan@hernandezxaraya.cl` → cada uno a su Gmail.
   - (Opcional) Activa **Catch-all** para que cualquier `loquesea@hernandezxaraya.cl` también llegue.

✅ Listo: ya **recibes** correo corporativo. Para **responder mostrando** `hola@hernandezxaraya.cl`, sigue la Fase 5.

---

## Fase 3 — Publicar el sitio (Cloudflare Pages)

**Opción A — desde GitHub (recomendada, se actualiza solo):**
1. Sube este repo a GitHub (si aún no está).
2. Cloudflare → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → elige el repo.
3. Build settings: **Framework preset = None**, **Build command = (vacío)**, **Output directory = `/`** (es un sitio estático, sin build).
4. **Deploy**. Cada `git push` a `main` re-publica automáticamente.

**Opción B — subida directa (sin Git):**
- **Workers & Pages** → **Create** → **Pages** → **Upload assets** → arrastra los archivos del proyecto.

**Dominio propio:**
- En el proyecto de Pages → **Custom domains** → **Set up a domain** → `hernandezxaraya.cl` (y `www`). Como el DNS ya está en Cloudflare, se configura solo.

---

## Fase 4 — Formulario de contacto (recibir leads)

> El formulario usa **Web3Forms**: gratis, sin backend, envía cada mensaje a tu correo.

1. Entra a **https://web3forms.com** → pon `hola@hernandezxaraya.cl` (o tu Gmail) → te llega un **Access Key**.
2. Abre `index.html`, busca `REEMPLAZAR_CON_TU_ACCESS_KEY` y reemplázalo por tu key.
3. Guarda y vuelve a desplegar (push o re-upload).
4. Prueba: completa el formulario en el sitio → debe llegarte el correo.

> Plan gratis: 250 envíos/mes. Más que suficiente para una landing.

---

## Fase 5 — Responder mostrando `hola@hernandezxaraya.cl` (enviar)

> Cloudflare Email Routing solo **recibe**. Para **enviar/responder** desde Gmail mostrando tu dominio,
> Gmail necesita un servidor SMTP. Usamos **Brevo** (gratis, 300 correos/día).

1. Crea cuenta en **https://www.brevo.com** (gratis).
2. En Brevo → **SMTP & API** → **SMTP** → copia: servidor `smtp-relay.brevo.com`, puerto `587`, tu login y la **SMTP key**.
3. En Gmail → ⚙️ **Ver toda la configuración** → **Cuentas e importación** → **Enviar como** → **Añadir otra dirección**:
   - Nombre: `Hernández × Araya`
   - Email: `hola@hernandezxaraya.cl`
   - Desmarca "Tratar como alias" si quieres firmar siempre como el dominio.
   - SMTP: `smtp-relay.brevo.com`, puerto `587`, usuario y SMTP key de Brevo, conexión **TLS**.
4. Gmail enviará un correo de verificación a `hola@` → como ya tienes routing (Fase 2), te llega → confirma.
5. (Recomendado) En **Enviar como**, marca `hola@hernandezxaraya.cl` como **predeterminada**.

✅ Ahora recibes y respondes como `hola@hernandezxaraya.cl`, todo gratis.

> Alternativa más simple (buzón propio independiente): **Zoho Mail** plan gratis (hasta 5 cuentas) hace recibir+enviar
> sin SMTP externo. Si prefieres eso en vez de Cloudflare+Brevo, avísame y te dejo esos pasos.

---

## Fase 6 — Agenda de reuniones (autogestión)

> **Cal.com** (gratis, open-source) deja que el cliente reserve una reunión solo.

1. Crea cuenta en **https://cal.com** → elige tu usuario, ej. `hernandezxaraya`.
2. Conecta tu Google Calendar para que muestre tu disponibilidad real.
3. Crea un tipo de evento, ej. "Conversemos · 30 min".
4. Tu link será `https://cal.com/hernandezxaraya/...`. Si tu usuario o evento difiere de
   `https://cal.com/hernandezxaraya`, actualízalo en `index.html` (botón "Reservar una reunión").

---

## Fase 7 — Cotización / pagos online (opcional, fase 2)

> Para cobrar online en Chile, lo más simple sin backend son los **links de pago**.

- **MercadoPago** → crea un "Link de pago" por monto y reemplaza/añade un botón que apunte a ese link.
- **Flow.cl** o **Webpay (Transbank)** → integración formal (requiere inicio de actividades en SII y más configuración).
- Por ahora el formulario ya **captura el plan/cotización** que pide el cliente, que es el primer paso del flujo.

Cuando quieras activar pagos, avísame y lo integramos.

---

## Checklist rápido

- [x] Fase 1 — Dominio apuntando a Cloudflare (Active). NS: athena/rajeev.ns.cloudflare.com
- [x] Fase 2 — `hola@` llega a tu Gmail (Email Routing activo, MX+SPF publicados)
- [x] Fase 3 — Sitio publicado y online en https://hernandezxaraya.cl (HTTPS OK)
- [x] Fase 4 — Web3Forms conectado y formulario probado (leads llegan al Gmail)
- [ ] Fase 5 — Responder como `hola@` desde Gmail (PENDIENTE, ver nota abajo)
- [ ] Fase 6 — Link de Cal.com creado y puesto en el sitio
- [ ] Fase 7 — (Opcional) Pagos online

---

## Dónde quedamos (retomar aquí)

**Funcionando hoy:** sitio online con dominio + HTTPS, recibe correo en `hola@`, y el formulario manda leads.

**Pendiente — Fase 5 (responder como `hola@`):**
- Cuenta Brevo creada. SMTP probado: servidor `smtp-relay.brevo.com`, puerto `587`,
  login `aee1a4001@smtp-brevo.com`. La clave SMTP funciona (el envío devolvió `250`).
- **Problema:** el correo de prueba no llegó al Gmail. Causa probable: cuenta nueva de Brevo
  retenida/en revisión, y/o falta autenticar el dominio (sin SPF/DKIM de Brevo → spam).
- **Próximos pasos mañana:**
  1. Revisar **Brevo → Transaccional → Logs** para ver si salió "Delivered" (revisar Spam) o "Blocked".
  2. Autenticar el dominio en **Brevo → Remitentes, Dominios e IPs** → agregar `hernandezxaraya.cl`
     → copiar los registros (brevo-code TXT, DKIM, SPF/DMARC) y agregarlos en Cloudflare DNS.
  3. Terminar en Gmail: **Configuración → Cuentas e importación → Enviar como** con los datos SMTP de arriba.
- **Alternativa si Brevo sigue dando lata:** Zoho Mail (plan gratis) = buzón propio que recibe y envía
  sin SMTP externo. Más simple, bandeja aparte del Gmail.

**Pendiente — Fase 6 (agenda):** crear cuenta en Cal.com y poner el link real en `index.html`
(botón "Reservar una reunión", hoy apunta a `https://cal.com/hernandezxaraya`).

**Nota deploy:** el sitio se publicó por **subida directa** (archivo `hernandezxaraya-site.zip`),
no por Git, porque la app de Cloudflare en GitHub no tiene permiso sobre el repo de `ValeHernandez-91`.
Para auto-deploy en cada push, instalar la app de Cloudflare Pages en la cuenta GitHub de Valentina.
Por ahora, para actualizar el sitio: re-generar el zip y re-subirlo, o conectar Git con Vale.
