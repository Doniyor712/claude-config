---
name: burp-mcp
description: Burp Suite MCP server ulangan (SSE, port 9876) — Claude Code' dan Burp tool'lari
metadata:
  type: project
---

Burp Suite MCP extension Claude Code'ga ulangan.

- **Transport:** SSE, endpoint `http://127.0.0.1:9876/` (root `/`, NOT `/sse` — `/sse` 404 beradi; server `?sessionId=` query param bilan ishlaydi)
- **Scope:** user (`~/.claude.json`), barcha loyihalarda mavjud
- **Qo'shilgan:** `claude mcp add --scope user --transport sse burp http://127.0.0.1:9876/`
- **O'chirish:** `claude mcp remove burp -s user`
- **25 tool:** proxy HTTP/WS history (+regex), send_http1/http2_request, send_to_intruder, create_repeater_tab, set_proxy_intercept_state, base64/url encode-decode, get/set user/project options, editor contents, organizer items.

Shart: Burp ochiq + MCP extension yoqilgan (9876 tinglaydi) bo'lishi kerak, aks holda ulanish uziladi. Tool'lar yangi `claude` sessiyasida faollashadi. Sana: 2026-08-26.

## Sozlangan theme/appearance (2026-08-26)
User options qo'llangan (MCP `set_user_options` orqali, `~/.claude` emas Burp user config'ga avtomatik saqlanadi):
- Theme (`display.user_interface.look_and_feel`): **Dark**
- UI font_size: **14**
- Zebra striping (`display.table_appearance.zebra_striping`): **false** (o'chirilgan)
- Editor shrift (`display.http_message_display.font_name`): **Fira Code** (ligaturali; `/usr/share/fonts/truetype/firacode/`)
- Editor font_size: **14**, font_smoothing: true, pretty_print_by_default: true

MUHIM: `set_user_options`/`set_project_options` ishlashi uchun Burp MCP tab'da **"Enable tools that can edit your config"** yoqilgan bo'lishi shart (default o'chiq).
Project options'da display/theme kaliti YO'Q — theme faqat user-level, barcha project'larga taalluqli.
Reusable helper: `/home/kali/burpmcp.sh <tool_name> '<json_args>'` (ba'zan katta javobda bo'sh qaytaradi — u holda inline SSE+POST usulini ishlatish kerak).
