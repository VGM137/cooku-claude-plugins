# cooku-restaurants

Pregúntale a Claude por tu restaurante en [Cooku](https://usecooku.com): ventas,
productos más vendidos, márgenes y food cost, comparativas entre periodos,
cierres de caja, alertas de inventario y ocupación de reservas. **Solo lectura:**
ninguna herramienta cambia nada en Cooku.

## Qué incluye

- **Conector MCP remoto** `cooku-restaurants` →
  `https://api.usecooku.com/mcp/restaurant` (HTTP, OAuth). Es el mismo servidor
  que el conector de Cooku para restaurantes, así que no se duplican herramientas.
- **Skill** `analitica-de-restaurante-cooku`: le enseña a Claude a empezar por el
  contexto del negocio, a usar fechas locales y a avisar cuando el plan recorta
  el histórico.

El plugin no ejecuta programas en tu equipo, no instala paquetes, no tiene hooks
y no guarda claves: solo declara la URL del servidor y la skill.

## Herramientas

| Herramienta | Qué hace |
|---|---|
| `business_context` | Negocios y sucursales a los que tienes acceso, zona horaria, moneda, fecha de hoy y límites del plan |
| `sales_summary` | Ingresos, pedidos, ticket medio, propinas y descuentos, por día, método de pago y tipo de pedido |
| `compare_periods` | Compara un rango con el periodo anterior, el año pasado o un rango propio |
| `top_products` | Ranking de productos por ingreso o por unidades |
| `margins` | Margen bruto y costo de lo vendido por día de una sucursal (requiere recetas) |
| `inventory_alerts` | Alertas del reporte diario de inventario: stock bajo, mermas, variaciones, precios de proveedor |
| `cash_closes` | Cierres diarios (Z): ventas, impuestos, propinas, efectivo esperado y contado |
| `reservation_occupancy` | Reservas y cubiertos por día y ocupación estimada (requiere reservas) |

## Conectar

1. Instala el plugin y pulsa **Connect** (Claude) o `/mcp` → **Authenticate**
   (Claude Code).
2. Inicia sesión con tu cuenta de Cooku y elige qué organizaciones compartes con
   Claude. Solo pueden conectarlo los administradores de la organización y los
   gerentes de sucursal.

## Qué datos se envían y a dónde

Las preguntas llegan a `api.usecooku.com` como llamadas a las herramientas
(periodo, sucursal, filtros). Las respuestas son cifras agregadas de tu propio
negocio; no incluyen datos de tarjetas. Nada se envía a terceros. Cooku registra
cada llamada (herramienta, fecha y resultado) para seguridad y soporte.

## Seguridad

- Todas las herramientas son de solo lectura.
- Para cortar el acceso, revoca la conexión en Cooku › Ajustes › Integraciones,
  desconecta el conector en Claude o escribe a hola@usecooku.com.

## In English

Read-only analytics for restaurants that run on Cooku: sales, top products,
margins and food cost, period comparisons, cash closes, inventory alerts and
reservation occupancy. The plugin adds the remote MCP server
`https://api.usecooku.com/mcp/restaurant` (OAuth with the user's Cooku account;
org admins and branch managers only) and one skill on how to query it. It runs
nothing locally and sends nothing to third parties.

Privacidad / Privacy: <https://usecooku.com/pa/politica-de-privacidad> ·
Soporte / Support: hola@usecooku.com
