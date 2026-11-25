# cooku-commerce

Pide comida y reserva mesa en restaurantes que usan [Cooku](https://usecooku.com)
sin salir de Claude: buscar restaurantes, ver el menú, cotizar, hacer el pedido
(para recoger, a domicilio o a tu mesa cuando estás en el local), seguir su
estado y reservar mesa.

## Qué incluye

- **Conector MCP remoto** `cooku-commerce` →
  `https://api.usecooku.com/mcp/commerce` (HTTP, OAuth). Es el mismo servidor
  que el conector de Cooku para comensales, así que no se duplican herramientas.
- **Skill** `pedir-y-reservar-en-cooku`: le enseña a Claude el orden de las
  herramientas y las reglas de confirmación antes de pedir o reservar.

El plugin no ejecuta programas en tu equipo, no instala paquetes, no tiene hooks
y no guarda claves: solo declara la URL del servidor y la skill.

## Herramientas

| Herramienta | Qué hace | Escribe |
|---|---|---|
| `search_restaurants` | Busca restaurantes por nombre, zona o tipo de comida | No |
| `get_menu` | Menú con precios, opciones, alérgenos y disponibilidad | No |
| `quote_order` | Calcula el total exacto; devuelve un `quoteId` de 10 minutos | No |
| `create_order` | Crea el pedido de una cotización confirmada por el usuario | Sí |
| `get_order_status` | Estado del pedido y del pago | No |
| `check_availability` | Horas libres para reservar una fecha y número de personas | No |
| `reserve_table` | Pide una reserva; queda pendiente hasta que el restaurante confirma | Sí |
| `find_destination` | Comprueba la mesa o el lugar del local donde estás (habitación, coworking, área común) por el código impreso bajo el QR o el enlace del QR | No |
| `link_destination` | Enlace de 15 minutos para escanear el QR de tu mesa con el teléfono | Sí |
| `forget_destination` | Olvida el lugar que escaneaste cuando ya no estás ahí | Sí |

**Pedir a la mesa.** Solo en restaurantes que lo activan. Claude te pide el
código de 8 caracteres impreso bajo el QR de tu mesa (o te da un enlace para
escanearlo) y, si el lugar lo exige, el PIN de 6 dígitos que tiene el local.
Antes de pedir confirma contigo el lugar junto con el total. Ni el código ni el
PIN salen de Cooku.

## Instalar

En Claude Code:

```
/plugin install cooku-commerce --marketplace VGM137/cooku-claude-plugins
```

En Claude (web, escritorio y Cowork), búscalo en el directorio o añade este
repositorio como marketplace en **Customize › Plugins**.

## Conectar

1. Instala el plugin y pulsa **Connect** (Claude) o `/mcp` → **Authenticate**
   (Claude Code).
2. Escribe tu correo en la página de Cooku y luego el código de 6 dígitos que te
   llega.
3. Tu nombre, correo y teléfono se usan en los pedidos y reservas; Claude no
   tiene que pedírtelos.

## Qué datos se envían y a dónde

Todo va solo a `api.usecooku.com`: lo que busques, los platos que elijas, la
dirección de entrega si pides a domicilio, el código y el PIN de la mesa si
pides en el local, las notas para la cocina y los datos de contacto que diste al
conectar. Cooku los comparte con el restaurante al que
le pides o reservas, para que pueda atenderte. El pago en línea, cuando el
restaurante lo exige, se hace en la página de pago de Cooku en tu navegador:
Claude nunca ve ni recibe datos de tarjeta.

## Seguridad

- Claude siempre te enseña el desglose y el total y espera tu «sí» antes de
  crear un pedido, y confirma restaurante, fecha, hora y personas antes de
  reservar.
- Hay límites por persona: 5 pedidos por hora y 15 al día; 3 reservas por hora
  y 6 al día.
- Para cortar el acceso, desconecta el conector o escribe a hola@usecooku.com.

## In English

Order food (pickup, delivery, or to your table when you are at the restaurant,
using the code printed under the table's QR and, if required, a 6-digit PIN)
and book tables at restaurants that run on Cooku. The plugin adds the remote MCP server `https://api.usecooku.com/mcp/commerce`
(OAuth with an email code) and one skill that makes Claude quote first, show the
total and wait for the user's explicit confirmation before `create_order` or
`reserve_table`. It runs nothing locally; data goes only to Cooku and to the
restaurant the user orders from; card payments happen on Cooku's pay page in the
browser, never in the chat.

Privacidad / Privacy: <https://usecooku.com/pa/politica-de-privacidad> ·
Términos / Terms: <https://usecooku.com/pa/terminos-comensales> ·
Soporte / Support: hola@usecooku.com
