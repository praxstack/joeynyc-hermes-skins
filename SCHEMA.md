# Hermes Skin Schema

Complete reference for all configurable skin keys.

## Top-Level Structure

```yaml
name: myskin                    # Required. Must match filename.
description: Short description  # Optional but recommended.

colors: { ... }       # 28 color keys (hex strings; all optional except name)
spinner: { ... }      # 4 spinner keys (lists)
branding: { ... }     # 6 branding keys (strings)
tool_prefix: "┊"      # Single character prefixed to tool output lines
tool_emojis: { ... }  # Per-tool emoji overrides
banner_logo: |        # Rich-markup ASCII art logo (replaces HERMES_AGENT banner)
banner_hero: |        # Rich-markup hero art (replaces caduceus art)
```

## Colors (28 keys)

| Key | What it colors | Default |
|-----|----------------|---------|
| `banner_border` | Panel border around startup banner | `#CD7F32` (bronze) |
| `banner_title` | Title text in banner | `#FFD700` (gold) |
| `banner_accent` | Section headers in banner | `#FFBF00` (amber) |
| `banner_dim` | Muted text (separators, secondary labels) | `#B8860B` (dark goldenrod) |
| `banner_text` | Body text (tool names, skill names) | `#FFF8DC` (cornsilk) |
| `ui_accent` | General UI accent (highlights, active elements) | `#FFBF00` |
| `ui_label` | UI labels and tags | `#DAA520` (goldenrod) |
| `ui_ok` | Success indicators | `#4caf50` (green) |
| `ui_error` | Error indicators | `#ef5350` (red) |
| `ui_warn` | Warning indicators | `#ffa726` (orange) |
| `prompt` | Interactive prompt text | `#FFF8DC` |
| `input_rule` | Horizontal rule above input area | `#CD7F32` |
| `response_border` | Response box border (ANSI escape) | `#FFD700` |
| `status_bar_bg` | Prompt/TUI status bar background | `#1a1a2e` |
| `status_bar_text` | Status bar default text | `#C0C0C0` |
| `status_bar_strong` | Status bar highlighted text | `#FFD700` |
| `status_bar_dim` | Status bar separators/muted text | `#8B8682` |
| `status_bar_good` | Healthy context/status indicators | `#8FBC8F` |
| `status_bar_warn` | Warning context/status indicators | `#FFD700` |
| `status_bar_bad` | High-usage context/status indicators | `#FF8C00` |
| `status_bar_critical` | Critical context/status indicators | `#FF6B6B` |
| `voice_status_bg` | Voice status pill background | `status_bar_bg` |
| `completion_menu_bg` | Completion menu background | `#1a1a2e` |
| `completion_menu_current_bg` | Active completion row background | `#333355` |
| `completion_menu_meta_bg` | Completion metadata background | `completion_menu_bg` |
| `completion_menu_meta_current_bg` | Active completion metadata background | `completion_menu_current_bg` |
| `session_label` | Session label color | `#DAA520` |
| `session_border` | Session ID dim border color | `#8B8682` |

The 2026.4.23 release added status bar and completion menu keys. Older 15-color
skins still load because Hermes inherits missing values from `default`, but dark
custom skins should define the completion/status keys to avoid default menu/status
colors clashing with the theme.

## Spinner (4 keys)

| Key | Type | Description |
|-----|------|-------------|
| `waiting_faces` | list of strings | Faces cycled while waiting for API |
| `thinking_faces` | list of strings | Faces cycled during model reasoning |
| `thinking_verbs` | list of strings | Verbs shown in spinner messages |
| `wings` | list of [left, right] | Decorative brackets around spinner |

## Branding (6 keys)

| Key | Description | Default |
|-----|-------------|---------|
| `agent_name` | Banner title and status display | `Hermes Agent` |
| `welcome` | CLI startup message | `Welcome to Hermes...` |
| `goodbye` | Exit message | `Goodbye! ⚕` |
| `response_label` | Response box header label | `⚕ Hermes` |
| `prompt_symbol` | Symbol before user input | `❯` |
| `help_header` | /help command header | `(^_^)? Available...` |

## Other Keys

| Key | Type | Description | Default |
|-----|------|-------------|---------|
| `tool_prefix` | string | Character prefixed to tool output lines | `┊` |
| `tool_emojis` | dict | Per-tool emoji overrides `{tool_name: emoji}` | `{}` |

Valid tool names: `terminal`, `web_search`, `read_file`, `write_file`, `search_files`, `execute_code`, `browser_navigate`, `delegate_task`, `mixture_of_agents`, `memory`, `clarify`, `cronjob`, `process`, `todo`
| `banner_logo` | string | Rich-markup ASCII art logo | `""` |
| `banner_hero` | string | Rich-markup hero art | `""` |

## Rich Markup

`banner_logo`, `banner_hero`, `welcome`, and `goodbye` all support Rich console markup:

```
[bold #FFD700]Gold bold text[/]
[dim #555555]Dimmed text[/]
[#FF0000]Red text[/]
```

### Per-Character Gradients

You can apply a color gradient across text by wrapping each character in its own markup tag.
For example, a red-to-white gradient on the welcome message:

```yaml
welcome: "[bold #FF0000]S[/][bold #FF0404]K[/][bold #FF0909]Y[/]..."
```

Use an easing curve (e.g. `t^1.5`) so the primary color holds through most of the text
and the secondary color appears toward the end. See `skins/skynet.yaml` for a full example.

## Inheritance

Missing values inherit from the `default` skin. You only need to define what you want to change.

## Full Template

See [template.yaml](template.yaml) for a copy-paste starting point with all keys.
