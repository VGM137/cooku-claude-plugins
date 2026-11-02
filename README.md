# Cooku para Claude

Conectores oficiales de [Cooku](https://usecooku.com) empaquetados como plugins de
Claude. Instalarlos conecta el servidor MCP de Cooku ya configurado: nadie tiene
que copiar una URL.

| Plugin | Para quién | Servidor MCP | Acceso |
|---|---|---|---|
| `cooku-commerce` | Comensales | `https://api.usecooku.com/mcp/commerce` | Buscar restaurantes, menú, cotizar, pedir, reservar mesa |
| `cooku-restaurants` | Dueños y gerentes de restaurantes en Cooku | `https://api.usecooku.com/mcp/restaurant` | Analítica de solo lectura |

## Instalar

### Claude Code

```
/plugin marketplace add VGM137/cooku-claude-plugins
/plugin install cooku-commerce@cooku
/plugin install cooku-restaurants@cooku
```

Después, `/mcp`, elige el servidor de Cooku y pulsa **Authenticate**: se abre el
navegador para iniciar sesión.

### Claude (web, escritorio y Cowork)

**Customize › Plugins › Add**: añade este repositorio como marketplace, o sube el
zip de una carpeta de `plugins/`. Luego, en la pestaña **Connectors** del plugin,
pulsa **Connect** e inicia sesión.

## Inicio de sesión

Los dos usan OAuth 2.1 con PKCE contra `https://api.usecooku.com`. Cooku no
guarda ninguna clave en el plugin.

- **cooku-commerce:** el comensal recibe un código de 6 dígitos en su correo. El
  nombre, el correo y el teléfono de sus pedidos son los que dio al conectar.
- **cooku-restaurants:** el usuario inicia sesión con su cuenta de Cooku y elige
  qué organizaciones comparte. Solo pueden conectarlo los administradores de la
  organización y los gerentes de sucursal.

## Seguridad

- `cooku-commerce` siempre enseña la cotización y pide confirmación antes de
  crear un pedido. El pago en línea se hace en la página de Cooku, nunca en el
  chat.
- `cooku-restaurants` no escribe nada.
- Para cortar el acceso, desconecta el conector en Claude o escribe a
  hola@usecooku.com.

Privacidad: <https://usecooku.com/pa/politica-de-privacidad> ·
Términos para comensales: <https://usecooku.com/pa/terminos-comensales> ·
Soporte: hola@usecooku.com
